# Test plan — Research_Agent_AI

## Scope

This repository contains no application code: its entire tree is the
product's licence (AGPL-3.0), product terms (TERMS.md), README, and funding
configuration. Testing therefore covers the repository's document set —
that it is internally consistent and navigable — and nothing else. There is
no engine behaviour to test here, because the engine's source is not in
this repository; product-level criteria (build, a product test suite,
static analysis of product code) cannot be evidenced from this tree and
are recorded as such in the OpenSSF filing pack, not smoothed over. When
the source is published here, this plan must be rewritten around the real
suites in the same change that lands them.

## Suites

| Suite | Covers | Run it | Runs in CI |
|---|---|---|---|
| Validator tests (`tests/test_check_docs.py`) | The validator itself: a valid set passes; a broken relative link fails; an empty document fails; external links are not treated as files | `python3 -m unittest discover -s tests -v` | Yes — `.github/workflows/ci.yml` |
| Document validation (`scripts/check_docs.py`) | Every `*.md` file is non-empty and UTF-8 readable; every relative Markdown link resolves to a file that exists | `python3 scripts/check_docs.py` | Yes — `.github/workflows/ci.yml` |

## CI gates

- Validator test suite and document validation green on every push and
  pull request to `main`; a broken relative link, an empty/unreadable
  document, or a failing validator test blocks merge.

## Cadence

- Every pull request: validator tests + document validation.
- Every release candidate: the release-readiness run (checker + evidence
  reads), per the house Release-Readiness Standard.

## Coverage bar

No numeric floor; new or edited documents land with the validation check
passing, per CONTRIBUTING.
