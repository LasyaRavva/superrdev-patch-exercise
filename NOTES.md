# Patch notes

## Summary of changes

Fixed the task-search predicate so archived records are never returned and the selected status applies to title and description matches. I updated the matching H2 and Oracle reference SQL. The API no longer deliberately sleeps before every search; it validates filters and pagination, and delegates paging/counting to the database instead of loading every match into memory. The UI resets to page one when a filter changes and cancels obsolete requests, preventing older responses from replacing newer results. A backend integration test covers the search regression and invalid input.

## Not changed

I did not add task creation, authentication, authorization, or new indexes: they are outside this focused read-only search patch and need product/security requirements or production data before implementation.

## Biggest remaining risk

The current case-insensitive `%term%` search will not scale well on a large production data set. It should be reviewed with real query plans and likely replaced with database-specific full-text/search indexes.

## Tools/AI used

Used Codex to inspect the codebase, identify the predicate and request-lifecycle defects, draft the patch, and run checks. I reviewed the resulting changes and test intent.
