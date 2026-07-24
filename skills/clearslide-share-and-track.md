---
name: Share a presentation and track engagement
description: Create a trackable link for a ClearSlide presentation and read back engagement insights.
api: openapi/clearslide-openapi.yml
operations: [getPresentations, postLinks, getInsights]
---

# Share a ClearSlide presentation and track engagement

Use this flow to turn an existing ClearSlide presentation into a trackable link and then read the
engagement statistics it generates.

## Auth
- OAuth 2.0. Register a client redirect URL with `apisupport@clearslide.com` to receive a client id
  and secret, then obtain a bearer token from `https://oauth.platform.clearslide.com/oauth/token`
  (authorization_code or password grant). Send `Authorization: Bearer <access_token>`.
- Scope: `read` for listing/insights, `write` for creating links.

## Steps
1. **Find the presentation** — `GET /presentations` (`getPresentations`). Results are sorted
   descending by `dateModified` and paginated at page size 100. Pick the target presentation id.
2. **Create a trackable link** — `POST /links` (`postLinks`) referencing that presentation.
3. **Read engagement** — `GET /insights` (`getInsights`) to retrieve statistics for the sent pitch.

## Notes
- No idempotency-key contract is documented; avoid blind retries on `POST /links`.
- Base URL: `https://platform.clearslide.com`.
