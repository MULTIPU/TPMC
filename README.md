# The Pees Model College (TPMC) — Website Setup & Completion Checklist

**School:** The Pees Model College  
**Location:** Epe, Lagos, Nigeria  
**Motto:** Greater Glory  
**Supported school classes:** JSS 1, JSS 2, JSS 3, SSS 1, SSS 2, SSS 3  
**Frontend:** Static HTML/CSS/JavaScript (GitHub Pages compatible)  
**Backend target:** Supabase (project access/configuration must be confirmed)

## What this package is

`index.html` is the refined frontend source based on the latest available refined TPMC HTML in this workspace. It includes UI polish, a centered-logo styling pass, interaction/focus effects for tabs, a rendered-text cleanup for literal `\n`/`\r` artifacts, JSS1–SSS3 class choices in the curriculum helper, and separate Practical Lesson and Vocational Lesson selection cards.

**Important:** the two lesson cards currently provide selection feedback only. They are not proof of saved registrations or attendance records. Backend integration and workflow testing are still required. No live deployment is performed by this package.

## Deploy on GitHub Pages

1. Back up the repository and current deployed `index.html`.
2. Upload this package's `index.html` to the repository root, replacing the homepage only after review.
3. Keep the existing assets, workflows, source directories, and configuration files unless the project maintainer confirms they are unused.
4. In GitHub, open **Settings → Pages** and verify the correct branch/folder and deployment status.
5. Open the published site on a phone and desktop; clear cache or use a private window to avoid seeing an old version.

## Required school information

Fill in and verify these items before public launch:

- Official name spelling, crest/icon files, motto, physical address and map location.
- Main phone numbers, official email, office hours and approved WhatsApp contacts/group invite links.
- Admissions criteria, application dates, fees, payment instructions and refund policy.
- School calendar, term dates, subjects, approved class list (JSS 1–3 and SSS 1–3), grading scale and promotion rules.
- Staff names, titles, approved profile photographs, subjects/roles and consent to publish.
- Privacy notice, data-retention policy, safeguarding/child-protection contact and terms of use.
- Accurate notices, policies, uniforms, school photos, practical-lesson rules and vocational offerings.
- Emergency contact details and the responsible person for website content.

## Supabase/backend information required

Before implementation, the project owner must identify the existing Supabase project (do not create a duplicate blindly) and provide access through the connected Supabase integration. Record these non-secret values in deployment configuration:

- Supabase project URL.
- Publishable key (safe for browser use when RLS is correctly configured).
- Project reference and deployment environments (development/production).
- Existing database schema, migrations, tables, triggers, RLS policies, storage buckets and Edge Functions.
- Authentication providers currently enabled and allowed redirect URLs.
- Public site URL and any custom domain.

**Never put a Supabase `service_role` key, secret API key, OAuth client secret, database password, or private credentials in `index.html`, a public repository, or browser storage.** Keep privileged secrets only in Supabase Edge Function secrets or another server-side secret manager.

## Roles and permissions to implement and test

- Technical Administrator: technical configuration, service health, role assignment and approved operational tasks; no unrestricted data access by default.
- School Management Administrator: school settings, admissions, classes, staff and approved academic/financial workflows.
- Teacher/staff: only assigned classes, attendance and permitted academic records.
- Student: own profile, own class information and permitted learning resources.
- Parent/guardian: linked child records only, where the school supports guardian accounts.

Role authorization must be enforced by database RLS and server-side checks, not merely by hiding UI buttons or trusting editable user metadata. Provision the first administrator through a controlled owner-approved process; never allow public sign-up to grant administrator privileges.

## Functional completion checklist

### Identity and access
- [ ] Email/password or chosen non-Google sign-in works, including recovery and logout.
- [ ] Google authentication is configured separately when OAuth credentials and redirect URLs are ready.
- [ ] Roles are assigned securely and unauthorized access is denied server-side.
- [ ] Session expiry, error messages, duplicate accounts and account recovery are tested.

### School data
- [ ] Student admission/profile create, read, update and approval work end-to-end.
- [ ] Staff profile and role changes persist and are permission checked.
- [ ] Only JSS 1, JSS 2, JSS 3, SSS 1, SSS 2 and SSS 3 are offered for applicable school-class calculations, reports and admissions workflows.
- [ ] Curriculum/lesson reference content is distinguished from student records and current academic data.
- [ ] Grading, results, promotion, attendance and reports use the approved school rules.

### Practical and vocational lessons
- [ ] Practical Lesson and Vocational Lesson remain distinct activity types.
- [ ] Registration accepts eligible students from any of the six supported classes (confirm whether “any previous class” means only JSS1–SSS3 or includes alumni; school must decide).
- [ ] Attendance records each activity type separately, with date, session, student, class, instructor and attendance status.
- [ ] Duplicate registration/attendance, corrections and authorized exports are handled.
- [ ] Backend writes and reads are verified; frontend selection alone is not sufficient.

### Fees and sensitive data
- [ ] Fee/payment records are reconciled with the chosen payment provider and never marked paid from an unverified browser callback.
- [ ] Salary, payment, guardian and student records have strict least-privilege policies.
- [ ] Audit trails exist for approvals and changes to sensitive records.
- [ ] Uploads have file type/size validation, private buckets where appropriate and restricted download policies.

### Technical operations
- [ ] All API routes referenced in the HTML are mapped to deployed server-side services; GitHub Pages cannot run `/api/*` server routes by itself.
- [ ] Database migrations are versioned and reviewed before production.
- [ ] RLS is enabled for every exposed table and policies are tested as each role.
- [ ] Supabase advisors and logs are checked; backups and restore procedures are documented.
- [ ] Forms have loading, success, empty, offline and error states; no fake success messages.
- [ ] Mobile, keyboard navigation, contrast, reduced motion and major browsers are tested.
- [ ] No secrets, test credentials, debug data or placeholder contact details remain in public assets.

## Recommended database entities (confirm against existing schema before creating)

Possible tables include `profiles`, `user_roles`, `students`, `guardians`, `staff`, `classes`, `subjects`, `enrollments`, `attendance_sessions`, `attendance_records`, `lesson_types`, `lesson_registrations`, `results`, `fee_invoices`, `payments`, `announcements`, `documents`, and `audit_events`. This is a planning list, **not a claim that these tables already exist**. Inspect the existing database first to avoid duplicates or data loss.

## Launch acceptance tests

1. Sign in as each role and verify both allowed and denied actions.
2. Create a test student in JSS 1 and another in SSS 3; verify class filters and reports.
3. Register a test student for Practical Lesson and Vocational Lesson separately; verify separate attendance entries persist after refresh and a second device/session.
4. Verify staff updates persist, and an ordinary user cannot edit another user's profile or change their own role.
5. Verify fees/payments cannot be forged by changing browser data.
6. Test no-network, invalid form, expired session and unauthorized API responses.
7. Verify the published GitHub Pages build uses the correct asset paths and manifest.

## Current limitations / handover notes

- This package is a frontend refinement, not a backend deployment.
- Supabase project discovery previously returned no accessible projects through the connected tool, so the actual project, schema, RLS policies and functions remain unverified.
- Google OAuth must be configured separately in Supabase and the Google Cloud project once the production URL is known.
- Lesson registration and attendance need real database integration before they should be represented as operational.
- Do not remove old repository files until dependency and deployment checks confirm they are unnecessary.
