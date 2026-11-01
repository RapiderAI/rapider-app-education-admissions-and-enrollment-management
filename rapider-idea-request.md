<!-- Rapider Official App SOW & Specification | App #168: Education Admissions & Enrollment Management (education-admissions-and-enrollment-management) | Domain: EDU -->

# #168 Education Admissions & Enrollment Management (`education-admissions-and-enrollment-management`) — Scope of Work (SOW)

- **App Number & Name:** `#168` — Education Admissions & Enrollment Management
- **Proposed App Key:** `education-admissions-and-enrollment-management`
- **Suite / Domain Key & Model Prefix:** `EDU` (`Edu*`)
- **Representative Product (`P1`):** Slate by Technolutions
- **Combined Feature Catalog:** [../combined-features/168-education-admissions-and-enrollment-management-features.md](../combined-features/168-education-admissions-and-enrollment-management-features.md)
- **Target Release Posture:** Prospective Student Recruitment, Application Checklists, Holistic Multi-Reader Committee Review, Embargoed Decisions, Merit Aid, Enrollment Contracts & SIS Matriculation Microapplication

---

## 1. Executive Outcome & Target Audience

### 1.1 Business Problem Solved
Generic B2B sales CRMs model deals as linear `Lead -> Opportunity -> Quote` pipelines, failing completely on educational admissions where thousands of applicants submit multi-item document checklists, confidential FERPA-waived teacher recommendations, blind two-reader committee scores, embargoed simultaneous Decision Day releases, merit-scholarship net-tuition packages, e-signed K-12 re-enrollment contracts, and summer-melt onboarding milestones. **Rapider Education Admissions & Enrollment Management (`education-admissions-and-enrollment-management`)** delivers a purpose-built K-12, bootcamp, and Higher-Ed enrollment engine unifying recruitment (`CRM`/`MKT`), holistic reader evaluation, embargoed decisions, `FIN` tuition/deposit contracts, and zero-rekey matriculation into `#161 Student Information System (SIS)`.

### 1.2 Target Personas & Progressive Disclosure
- **SME Fast-Path Defaults (Independent K-12 Schools, Language/Vocational Academies, Bootcamps):** Publish an intake term application with automatic document checklists, schedule campus tours/shadow days, collect recommendations, review files on a `<rapider-kanban>` board, send e-signable tuition enrollment/re-enrollment contracts with deposit `FinInvoice`s, and promote enrolled students into `#161 SIS` in one click.
- **Enterprise Progressive Disclosure (Colleges, Universities, Selective Multi-Campus Districts):** Unlock territory-routed recruitment funnels (`CrmTerritory`), blind multi-reader *Slate Reader* bins (`FIRST_READ` -> `SECOND_READ` -> `COMMITTEE`) with conflict-of-interest locks, dual-control embargoed batch decision drops, `FinBudget`-governed scholarship/discount-rate modeling, conditional/I-20 visa clearance gates, and anti-summer-melt radars.

### 1.3 Measurable Business Outcomes
- **40% Higher Application Completion Rate:** Dynamic applicant portals and targeted missing-checklist nudges convert stalled incomplete applications before round deadlines.
- **Zero Accidental Early Decision Leaks & 100% FERPA Waiver Integrity:** Dual-control Home `WorkItem` release gates enforce decision embargoes, while waived recommendation letters are stripped at the API serializer layer.
- **Zero Manual SIS Re-Keying:** Deposited and cleared enrollees emit `edu.admissions.matriculated.v1` to provision `#161` `EduStudentProfile` and `EduGuardianLink` records idempotently.

### 1.4 Benchmark Summary (`P1`–`P6`)
Synthesizes the holistic *Slate Reader* bins, checklists, and embargoed decision releases of **`P1` Slate by Technolutions**, the K-12 shadow days and annual tuition re-enrollment contracts of **`P2` Finalsite Enrollment**, the net-tuition payment plan integration of **`P3` Blackbaud Enrollment**, the recruiter territories and conditional/visa workflows of **`P4` Ellucian CRM Recruit**, the Constituent 360 split-screen review and grounded AI briefs of **`P5` Salesforce Education Cloud**, and the program seat-quota to SIS conversion of **`P6` Workday Student Admissions**.

---

## 2. In-Scope, Out-of-Scope & Suite Ownership Boundaries

### 2.1 In-Scope Capabilities
1. Prospective student/family inquiry capture (`EduAdmissionsInquiry`), sibling/legacy detection, `CrmTerritory` counselor assignment, and campus tours/shadow days/interviews (`EduAdmissionsVisit`).
2. Multi-round applications (`EduApplication`), dynamic document checklists (`EduApplicationChecklistItem`), confidential FERPA-waived recommendation workflows (`EduRecommendationRequest`), and application fee/waiver handling.
3. Blind multi-reader rubric scoring, conflict-of-interest recusal, and sequential reader bins (`EduReaderEvaluation`).
4. Embargoed admissions decisions & merit scholarship/grant awards (`EduAdmissionDecision`) with dual-control release approvals and program seat-quota/aid-budget guards.
5. Digital tuition enrollment & annual K-12 re-enrollment contracts (`EduEnrollmentContract`), deposit collection (`FIN`), anti-summer-melt tracking, and idempotent `#161 SIS` matriculation.

### 2.2 Out-of-Scope Capabilities (Delegated to Adjacent Rapider Apps)
- **Post-matriculation course registration, daily attendance, gradebooks, GPAs, and academic transcripts:** Owned by `#161 Student Information System (SIS)` (`student-information-system-sis`).
- **Paid ad media buying, broadcast email/SMS delivery engines, and landing-page CMS:** Owned by `MKT` (`campaigns`, `email`, `sms`, `forms`, `events`) and `COM` (`website`).
- **Payment gateway card vaulting, recurring installment ledger collection, and general ledger accounting:** Owned by `FIN` (`billing`, `subscriptions`, `payments`, `acc`, `budgeting`).

### 2.3 Cross-Suite Ownership & Integration Contract

| Domain / App | Owns (Canonical Models) | Integration Contract with `education-admissions-and-enrollment-management` |
| :--- | :--- | :--- |
| **`education-admissions-and-enrollment-management` (`#168` — This App)** | `EduAdmissionsInquiry`, `EduAdmissionsVisit`, `EduApplication`, `EduApplicationChecklistItem`, `EduRecommendationRequest`, `EduReaderEvaluation`, `EduAdmissionDecision`, `EduEnrollmentContract` | Governs the prospective learner lifecycle from first inquiry through matriculation into `#161 SIS`. |
| **`#161 Student Information System` (`EDU`)** | `EduAcademicTerm`, `EduAcademicProgram`, `EduStudentProfile`, `EduGuardianLink` | `#168` targets `#161` intake terms & programs, checks active sibling records, runs K-12 returning-student re-enrollment contracts, and emits `edu.admissions.matriculated.v1` to create `EduStudentProfile` + `EduGuardianLink`. |
| **`CRM` Suite (`crm`)** | `CrmLead`, `CrmContact`, `CrmAccount`, `CrmTerritory` | Deduplicates prospective learners/guardians against `CrmLead`/`CrmContact` and routes counselor ownership using canonical `CrmTerritory`. |
| **`MKT` Suite (`forms`, `events`, `campaigns`, `email`, `sms`)** | `MktForm`, `MktEvent`, `MktCampaign`, `MktEmailMessage`, `MktSmsMessage` | `MktForm` captures RFI inquiries; `MktEvent` powers open-house registrations; `MKT` dispatches missing-checklist nudges and decision notifications. |
| **`FIN` Suite (`billing`, `subscriptions`, `payments`, `budgeting`)** | `FinInvoice`, `FinSubscription`, `FinPaymentIntent`, `FinBudget` | Application fees and enrollment deposits issue `FinInvoice`s; 10-month tuition contracts provision `FinSubscription`s; scholarship totals check `FinBudget` envelopes. |
| **`HR` Suite (`employees`)** | `HrEmployee` | Admissions counselors, faculty interviewers, committee readers, and staff-child priority checks reference canonical `HrEmployee.id`. |
| **Rapider Platform Services** | Identity/RBAC, Files/Drive, Home `WorkItem`, `projectChannelMessage` | Stores transcripts/essays/recommendations in Drive; routes fee waivers, over-cap scholarships & batch decision releases via Home `WorkItem`s. |

---

## 3. Primary Web Pages & Sidebar Navigation Architecture (13 Pages)

Every visible sidebar section strictly enforces the **Minimum 3 Items Rule (`>= 3` items with `displayOnMenu: true`)**: `Recruitment` (3 items), `Review & Decisions` (3 items), and `Enrollment & Governance` (3 items) = 9 visible items + 4 hidden detail/drawer routes (`displayOnMenu: false`).

| # | Route | Page Title | Sidebar Section | Menu Visible | Key Components & UX |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `admissions-pulse` | Admissions & Yield Pulse | `Recruitment` | `true` (Order 1) | KPI cards (`countSWR`): Active Inquiries, Complete Applications, Reader Queue Backlog, Admitted vs. Seat Target, Deposits Paid, Aid Discount Rate %. |
| 2 | `inquiries-prospects` | Inquiries & Territories | `Recruitment` | `true` (Order 2) | `EduAdmissionsInquiry` explorer (`findSWR`) with `#activeFilterTagsBar` (Term, Territory, Source Campaign, Sibling/Legacy), `<rapider-phone-input>`, clickable Prospect Name -> `application-reader-detail`, icon+text Edit, icon-only Delete. |
| 3 | `visits-interviews` | Tours, Shadow Days & Interviews | `Recruitment` | `true` (Order 3) | `EduAdmissionsVisit` schedule linked to `MktEvent`, host assignment, check-in status, and interviewer rubric submission. |
| 4 | `applications-board` | Applications & Checklists | `Review & Decisions` | `true` (Order 1) | `<rapider-kanban>` pipeline (`STARTED` -> `AWAITING_CHECKLIST` -> `COMPLETE_READY_FOR_REVIEW` -> `IN_COMMITTEE` -> `DECISION_STAGED` -> `MATRICULATED`) + table toggle and `#activeFilterTagsBar`. |
| 5 | `holistic-reader` | Reader Bins & Committee | `Review & Decisions` | `true` (Order 2) | `EduReaderEvaluation` bin queue (`FIRST_READ`, `SECOND_READ`, `COMMITTEE`, `DEAN_FINAL`) with blind-read locks, COI recusal button, and discrepancy flags. |
| 6 | `decisions-aid` | Decisions & Merit Scholarships | `Review & Decisions` | `true` (Order 3) | Embargoed `EduAdmissionDecision` & scholarship packaging workbench (`Decimal128`), program seat-cap gauges, `FinBudget` aid meter, and Release Batch `WorkItem` action. |
| 7 | `contracts-deposits` | Contracts, Deposits & Re-Enrollment | `Enrollment & Governance` | `true` (Order 1) | `EduEnrollmentContract` tracker (new deposits + K-12 annual re-enrollment waves), `FinInvoice`/`FinSubscription` status, and Promote to `#161 SIS` action. |
| 8 | `melt-onboarding` | Conditions, Visas & Melt Radar | `Enrollment & Governance` | `true` (Order 2) | Conditional offer clearance, international I-20/CAS milestones (`ADM-017`), and anti-summer-melt readiness checklist monitor (`ADM-020`). |
| 9 | `yield-analytics` | Funnel, Yield & Aid Simulator | `Enrollment & Governance` | `true` (Order 3) | Source-to-matriculation funnel conversion, historical yield curves, and `Decimal128` net-tuition / discount-rate scenario simulator (`ADM-024`). |
| 10 | `application-reader-detail` | Split-Screen Dossier & Reader | *(Hidden)* | `false` | Holistic split-screen view (`#/application-reader-detail?id=...`) showing Drive packet viewer, `EduApplicationChecklistItem` verification, waived `EduRecommendationRequest`s, blind `EduReaderEvaluation` rubric, AI Dossier Brief (`ADM-021`), and `Back to list`. |
| 11 | `contract-decision-detail` | Decision Letter & Contract View | *(Hidden)* | `false` | Detailed `EduAdmissionDecision` + `EduEnrollmentContract` audit view (`#/contract-decision-detail?id=...`) with net-tuition breakdown, e-signature seal, `FinInvoice` deposit status, and `#161` matriculation link. |
| 12 | `inquiry-visit-drawer` | Log Inquiry / Schedule Visit | *(Hidden)* | `false` | Sliding drawer to create/edit `EduAdmissionsInquiry` (`<rapider-phone-input>`) or book `EduAdmissionsVisit`, `finally` button reset, and `closePageDrawer()`. |
| 13 | `decision-contract-drawer` | Stage Decision / Issue Contract | *(Hidden)* | `false` | Sliding drawer to stage `EduAdmissionDecision` (`Decimal128` scholarship), request waiver/release `WorkItem`, or generate `EduEnrollmentContract` with `closePageDrawer()`. |

**Mandatory Rapider UI Standards Enforced Across All 13 Pages:**
- **SWR & Soft-Delete Hygiene:** Initial loads exclusively call `window.rapiderApi.findSWR` / `countSWR` with zero manual `isDeleted` filter clauses and filter `item.isDeleted !== true` in memory.
- **Table Actions & Navigation:** Zero standalone "View" buttons in `Actions`; primary identifiers navigate to `#/application-reader-detail?id=...` or `#/contract-decision-detail?id=...`; Edit uses icon + text; Delete uses icon-only with `title="Delete"` and `aria-label="Delete"`.
- **Contrast & Dialog Ban:** Primary and danger buttons enforce `#ffffff !important` white text; native `alert`/`confirm`/`prompt` are strictly banned.

---

## 4. Canonical Data Models (`Edu*` — 8 Models)

All models use platform-generated UUID `id` (`00000000-xxxx-xxxx-xxxx-xxxxxxxxxxxx` in sample seeds), omit `projectId`, enforce optimistic `version`, and store all application fees, rubric weights/scores, gross tuition, scholarships, and deposits as `Decimal128`.

| Model Name | Key Fields & Types | Relationships & External Refs | Invariants & Lifecycle |
| :--- | :--- | :--- | :--- |
| **`EduAdmissionsInquiry`** | `id` (UUID), `firstName`, `lastName`, `email` (string), `phoneE164` (string), `entryGradeOrLevel` (string), `priorityFlags` (string[]: `SIBLING`, `ALUMNI_LEGACY`, `STAFF_CHILD`), `stage` (`NEW_INQUIRY`, `NURTURING`, `VISITED`, `APPLICATION_STARTED`, `ARCHIVED`), `version` (int) | `targetTermId` -> `EduAcademicTerm.id`, `targetProgramId` -> `EduAcademicProgram.id`, `crmLeadId` -> `CrmLead.id`, `guardianContactId` -> `CrmContact.id`, `territoryId` -> `CrmTerritory.id`, `counselorEmployeeId` -> `HrEmployee.id`, `sourceCampaignId` -> `MktCampaign.id` | Deduplicates against `CrmLead`/`CrmContact` on normalized email + E.164 phone before creation. |
| **`EduAdmissionsVisit`** | `id` (UUID), `visitType` (`OPEN_HOUSE`, `CAMPUS_TOUR`, `SHADOW_DAY`, `ADMISSIONS_INTERVIEW`), `startAt` (Date), `endAt` (Date), `attendanceStatus` (`REGISTERED`, `CHECKED_IN`, `NO_SHOW`, `CANCELLED`), `interviewRating` (`Decimal128`), `interviewerNote` (string), `version` (int) | `inquiryId` -> `EduAdmissionsInquiry.id`, `applicationId` -> `EduApplication.id` (optional), `mktEventId` -> `MktEvent.id` (optional), `hostEmployeeId` -> `HrEmployee.id` | `interviewerNote` and `interviewRating` are restricted to admissions staff/readers and never exposed to applicants. |
| **`EduApplication`** | `id` (UUID), `applicationNumber` (string, unique), `roundType` (`EARLY_DECISION`, `EARLY_ACTION`, `REGULAR_DECISION`, `ROLLING`, `TRANSFER`, `K12_STANDARD`), `applicationFeeAmount` (`Decimal128`), `feeStatus` (`UNPAID`, `PAID`, `WAIVED`), `stage` (`STARTED`, `AWAITING_CHECKLIST`, `COMPLETE_READY_FOR_REVIEW`, `IN_COMMITTEE`, `DECISION_STAGED`, `DECISION_RELEASED`, `MATRICULATED`, `WITHDRAWN`), `currentReaderBin` (`NONE`, `FIRST_READ`, `SECOND_READ`, `COMMITTEE`, `DEAN_FINAL`), `requiresStudentVisa` (boolean), `submittedAt` (Date), `matriculatedStudentId` (UUID), `version` (int) | `inquiryId` -> `EduAdmissionsInquiry.id`, `targetTermId` -> `EduAcademicTerm.id`, `targetProgramId` -> `EduAcademicProgram.id`, `feeInvoiceId` -> `FinInvoice.id` (optional) | Cannot enter `COMPLETE_READY_FOR_REVIEW` until `feeStatus` is `PAID` or `WAIVED` AND all required pre-decision `EduApplicationChecklistItem`s are `VERIFIED` or `WAIVED`. |
| **`EduApplicationChecklistItem`** | `id` (UUID), `itemCode` (string), `label` (string), `phase` (`PRE_DECISION`, `POST_OFFER_CONDITION`, `PRE_MATRICULATION_MELT`), `isRequired` (boolean), `driveFileId` (string), `status` (`MISSING`, `UPLOADED_PENDING_VERIFY`, `VERIFIED`, `REJECTED_REUPLOAD`, `WAIVED`), `verifiedAt` (Date), `version` (int) | `applicationId` -> `EduApplication.id`, `verifiedByEmployeeId` -> `HrEmployee.id` | Completing the final required `PRE_DECISION` item triggers automatic transition of `EduApplication` to `COMPLETE_READY_FOR_REVIEW` and `FIRST_READ`. |
| **`EduRecommendationRequest`** | `id` (UUID), `recommenderName` (string), `recommenderEmail` (string), `recommenderRole` (`TEACHER`, `COUNSELOR`, `EMPLOYER`), `waivedRightToView` (boolean), `driveFileId` (string), `ratingSummaryJson` (JSON), `status` (`REQUESTED`, `SUBMITTED`, `VERIFIED`), `submittedAt` (Date), `version` (int) | `applicationId` -> `EduApplication.id` | Hard FERPA invariant: when `waivedRightToView = true`, API serializers strip `driveFileId` and `ratingSummaryJson` from all applicant/guardian queries permanently. |
| **`EduReaderEvaluation`** | `id` (UUID), `readerSlot` (`FIRST_READER`, `SECOND_READER`, `COMMITTEE_CHAIR`), `conflictOfInterestRecused` (boolean), `academicScore` (`Decimal128`), `extracurricularScore` (`Decimal128`), `personalFitScore` (`Decimal128`), `compositeReaderScore` (`Decimal128`), `readerRecommendation` (`STRONG_ADMIT`, `ADMIT`, `WAITLIST`, `DENY`), `confidentialReaderNote` (string), `submittedAt` (Date), `version` (int) | `applicationId` -> `EduApplication.id`, `readerEmployeeId` -> `HrEmployee.id` | `SECOND_READER` cannot read `FIRST_READER` fields prior to submitting own evaluation; setting `conflictOfInterestRecused = true` revokes file access for `readerEmployeeId`. |
| **`EduAdmissionDecision`** | `id` (UUID), `decisionOutcome` (`ADMIT_UNCONDITIONAL`, `ADMIT_CONDITIONAL`, `WAITLIST`, `DEFER`, `DENY`), `conditionsSummary` (string), `conditionsCleared` (boolean), `waitlistRank` (int), `grossTuitionAmount` (`Decimal128`), `meritScholarshipAmount` (`Decimal128`), `needGrantAmount` (`Decimal128`), `netTuitionAmount` (`Decimal128`), `currency` (string), `embargoStatus` (`STAGED_EMBARGOED`, `APPROVED_SCHEDULED`, `RELEASED_TO_APPLICANT`), `portalReleaseAt` (Date), `replyDeadlineAt` (Date), `version` (int) | `applicationId` -> `EduApplication.id`, `aidBudgetId` -> `FinBudget.id` (optional), `approvedByEmployeeId` -> `HrEmployee.id` | Invariant: `netTuitionAmount == grossTuitionAmount - meritScholarshipAmount - needGrantAmount >= 0.00`; strictly invisible to applicants until `embargoStatus = RELEASED_TO_APPLICANT` AND `now >= portalReleaseAt`. |
| **`EduEnrollmentContract`** | `id` (UUID), `contractType` (`NEW_ENROLLMENT`, `ANNUAL_RE_ENROLLMENT`), `paymentPlanChoice` (`ANNUAL_FULL`, `SEMI_ANNUAL`, `TEN_MONTH_INSTALLMENT`), `netContractAmount` (`Decimal128`), `requiredDepositAmount` (`Decimal128`), `currency` (string), `signedGuardianOrStudentName` (string), `signedAt` (Date), `depositStatus` (`UNPAID`, `PAID`, `WAIVED`), `status` (`ISSUED`, `SIGNED_AWAITING_DEPOSIT`, `ACTIVE_EXECUTED`, `DECLINED_EXPIRED`), `version` (int) | `applicationId` -> `EduApplication.id` (nullable for K-12 re-enrollment), `returningStudentId` -> `EduStudentProfile.id` (for re-enrollment), `billingContactId` -> `CrmContact.id`, `depositInvoiceId` -> `FinInvoice.id`, `tuitionSubscriptionId` -> `FinSubscription.id` | Signed contracts (`ACTIVE_EXECUTED`) lock financial and signature fields immutably and trigger `#161 SIS` matriculation once any `ADMIT_CONDITIONAL` conditions clear. |

---

## 5. Core End-to-End User Journeys

### 5.1 Journey 1: SME Independent School Fast-Path — Tour, Checklist, Contract & `#161 SIS` Push
1. Prospective parent submits an `MktForm` inquiry (`EduAdmissionsInquiry`), auto-flagged `SIBLING` from an active `#161` brother, and books a `SHADOW_DAY` on `visits-interviews`.
2. Family completes `EduApplication`, pays the `\$75.00` fee (`FinInvoice`), and triggers two `EduRecommendationRequest`s (`waivedRightToView = true`). Once transcripts and teacher recs arrive, `#168` auto-moves the card to `COMPLETE_READY_FOR_REVIEW`.
3. Admissions Director stages `ADMIT_UNCONDITIONAL` with a `\$3,000.00` sibling/merit award (`netTuitionAmount = \$21,000.00`), releases the offer, and issues an `EduEnrollmentContract` (`TEN_MONTH_INSTALLMENT` + `\$1,500.00` deposit).
4. Parent e-signs and pays the `\$1,500.00` deposit `FinInvoice`; `#168` provisions the 10-month `FinSubscription` and emits `edu.admissions.matriculated.v1`, creating `EduStudentProfile` + `EduGuardianLink` in `#161 SIS`.

### 5.2 Journey 2: University Blind Multi-Reader Bins, COI Recusal & Committee Escalation
1. Reader 1 opens `#/application-reader-detail?id=...` in `FIRST_READ`, reviews the grounded AI Dossier Brief (`ADM-021`) with transcript citations, and submits `ADMIT` (`compositeReaderScore = 88.50`).
2.Assigned Reader 2 recognizes the applicant as a neighbor, clicks **Declare Conflict of Interest** (`conflictOfInterestRecused = true`), and `#168` immediately locks Reader 2 out and reassigns Reader 3.
3. Blinded Reader 3 submits `DENY` (`compositeReaderScore = 64.00`); `#168` detects the `ADMIT` vs. `DENY` split and automatically routes the file into the `COMMITTEE` bin.

### 5.3 Journey 3: Embargoed Decision Day Batch Release via Dual-Control Home `WorkItem`
1. 1,400 Regular Decision outcomes and `Decimal128` merit scholarships (validated against `FinBudget`) sit in `STAGED_EMBARGOED` scheduled for `March 25, 5:00 PM EDT` (`portalReleaseAt`).
2. Prior to sign-off, applicant portal APIs return zero decision or scholarship fields. Dean of Admissions approves the batch release Rapider Home `WorkItem`, arming `APPROVED_SCHEDULED` for exact simultaneous release at 5:00 PM.

### 5.4 Journey 4: Conditional Offer, Visa Milestone & Anti-Summer-Melt Intervention
1. An international admit accepts `ADMIT_CONDITIONAL` (requiring final transcript GPA `>= 3.00` and financial affidavit for I-20).
2. `melt-onboarding` highlights the student missing immunization upload 35 days before orientation; Counselor sends a grounded AI Missing-Checklist Nudge (`ADM-022`), verifies the final documents (`conditionsCleared = true`), and completes `#161 SIS` matriculation.

### 5.5 Journey 5: K-12 Annual Returning-Student Re-Enrollment Wave
1. Every February, Enrollment Manager generates `ANNUAL_RE_ENROLLMENT` `EduEnrollmentContract`s for 480 returning `#161` `EduStudentProfile` households, tracking real-time returning seat retention alongside incoming new-admit seat targets.

### 5.6 Journey 6: Click-Through Navigation & `#activeFilterTagsBar` State Restoration
1. Counselor filters `applications-board` by `Round: "EARLY_ACTION"` and `Bin: "COMMITTEE"`, rendering `#activeFilterTagsBar` chips.
2. Clicking **APP-2026-04182 ( Maya Lin )** transitions cleanly to `#/application-reader-detail?id=...` without `<base href>` 404 diversion, renders the split-screen packet, and **Back to list** restores the exact filtered view.

---

## 6. Consolidated Feature Priorities & Work Packages

### `P0` Foundation Work Packages (Must-Have Core Release)
- **WP-P0-1 — Inquiry Capture, Territories & Campus Visits (`ADM-001`, `ADM-002`):** Deliver `EduAdmissionsInquiry` (`CRM`/`MKT` dedupe, `<rapider-phone-input>`, `CrmTerritory`) and `EduAdmissionsVisit` tours/interviews.
- **WP-P0-2 — Applications, Dynamic Checklists, Waived Recs & App Fees (`ADM-005`, `ADM-006`, `ADM-007`, `ADM-008`):** Build `<rapider-kanban>` `applications-board`, `EduApplicationChecklistItem` auto-progression, FERPA-waived `EduRecommendationRequest` isolation, and `FinInvoice` fee/waiver `WorkItem`s.
- **WP-P0-3 — Blind Holistic Reader Bins & Embargoed Decisions/Aid (`ADM-010`, `ADM-011`, `ADM-014`, `ADM-015`):** Deliver split-screen `application-reader-detail`, blind co-reader independence, dual-control `EduAdmissionDecision` embargoes, and `Decimal128` net-tuition scholarship packaging.
- **WP-P0-4 — Enrollment Contracts, Deposits & `#161 SIS` Matriculation (`ADM-016`, `ADM-018`):** Deliver e-signed `EduEnrollmentContract` (new + K-12 re-enrollment), `FIN` deposit/subscription handoffs, and idempotent `#161 SIS` promotion.

### `P1` Enterprise Scale Work Packages
- **WP-P1-1 — Priority Flags, Batch Imports, COI Recusal & Seat/Budget Shaping (`ADM-003`, `ADM-004`, `ADM-009`, `ADM-012`, `ADM-013`):** Add sibling/legacy/staff detection, source funnel analytics, external batch imports, COI recusal locks, and `#161` seat-cap / `FinBudget` monitors.
- **WP-P1-2 — Conditional/Visa Clearance, Waitlist Waves & Anti-Melt Radar (`ADM-017`, `ADM-019`, `ADM-020`):** Add conditional transcript/I-20 gates, rank-ordered 72-hour waitlist waves, and pre-term summer-melt readiness tracking.

### `P2` Adjacent & Grounded AI Work Packages
- **WP-P2-1 — Grounded AI Reader Briefs, Checklist Nudges, NL Queries & Yield Simulator (`ADM-021`, `ADM-022`, `ADM-023`, `ADM-024`):** Deliver non-scoring cited dossier summaries in `projectChannelMessage`, personalized missing-item nudges, natural-language `#activeFilterTagsBar` query translation, and `Decimal128` yield/discount-rate simulation.

---

## 7. Roles, Permissions & Field-Level Governance

| Role | Permitted Actions | Restricted / Field-Level Boundaries |
| :--- | :--- | :--- |
| **Applicant / Prospective Guardian** | Submit `EduApplication`, upload `EduApplicationChecklistItem` files, book `EduAdmissionsVisit`s, view `RELEASED_TO_APPLICANT` decisions & aid letters, e-sign `EduEnrollmentContract`, and pay `FIN` fees/deposits. | Zero access to `STAGED_EMBARGOED` / `APPROVED_SCHEDULED` decisions, `EduReaderEvaluation` scores/notes, `interviewerNote`s, or `waivedRightToView = true` recommendations. |
| **External Recommender** | Upload confidential recommendation via single-use scoped token for a specific `EduRecommendationRequest`. | Zero access to any other applicant field or portal route. |
| **Admissions Counselor / Reader (`HrEmployee`)** | Manage assigned `CrmTerritory` inquiries/visits, verify checklist items, score assigned `EduReaderEvaluation` bins, and draft staged decisions. | Blinded from co-reader scores before submitting own read; immediately locked out on `conflictOfInterestRecused = true`; cannot unilaterally lift batch decision embargoes. |
| **Financial Aid / Enrollment Officer** | Package `meritScholarshipAmount` / `needGrantAmount` within `FinBudget` thresholds, manage `EduEnrollmentContract` payment plans, and review fee-waiver `WorkItem`s. | Over-cap scholarship awards require Dean/Director Home `WorkItem` approval. |
| **Dean / Director of Admissions** | Configure rounds, seat quotas, and rubrics; chair `COMMITTEE` bin; approve batch decision release and over-cap aid Home `WorkItem`s; trigger waitlist waves. | Cannot alter signed `ACTIVE_EXECUTED` `EduEnrollmentContract` signatures or expose FERPA-waived letters to applicants. |

---

## 8. Technical APIs, Guarded Commands, Events & `requiredWorkflows`

### 8.1 Guarded Domain Commands
Every state-mutating API enforces `idempotencyKey`, `correlationId`, and `expectedVersion`:
- `edu.admissions.verifyChecklistItem` — Marks item `VERIFIED` and atomically advances `EduApplication` to `COMPLETE_READY_FOR_REVIEW` + `FIRST_READ` when all required `PRE_DECISION` items + fee clear.
- `edu.admissions.submitReaderEvaluation` — Enforces COI non-recusal, records `Decimal128` rubric scores, and routes to `SECOND_READ` or `COMMITTEE` on reader divergence.
- `edu.admissions.approveDecisionBatchRelease` — Dual-control command (`WorkItem` backed) transitioning `STAGED_EMBARGOED` decisions to `APPROVED_SCHEDULED` for `portalReleaseAt`.
- `edu.admissions.executeEnrollmentContract` — Seals digital signature, creates deposit `FinInvoice` + installment `FinSubscription` in `FIN`, and marks `SIGNED_AWAITING_DEPOSIT`.
- `edu.admissions.matriculateToSis` — Verifies `ACTIVE_EXECUTED` contract + `depositStatus` (`PAID`/`WAIVED`) + `conditionsCleared`, then emits `edu.admissions.matriculated.v1` idempotently.

### 8.2 Domain Events Published & Consumed (Kafka)
- **Published:** `edu.admissions.inquiryCaptured.v1`, `edu.admissions.applicationCompleted.v1`, `edu.admissions.decisionsReleased.v1`, `edu.admissions.contractSigned.v1`, `edu.admissions.matriculated.v1`.
- **Consumed:** `mkt.form.submitted.v1` & `mkt.event.attended.v1` (from `MKT`), `fin.invoice.settled.v1` (marks application fee or enrollment deposit `PAID` and triggers matriculation check).

### 8.3 `requiredWorkflows` (Declared in `app.manifest.json`)
1. `applicationChecklistCompletionAndBinRoutingWorkflow` — Evaluates dynamic checklist completeness, blind reader bin progression, and discrepancy escalation.
2. `embargoedDecisionReleaseWorkflow` — Releases `APPROVED_SCHEDULED` decisions precisely at `portalReleaseAt` and dispatches `MKT` portal notifications.
3. `enrollmentContractDepositAndSisMatriculationWorkflow` — Orchestrates `FIN` deposit/subscription creation and emits `edu.admissions.matriculated.v1` to `#161 SIS` once conditions clear.
4. `missingChecklistAndSummerMeltNudgeWorkflow` — Identifies incomplete applicants and at-risk deposited students ahead of deadlines for counselor outreach.

### 8.4 Grounded Rapider AI Rules
- **Strict EU AI Act High-Risk Education Safeguard:** AI Reader Dossier Briefs (`ADM-021`) are strictly factual, citation-linked document summaries—AI is **PROHIBITED** from generating admission scores, predicting applicant "fit," or recommending `ADMIT`/`DENY` outcomes.
- AI Checklist Nudges (`ADM-022`) and NL Query Builders (`ADM-023`) MUST ground every statement in retrieved `EduApplicationChecklistItem` and `EduAdmissionsInquiry` records and require human confirmation before sending external communications.

---

## 9. Security, Privacy, Compliance & Non-Functional Requirements

- **FERPA Waiver Confidentiality, COPPA & EU AI Act Compliance:** Waived recommendations (`waivedRightToView = true`), internal `EduReaderEvaluation` notes, and `interviewerNote`s are isolated server-side from applicant/guardian tokens. High-stakes admission evaluations remain 100% human-scored in compliance with EU AI Act Annex III education provisions.
- **Data Retention & Right to Erasure:** Non-matriculated denied/withdrawn applicant dossiers follow configurable institutional retention policies (e.g., 1–3 years) before automated PII archival/purge, while matriculated records hand off cleanly to `#161 SIS`.
- **Exact `Decimal128` Precision:** Application fees (e.g., `\$75.00`), gross tuition (`\$42,500.00`), merit scholarships (`\$15,000.00`), net contract amounts (`\$27,500.00`), deposits (`\$500.00`), and weighted reader rubrics strictly use `Decimal128`.
- **Accessibility & Responsive Applicant/Reader UX:** Full WCAG 2.2 AA compliance (accessible applicant checklists, keyboard-driven split-screen reader, `#ffffff !important` contrast on primary/danger buttons across light and dark modes) across `390px`, `768px`, and `1440px`.

---

## 10. Deterministic Acceptance Criteria

1. **Sidebar 3-Item Section Rule:** `app.manifest.json` defines 3 visible sidebar sections (`Recruitment`, `Review & Decisions`, `Enrollment & Governance`), each containing 3 visible items (`displayOnMenu: true`), while all 4 detail/drawer routes set `displayOnMenu: false`.
2. **SWR & Soft-Delete Query Hygiene:** Initial loads across all pages invoke `findSWR` / `countSWR` with zero manual `isDeleted` filter clauses and filter `item.isDeleted !== true` in memory.
3. **Search, `#activeFilterTagsBar` & Clear All:** Filtering `inquiries-prospects`, `applications-board`, `holistic-reader`, or `contracts-deposits` displays HTML-escaped chips in `#activeFilterTagsBar` with `[Clear all]`, restoring the full dataset in one click.
4. **Table Action Standard:** Zero standalone "View" buttons appear in `Actions`; primary identifiers navigate to `#/application-reader-detail?id=...` or `#/contract-decision-detail?id=...`; Edit uses icon + text and Delete uses icon-only with `title="Delete"` and `aria-label="Delete"`.
5. **Custom Elements Adoption:** Prospect/guardian phone fields in `inquiries-prospects` and `inquiry-visit-drawer` use `<rapider-phone-input>`, and `applications-board` uses `<rapider-kanban>`.
6. **Optimistic Lifecycle & Drawer Auto-Close:** Saving `inquiry-visit-drawer` or `decision-contract-drawer` resets button state in a `finally` block, calls `closePageDrawer()`, clears SWR cache, broadcasts events, and refreshes parent views; deletions confirm via `#rapiderConfirmOkBtn` with zero native `alert`/`confirm`/`prompt`.
7. **Embargo & FERPA Recommendation Hard Gates:** Applicant APIs return zero `EduAdmissionDecision` fields while `embargoStatus != RELEASED_TO_APPLICANT` (or `now < portalReleaseAt`) and zero `driveFileId`/content for `EduRecommendationRequest` rows with `waivedRightToView = true`.
8. **Blind Co-Reader & COI Recusal Determinism:** `SECOND_READER` cannot read `FIRST_READER` scores prior to submitting own evaluation; split `ADMIT`/`DENY` reads auto-route to `COMMITTEE`; `conflictOfInterestRecused = true` immediately revokes file access for that reader.
9. **Exact `Decimal128` Net-Tuition & `FIN` Contract Integrity:** Saving an `EduAdmissionDecision` enforces `netTuitionAmount == grossTuitionAmount - meritScholarshipAmount - needGrantAmount >= 0.00` (`Decimal128`), and executing an `EduEnrollmentContract` creates a canonical `FinInvoice` deposit without shadow GL tables.
10. **Idempotent `#161 SIS` Matriculation:** Settling the contract deposit and clearing offer conditions emits `edu.admissions.matriculated.v1` and stamps `matriculatedStudentId` once without creating duplicate `#161` students on retry.
11. **Click-Through Navigation & Theme Compliance:** Clicking an application in `applications-board` navigates cleanly to `#/application-reader-detail?id=...` without `<base href>` 404 diversion, `Back to list` restores filters, all pages pass `validate_theme` in dark/light modes with `#ffffff !important` primary/danger buttons, and zero schemas contain `projectId`.
