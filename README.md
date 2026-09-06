# mo2-node-ci

Express quote API used to demonstrate a Node.js CI pipeline running lint, unit tests and
integration tests as separate quality gates.

## Layout

| Path | Purpose |
| --- | --- |
| `src/pricing.js` | Pure pricing rules: line totals, discounts, VAT |
| `src/app.js` | Express app exposing `/health` and `/quote` |
| `tests/unit` | Tests for the pricing rules in isolation |
| `tests/integration` | Tests driving the running app through HTTP via supertest |

## CI

`.github/workflows/ci.yml` runs three jobs on every push and pull request to `main`:

- **lint** — ESLint flat config across the repository.
- **unit-tests** — `vitest run tests/unit`.
- **integration-tests** — `vitest run tests/integration`, gated on `unit-tests` passing.

`.github/workflows/dependency-review.yml` runs `dependency-review-action` on pull requests
and fails the check when a dependency introduces a vulnerability of **high** severity or above.

All three CI jobs are required status checks on `main`.

## Running locally

```bash
npm ci
npm run lint
npm run test:unit
npm run test:integration
```
