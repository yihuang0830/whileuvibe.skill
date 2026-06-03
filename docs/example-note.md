# Study Note: Building the Login Feature

> *This is an example of what `/study-note` generates — written using the actual code from the session.*

## 1. What We Built

We built a login system where users can enter their email and password, submit a form, and stay logged in across page refreshes. Under the hood, the backend verifies the password, creates a session token, and sends it back to the browser.

## 2. Files Changed

- `app/login/page.tsx` — The login form UI and the code that sends the request
- `app/api/login/route.ts` — The backend endpoint that receives the form data and does the verification
- `lib/auth.ts` — Reusable functions for hashing passwords and generating session tokens
- `lib/db.ts` — Database queries for looking up users by email

## 3. Main Technical Concepts

### 3.1 POST vs GET

We used `POST` instead of `GET` for the login request. Here's why that matters:

```ts
// app/api/login/route.ts
export async function POST(req: Request) {
  const { email, password } = await req.json()
  ...
}
```

With `GET`, data goes in the URL: `yoursite.com/login?password=abc123`. That means it's visible in browser history, server logs, and anyone looking over your shoulder. `POST` sends data in the request body — invisible in the URL. For anything sensitive, always use `POST`.

**Analogy:** GET is like writing on a postcard. POST is like putting it in an envelope.

### 3.2 Password Hashing

We never store the actual password. We store a hash — a scrambled version that can't be reversed.

```ts
// lib/auth.ts
import bcrypt from 'bcrypt'

export async function hashPassword(password: string) {
  return bcrypt.hash(password, 10)
}

export async function verifyPassword(password: string, hash: string) {
  return bcrypt.compare(password, hash)
}
```

Why not just store the password? Because databases get hacked. If attackers get a list of hashed passwords, they still can't log in — they don't know the original password, and hashes can't be reversed. `bcrypt.compare()` works by hashing the input and checking if the result matches the stored hash.

### 3.3 Session Tokens

After login succeeds, the server creates a token — a random string that proves "this person has already logged in."

```ts
// lib/auth.ts
export function createSessionToken(userId: string) {
  return jwt.sign({ userId }, process.env.JWT_SECRET, { expiresIn: '7d' })
}
```

The browser stores this token (usually in a cookie or localStorage). On every future request, it sends the token back. The server checks: "is this a valid token?" If yes, the user is authenticated. No need to log in again.

**Analogy:** Like a wristband at a concert. You prove your identity once at the door, and for the rest of the night, the wristband is your proof.

## 4. Data Flow

```
User enters email + password
    ↓
Frontend sends POST /api/login
    ↓
Backend extracts email + password from request body
    ↓
DB query: find user by email
    ↓
bcrypt.compare(password, user.passwordHash)
    ↓  (if match)
Create JWT session token
    ↓
Return token to frontend
    ↓
Browser stores token in localStorage
    ↓
User is now "logged in"
```

## 5. Important Code Decisions

### Decision 1: Validate input on the server, not just the frontend

Even though the form already checks that email and password are filled in, the API route checks again:

```ts
if (!email || !password) {
  return Response.json({ error: 'Missing fields' }, { status: 400 })
}
```

Why? Because users (or attackers) can skip your frontend entirely and send requests directly with `curl` or Postman. Never trust that your frontend ran.

### Decision 2: Auth logic lives in `lib/auth.ts`, not in the route

The route file only calls `verifyPassword()` and `createSessionToken()` — it doesn't implement them. This means if you need login in another route later, you just import the same functions. It also means the route file stays readable.

## 6. Bugs We Encountered

### Bug: Login always returned "Invalid credentials" even with correct password

**Symptom:** The form submitted successfully but every login attempt failed, even with the right password.

**Root cause:** The backend was comparing the raw password string directly against the stored hash:

```ts
// WRONG
if (password !== user.passwordHash) { ... }
```

This is always false because `"mypassword123"` will never equal `"$2b$10$..."` (a bcrypt hash).

**Fix:** Use `bcrypt.compare()` which knows how to check a password against its hash:

```ts
// CORRECT
const valid = await verifyPassword(password, user.passwordHash)
```

## 7. What You Should Remember

- **POST for sensitive data** — passwords, payment info, anything you wouldn't want in a URL
- **Never store raw passwords** — always hash, always use a library like bcrypt (don't write your own)
- **Session tokens are proof of prior login** — the server issues them, the browser stores them, and they expire
- **Validate on the server too** — frontend validation is just UX; it's not security
- **Keep auth logic in one place** — a `lib/auth.ts` that gets imported everywhere beats copy-pasting into every route

## 8. Quiz

1. Why do we use `POST` instead of `GET` for the login form?
2. If the database gets hacked and attackers see all the stored password hashes, can they log in to user accounts? Why or why not?
3. What does a session token prove, and how does the server know it's valid?
4. If you only validated input on the frontend and skipped server-side validation, what could go wrong?
5. What file would you edit if you wanted session tokens to expire after 1 day instead of 7?

## 9. Rebuild Challenge

**Implement logout without AI help.**

**Goal:** When the user clicks "Log out," invalidate their session so they can't use the old token anymore.

**Hints:**
- For a simple version: just delete the token from localStorage on the frontend
- For a more secure version: keep a server-side list of invalidated tokens (look up "token blacklist" or "token revocation")

**What you'll practice:** Understanding the full lifecycle of a session — not just login, but what it means for a session to end.
