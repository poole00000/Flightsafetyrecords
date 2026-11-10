# Reliant Air Charter — Qualification Records Builder

GitHub Pages-ready, browser-side bulk PDF preparation tool designed around **Reliant Air Charter Electronic Manual and Recordkeeping System Manual, Original 21-Apr-2025**. This is a preparation/export tool, **not the approved EMRS**, and does not integrate with JetInsight.

## Deploy with GitHub

1. Create a new repository (public for GitHub Pages on plans that require it; no private records in the repository).
2. Upload `index.html`, `app.js`, and `style.css` to the repository root.
3. Under **Settings → Pages**, choose **Deploy from a branch**, select `main` and `/ (root)`.
4. Open the Pages link. Imported PDFs stay in the browser's current session until the user downloads an export or project file. The site loads `pdf-lib` from a public CDN; the browser requests code, **not uploaded PDF files**, from that CDN. Internal review of any third-party dependencies remains necessary.

**NEVER commit pilot qualification PDFs, signed records, exported master PDFs, saved project JSON, or records containing personal data to GitHub.** Saved project JSON includes PDF bytes in Base64; handle as sensitive data.

## Workflow

1. Drop many source PDF documents into the browser.
2. Assign each record to a person and the **exact EMRS Appendix A.1.1 category**. For a 14- or 26-month record, enter its event date and verify the retention trigger. For a 'retain for current aircraft' record, mark release only if this was verified and enter the date the retention obligation ended. Permanent records are never eligible for exclusion. Records with unknown category or missing data block export. Legal/administrative hold blocks omission.
3. Check every record and confirm the export selection.
4. Generate a navigable master PDF. The export includes cover, linked record index, document dividers, and imported pages. When selected, records that are **more than an additional calendar year beyond their required retention period** are excluded **from this newly generated PDF only**.
5. Review the PDF visually and verify that all necessary record pages and signatures are present. Back up each original to **ReliantNAS → data backup**, as required by EMRS §3.1.0, **before** any upload to JetInsight. Have the Director of Operations or designee verify records (EMRS §2.4.1.E). Maintain JetInsight cloud copies, restricted access, and archives per the manual.
6. Download a project JSON to resume later; keep it in an authorized secure location, not in GitHub. Old projects do not automatically update with copies from JetInsight.

## Retention rules implemented (EMRS Appendix A.1.1, pages A-1 / A-2)

| Type | Manual minimum retention |
| --- | --- |
| Flight Instructor Initial Ground and Flight Training | Permanent |
| Flight Instructor Transition Ground and Flight Training | Retain for current aircraft |
| Flight Instructor (Simulator) Line Observation Program | 14 calendar-months |
| Flight Instructor Observation | 26 calendar-months |
| Check Pilot Initial Ground and Flight Training | Permanent |
| Check Pilot Transition Ground and Flight Training | Retain for current aircraft |
| Check Pilot (Simulator) Line Observation Program | 14 calendar-months |
| Check Pilot Observation | 26 calendar-months |
| Check Pilot Authorization | Retain for current aircraft |

For time-limited records the tool **assumes the event date is the retention-period trigger**. The manual does not fully specify every trigger, so the operator must verify that assumption against the governing training / qualification records and applicable regulations. 'Retain for current aircraft' is **not** a fixed retention period and must not be automatically interpreted as the expiry of an FAA authorization or qualification. An explicit determination and date is required before the additional one-year buffer can begin.

**Exclusion is not deletion.** The website does not, and cannot, delete previously generated PDFs, backups, copies in JetInsight, source files, git history, or files on a user's disk. FAA/NTSB preservation obligations, legal holds, longer retention requirements, and verified company procedures take precedence. No automatic destruction or retention override is implemented.

## Material limitations / approval gates

- **EMRS §1.3.0**: Any intended change to the EMRS, including addition of software or record procedures, is to be proposed to the FAA for review and acceptance **before implementation**. The operator should confirm whether using this export method as official recordkeeping requires acceptance.
- **EMRS §2.2.1.1** designates **JetInsight** as the recordkeeping software; this site does not replace it or provide approved permissions, signatures, access logs, or backups.
- **EMRS §2.1.1 and §2.4.1** require adequate detail, legibility, record continuity, and verification. Each original record must remain independently retrievable; a single large PDF might not be appropriate for all record types or JetInsight workflows.
- **Digitally signed PDFs:** pdf-lib assembles pages into a **new PDF**. Original PDF digital certificate signatures will **not remain cryptographically valid on the merged copy**. Keep every signed original intact and available in JetInsight / ReliantNAS as required. Do not treat the merged file as a replacement for the certified originals. This is especially relevant under EMRS §2.5.0–2.5.1.
- **EMRS §3.1.0** requires a copy of **each document** in the `data backup` folder on `reliantnas` **before upload** to JetInsight. One exported PDF alone is not an adequate substitute for those individual backups without an accepted procedure change.
- No automated identity/access management, authentication, audit trail, server-side record storage, or scheduled cleanup. Browser PDF merging can be resource-intensive for very large files. Test PDF hyperlinks and page appearance in the intended viewer.
- This tool was syntax-checked only; **browser end-to-end tests, security assessment, FAA acceptance, JetInsight upload validation, and cryptographic-signature compatibility have not been completed**.

