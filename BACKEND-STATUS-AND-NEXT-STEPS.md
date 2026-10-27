# TPMC backend preparation package (based on latest uploaded index-4.html)

## Source and changes
- Source used: the latest uploaded `index-4.html` (about 5.1 MB), not the earlier `index.html`.
- Output homepage: `index.html` (renamed for GitHub Pages).
- Existing Google OAuth entry points are disabled in this build so Google authentication can be configured separately. Email/ID login code is retained.
- Includes the latest uploaded `manifest.webmanifest`.

## Critical backend status
This package is NOT yet connected to a live backend. The source file itself has empty `window.SCL_SUPABASE_URL` and `window.SCL_SUPABASE_PUBLISHABLE_KEY` values. The connected Supabase account currently lists no projects, so there is no known project URL/key/schema/functions to connect to or deploy into.

Uploading this ZIP alone cannot make server-side features work: GitHub Pages serves static files only. To finish the real connection, provide access to the intended Supabase project (or explicitly authorize creation of a new project, which may incur cost), then reconcile and deploy database migrations, RLS policies, Edge Functions, Storage buckets, secrets, and Auth settings against the actual index4.html calls. Never put a service-role/secret key in `index.html`.

## Before publishing
1. Extract and back up the current repository.
2. Upload `index.html` and `manifest.webmanifest` to the site root. The manifest references `icon-192.png` and `icon-512.png`; ensure both files exist in that same root or change manifest paths to actual files.
3. Do not describe admin tools, profiles, admissions, attendance, salaries, or documents as live until the real backend is connected and tested.
4. Google sign-in is intentionally disabled here; configure it separately after the Supabase project and allowed redirect URLs are known.

## Audit findings from index-4.html
- Supabase URL and publishable key are blank.
- The page expects Supabase Auth, database RPCs/tables, and multiple Edge Function endpoints.
- It contains calls for roles such as `developer`, `technical_admin`, `management_admin`, and `affairs_admin`, and multiple administrative workflows. Their presence in the UI does not prove database permissions or server handlers exist.
- It includes `/api/*` paths; GitHub Pages cannot serve those as server endpoints. Those calls must be mapped to deployed Edge Functions or an actual API server.
- The manifest references icon-192.png and icon-512.png, which were not supplied with this upload package.
