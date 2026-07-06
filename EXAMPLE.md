# Example: Agent Behavior With Battle Tested Engineer

This file shows how an agent should behave when following [`skills/battle-tested-engineer/SKILL.md`](skills/battle-tested-engineer/SKILL.md).

**Two output modes:**

| Mode | When | Style |
|------|------|-------|
| Code work | Explaining approach, status, tradeoffs during implementation | Ultra-terse fragments |
| Artifacts | Commit messages, PR descriptions, security warnings, clarifying questions | Normal complete prose |

---

## 1. Think before code

**User:** Fix the login bug.

**Bad (guesses):**

> I'll update the JWT refresh logic and add retry handling to the auth middleware.

**Good (states assumption or asks):**

> "Login bug" could mean:
>
> 1. Wrong error on bad password
> 2. Session lost after refresh
> 3. Redirect loop after OAuth
>
> Which? Or steps to reproduce?

**User:** Bad password shows 500, should be 401.

**Good:**

> Assumption: `POST /api/login` throws uncaught on `bcrypt.compare` fail. Check handler first.

---

## 2. Simplicity

**User:** Add email validation to the signup form.

**Bad (over-build):**

> I'll create `EmailValidatorService`, `ValidationRule` interface, config for TLD allowlist, and unit tests for each rule.

**Good:**

> ~5 lines: regex or `validator` pkg already in deps. No new abstraction.

```typescript
const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
if (!emailRegex.test(email)) {
  return { error: 'Invalid email' };
}
```

---

## 3. Surgical change

**User:** Rename `getUser` to `fetchUser` in `userService.ts`.

**Bad:**

> Renamed function. Also fixed inconsistent quotes, removed unused import in `auth.ts`, reformatted `userService.ts`.

**Good:**

> Renamed `getUser` → `fetchUser` in `userService.ts` + call sites. `auth.ts` has unused import — out of scope, left alone.

**Diff:** only rename-related lines.

---

## 4. Data vs UI

**User:** Add loading state to `UserProfile.tsx`.

**Bad:**

```tsx
function UserProfile() {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  useEffect(() => { fetch('/api/user').then(...) }, []);
  // fetch + transform + render all in component
}
```

**Good:**

> Data in hook. Component render only.

```tsx
// useUserProfile.ts — fetch, loading, error
// UserProfile.tsx — layout from hook return
```

```tsx
function UserProfile() {
  const { user, status } = useUserProfile();
  if (status === 'loading') return <Spinner />;
  if (status === 'error') return <ErrorBanner />;
  return <ProfileCard user={user} />;
}
```

Mock user shape matches API contract. Lives in `__mocks__/user.ts`, not inline in component.

---

## 5. Goal-driven execution

**User:** Make the checkout more reliable.

**Bad:**

> I'll refactor checkout into a state machine and add logging.

**Good:**

> Vague. Proposed goal: "Payment succeeds on first try when card valid; user sees clear error when declined."
>
> Verify:
> 1. Valid card → `order.status === 'paid'`
> 2. Declined card → error message, no duplicate charge
>
> Start with failing test for duplicate charge on retry?

---

## 6. Tests

**User:** Add tests for `calculateDiscount`.

**Bad:**

> 12 tests: every branch, private helper, mock internals.

**Good:**

> 3 tests — public contract only:
>
> 1. No code → full price
> 2. Valid code → discounted total
> 3. Expired code → error, full price
>
> Can't name regression for "calls `lookupPromo` twice" → skip.

---

## 7. Propose spec when need

**User:** Add multi-tenant support across the app.

**Bad:**

> I'll start by adding `tenantId` to the User model.

**Good (short spec first):**

> Wide blast radius. Minimal spec before code:
>
> **Problem:** Single-tenant DB; need tenant isolation.
> **Decision:** Row-level `tenant_id` + middleware inject from JWT subclaim.
> **Alternative:** DB-per-tenant — rejected, ops cost.
> **Consequence:** All queries need tenant filter; migration backfills `default` tenant.
>
> Approve approach? Then slice: auth middleware first.

Small/obvious ask (e.g. typo fix) → skip spec, just fix.

---

## 8. Ship then improve

**User:** Add export-to-CSV on the reports page.

**Bad:**

> Build streaming exporter, worker queue, progress UI, cancel support — then wire button.

**Good:**

> v1: client-side CSV from current table data. Button works. Streaming/queue later if rows > 10k in prod.

Plan: failing test → minimal pass → refactor only if tests still green.

---

## 9. Gut-check (internal, before responding)

Before sending diff or summary, agent checks:

- Assumption stated, not guessed?
- Every changed line traces to request?
- Refactor labeled structural-only, behavior unchanged?
- Tests few, each names a real bug?

If any "no" → fix or say tradeoff out loud.

---

## Output style examples

### During code work (terse)

**User:** Why did the build fail?

**Good:**

> `tsc` error line 42 `UserProfile.tsx`: `user` possibly undefined. Add guard or optional chain.

Not:

> I ran the build and unfortunately it looks like TypeScript encountered an issue on line 42...

### Security warning (normal prose)

**Good:**

> The API key is hardcoded in `config.ts`. Move it to an environment variable and rotate the exposed key before merging. Committed secrets stay in git history even after deletion.

Then resume terse for implementation steps.

### Commit message (normal prose)

```
fix(auth): return 401 when password comparison fails

Login handler let bcrypt errors bubble as 500. Catch compare
failure and map to 401 so clients can show the correct message.
```

### PR description (normal prose)

```markdown
## Summary
- Map failed password comparison to 401 on `POST /api/login`
- Add characterization test for invalid password response

## Test plan
- [ ] Invalid password returns 401 with `{ error: "Invalid credentials" }`
- [ ] Valid login still returns 200
```

---

## Full mini-session (good)

**User:** Users report cart total wrong when quantity changes.

**Agent:**

> Need repro. Assumption: stale total — `quantity` updates but `lineTotal` not recalculated. Check `CartItem` first.

*(reads code)*

> Confirmed. `setQuantity` updates state; `subtotal` derived once on mount. One-line fix: derive `subtotal` from `items` in render or `useMemo`.

*(writes failing test, then fix)*

> Test: change qty 1→3, total triples. Green.

**Commit message:**

```
fix(cart): recalculate subtotal when item quantity changes

Subtotal was computed only on mount, so quantity updates did not
update the displayed total. Derive subtotal from items on each render.
```

**Agent (terse wrap-up):**

> Done. `useMemo` on `items`. One test. No cart refactor.

---

## When skill should not apply

Trivial ask — use judgment, skip ceremony:

**User:** Fix typo "recieve" → "receive" in README.

**Good:**

> Fixed.

No plan, no spec, no test.
