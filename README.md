# Samy Gamal Isakhron — Psychology & Mental Wellbeing

## Current deliverable
A bilingual (English/Arabic) responsive static preview. Open index.html in a browser. Use the header language switcher; the preference is stored locally in the browser. The footer's Admin demo opens an in-memory dashboard with clearly fictional data, filters, a chart, and demo CSV import/export. The booking form validates required fields, privacy consent, and Cairo-local dates. With the professional WhatsApp number configured, it opens a prefilled WhatsApp draft; the visitor must review and tap Send in WhatsApp. The site itself does not submit or save bookings.

## Project files
- index.html — public portfolio and interactive demo UI.
- profile-photo.jpg — user-provided profile portrait used on the homepage.
- logo.png — user-provided logo shown in the header and footer.
- Clients.csv, Sessions.csv, Services.csv, Certificates.csv, ProfessionalExperience.csv, Organizations.csv — fictional schema templates; the sample client/session rows are explicitly demo records.
- .env.example — blank placeholders only; no credentials.
- robots.txt and sitemap.xml — static placeholder SEO files. Replace the relative sitemap URL with the deployed canonical URL.

## Safety and scope
This is not a production booking system or secure dashboard. It has no server, database, authentication, server-side authorization, request persistence, real statistics, real availability, or Microsoft sync. The CSV buttons only import/export the demo client rows in volatile browser memory, and should only be used with the provided fictional format. No real client data should be entered, imported, stored, or uploaded. Admin is a front-end demo and is not private. All biography, qualifications, methods, specialties, experience, contacts, services, fees, languages, and public impact statistics still need Samy's review and approval. The interface contains no invented qualifications or client metrics.

## Local use and cost
Open index.html directly; no package install, build, account, or runtime cost is needed for this preview. It uses Google Fonts when online and falls back to system fonts if offline. Static hosting may offer a free tier, but no host, domain, or plan has been selected; check the provider's current storage, bandwidth, and commercial-use limits before relying on it. Custom domains generally have a recurring registrar cost. There is currently no ongoing service fee from this prototype.

## Recommended production architecture
A production implementation needs a server-rendered app/API, a supported database with migrations, and a maintained authentication provider or securely implemented passwordless/admin authentication. Authorize every private route and mutation server-side. Use a minimal data model with Clients (unique internal ID, pseudonym, optional nationality, first contact, status, necessary consent/retention metadata) and Sessions (unique session ID, client ID, service, date, format, duration, status, optional fee/payment status). Enforce foreign keys and unique IDs. Calculate distinct clients from Clients and sessions from Sessions. Keep booking requests separate and apply retention/deletion. Do not store clinical notes in this portfolio. Publish only aggregate values Samy has explicitly approved and screened for re-identification risk. Add rate limiting, CSRF/session protections, validation, safe errors, encrypted transport, backups, and restoration practice before use with real people.

## Excel / OneDrive status
Not connected; the environment has no tenant, account, workbook, app registration, or permissions. The provided CSVs are schema templates, not a live integration or two-way Excel sync. Microsoft Graph's Excel REST API documentation currently describes workbook access for OneDrive for Business and SharePoint; Consumer OneDrive workbook API support is not available. The documented Excel workbook endpoints use delegated Files.Read/Files.ReadWrite permissions for supported workbook operations and require an OAuth bearer token. App registration, consent, tenant/account eligibility, permissions, and the exact workbook location must be verified before choosing a secure server-side flow. Never put a client secret or token in this static site's code. See [Microsoft's Excel Graph API overview](https://learn.microsoft.com/en-us/graph/api/resources/excel?view=graph-rest-1.0) and [worksheet permissions](https://learn.microsoft.com/en-us/graph/api/workbook-list-worksheets?view=graph-rest-1.0).

For production, define and validate structured tables named Clients, Sessions, Services, Certificates, ProfessionalExperience, and Organizations. Use stable IDs, idempotent upserts, duplicate detection, and sync logs that omit personal data. Save privately first; recalculate dashboard counts from records; publish only separately approved aggregate statistics. The current demo has none of these backend guarantees.

## Configuration and deployment
No production server can be started from this static-only project. .env.example contains placeholders for a future backend; populate them only after its integration code exists, keep the actual .env out of version control, and rotate credentials if exposed. Before launch, supply approved bilingual content, logo/profile assets, contact details, appointment handling policy, hosting and database choices, admin identity/authentication requirements, and Microsoft account type/workbook. Configure HTTPS, server-side auth/authorization, privacy notice/consent, retention/deletion, backup restoration, and tested booking notifications before accepting requests. No external accounts have been created and no deployment is claimed.

## Verification completed
Inspected the existing project: it contained only the earlier static index.html and README.md. Checked the updated HTML for the required full name, no old name, presence of English/Arabic translations for UI data keys, language preference storage, consent checkbox, CSV demo controls, and the setup/template files. These are content checks only; this is not a production build or security test. No application test suite or build tooling exists in the project.


## Appointment booking and Google Calendar
See GOOGLE_CALENDAR_SETUP.md for the required backend, OAuth, database, availability configuration, and safe event-creation flow. The current static website intentionally does not send or save requests and does not connect to Google Calendar.


## Booking update (2026-10-26)
The existing psychological support card now has an Arabic professional description, a visible 45–60 minute range, 45/60 minute selectors, and a responsive booking request panel with online/in-person choice, date picker, time selector, name, one contact method, and required privacy consent. The calendar date minimum uses Africa/Cairo.

The time selector has no options until a real backend supplies availability; no office hours were provided. Submission is intentionally blocked and states that nothing was sent/saved. There is no database or Calendar connection, so confirmed-event conflict checks and booking confirmations are not implemented. The WhatsApp click-to-chat is configured with the public number supplied by Samy in the PROFESSIONAL_WHATSAPP_NUMBER setting in index.html. After an actual discussion in WhatsApp, Samy confirms the fee and exact appointment manually. Do not accept real requests through this static page. See GOOGLE_CALENDAR_SETUP.md for the steps that unlock real booking.

Source checks run: verified required fields, both durations, date input, Cairo timezone, past-date guard, duration sync, no fabricated time slots, both-language UI keys, and unique element IDs. These static checks do not constitute a browser interaction test, backend integration test, or conflict test. The project still has no test runner or build system.


## Session duration clarification
Clients do not choose between 45 and 60 minutes. The service states that one session lasts 45–60 minutes; time beyond 60 minutes must be agreed in advance and is charged separately. No service or booking form has a client-selected duration; all session services display the same 45–60 minute range and note that time beyond 60 minutes is agreed and charged separately. The form asks for a preferred time, not a selectable live slot.


## WhatsApp request flow
The browser prepares a short WhatsApp message containing only name, requested service, preferred format/date/time, and the supplied contact detail. It does not include a mental-health history. WhatsApp opens with a draft; the visitor still reviews and sends it. The professional number is configured in international digits (country code, no plus sign or punctuation). This number is public-facing contact information, not a secret. No booking is confirmed by opening the draft.
