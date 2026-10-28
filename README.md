# The Pees Model College — repaired website package

This is a repair of the existing TPMC HTML source, not a replacement design. The access-gate structure and existing school features are preserved while the specified conflicts are corrected.

## Publish together

Upload `index.html`, `manifest.webmanifest`, `icon-192.png`, `icon-512.png`, and the complete `assets/` folder together to the root of the intended TPMC GitHub Pages deployment. Do not upload only `index.html`: images are now stored once in `assets/` instead of repeatedly embedded in the HTML.

## Included fixes

- Supabase project URL and publishable browser key set to TPMC project `uecpngekrrbrxtquhrdm`.
- Existing access gate structure retained; Google OAuth still depends on enabling/configuring Google provider credentials in Supabase.
- School wallpaper set as the light-mode background; existing dark-mode palette retained; profile modal keeps its own background.
- Visible theme control positioned top-left; school badge centred above homepage navigation.
- Nigerian flag and coat of arms side-by-side at the same display size, without labels.
- Actual TPMC contacts populated; WhatsApp chooser includes each listed role and call links; school and technical admin emails included.
- Active registration and fee class options restricted to JSS 1–SSS 3; separate Primary Section placeholder remains.
- Timetable periods: Mon–Thu has eight 45-minute lessons and closes at 3:30 PM; Friday has seven 45-minute lessons plus fellowship and closes at 3:30 PM.
- Practical Lesson and Instructional Lesson controls included.
- Removed the visible literal `\n` artefact and externalized embedded raster images to shared local assets.

## Required before public launch

1. In Google Cloud Console, create/select a Web OAuth client and add this authorized redirect URI to that client:
   `https://uecpngekrrbrxtquhrdm.supabase.co/auth/v1/callback`
2. In Supabase Dashboard → Authentication → Sign In / Providers → Google, enable Google and enter the OAuth client ID and secret. Add the live website URL to Supabase Auth URL configuration. Never place the Google client secret or Supabase service-role key in this package.
3. The Supabase project currently has no TPMC application tables/migrations or Edge Functions. Database schema, RLS policies, and the frontend's API contracts still need to be implemented and tested before registrations, fees, results, attendance, and staff administration can be called fully live.
4. The GitHub integration can read the TPMC repository but write operations are currently denied. Publish only after write access is granted or an authorized maintainer uploads the package.

## Validation performed

- 133 inline JavaScript blocks passed `node --check`.
- All local image/manifest/icon paths referenced by the HTML were checked.
- No embedded raster base64 URIs remain in the HTML.
- The class picker contains only the six secondary classes.
- Timetable period durations were checked: all teaching periods are 45 minutes.
- A live browser visual test could not be completed in this environment.
