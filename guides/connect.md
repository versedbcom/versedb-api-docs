---
title: Connect to VerseDB
description: Get a read-only token for a member's account through an OAuth 2.0 authorization-code flow with PKCE.
order: 4
---

Lets a third-party site get a read-only token for a member's account without the member
copying one by hand. It is an OAuth 2.0 authorization-code flow with PKCE (S256).

1. Generate a random `code_verifier` (43-128 characters) and a `state`, and keep both on your
   server. The `code_challenge` is the base64url-encoded SHA-256 of the verifier, without padding.
2. Send the member to `https://versedb.com/connect` with `redirect_uri`, `state`,
   `code_challenge`, `code_challenge_method=S256`, and optionally `client_name` (your app, such as
   `WordPress`, 40 characters at most), `site_name` (100 at most) and `scope` (a space-separated
   subset of `read:public read:showcase`; both by default). `redirect_uri` must be HTTPS, or
   `http://localhost` while developing.
3. The member signs in if needed and approves or denies. VerseDB redirects to `redirect_uri` with
   `code` and `state`, or with `error=access_denied` and `state` when they deny. Check that
   `state` matches.
4. Within 5 minutes, exchange the code at `POST /api/v1/connect/token` from your server.

The token is named "{client_name}: {your host}", lasts 365 days, shows in the member's My Apps
page and counts toward their limit of 10 active tokens. Connecting the same site again replaces
its previous token. `read:showcase` reads the member's profile, collection, wishlist, pull list and
reading progress for display, without email, birth date, location, prices, notes, storage or loans.
