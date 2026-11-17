# Academy Quran

Everything of the Quran from the Academy LMS platform, taken out into its own repository: the Laravel module
(hifz map and daily review, the shared mushaf in a lesson and the mistakes notebook, the recitation check, programs
and plans, lessons' portions and results, exams and certificates, settings, the platform's copy of the text), its
tests, the portal's Quran screens, the app's Quran features, its docs, and its slice of the OpenAPI spec.

It is a **copy**, not a rewrite. Every file is exactly as it was in the platform repository at commit
**`84aca260`** ("Branding: take a browser icon up to 2 MB, shrunk to 256 px before it is sent"). Nothing was edited,
so nothing is lost. **It does not run on its own yet**: the code still calls the platform's contracts
(`Modules\SharedKernel\…`, `Modules\Learning\Contracts\…` and others) and the portal and app files still import the
platform's shared code. The sections below list every one of those dependencies.

The platform's database tables for the Quran were **not** dropped. They are still in the platform's database
(see [Tables it owns](#tables-it-owns)).

---

## Layout

Paths mirror the platform repository, so a file can go back to exactly where it came from.

| Path | What it is |
|---|---|
| `apps/api/modules/Quran/` | The whole Laravel module: `src/` (Actions, Domain, Queries, Filament screens, HTTP controllers and presenters, jobs, listeners, live signals, models, bridges to Learning and Classroom, privacy, setup step, text), `database/migrations`, `database/seeders`, `routes/api.php`, `routes/web.php`, `lang/ar`, `lang/en`, `config/quran.php`, `resources/views`, `resources/quran` (fallback text folder) |
| `apps/api/modules/Platform/…` | Quran code that lived in the Platform module's folder: the console's Quran page (`QuranConsole` and its view), the data migration that gives every plan the `quran` feature, `DemoQuranAreaSeeder` |
| `apps/api/public/fonts/quran/` | Amiri Quran font (OFL) for the panels |
| `apps/api/tests/` | Tests whose subject is the Quran: `Feature/Quran/*`, `Unit/Quran/*`, `Feature/Demo/DemoQuranTest.php`, `Feature/Platform/SpeechRecitationTest.php`, `Support/QuranLessons.php`, `Support/QuranProgram.php`, `Fixtures/quran/*` (Tanzil sample files) |
| `apps/web/` | The portal's Quran routes (`/family/quran`, `/family/hifz`, `/teach/lessons/{id}/quran`, `/teach/students/{enrollment}/quran`, `/teach/exams`, the public `/{locale}/certificates/{code}`), components (`quran/`, `mushaf/`, `hifz/`, `recited-words.tsx`, `teach/hifz-forms.tsx`, `teach/recitation-*.tsx`, `site/certificate.*`), libs (`lib/quran`, `lib/mushaf`, `lib/hifz`, `lib/teach/recitation*`), the Amiri Quran font, `e2e/quran.spec.ts` |
| `apps/web/messages/{en,ar}.quran.json` | The portal's Quran wording, extracted from `messages/{en,ar}.json` (namespaces `quran`, `hifz`, `mushaf`, `recited`, `certificate`, plus Quran keys inside `nav`, `teach` and others) |
| `apps/mobile/` | The app's `features/quran`, `features/mushaf`, `features/hifz`, the recitation pieces of homework and teaching, the journey's hifz card, the Amiri Quran font, tests and fixtures |
| `apps/mobile/tool/strings.quran.py`, `apps/mobile/lib/core/l10n/arb/app_{ar,en}.quran.arb` | The app's wording used by those features, extracted from `tool/strings.py` and the arb files (includes a few shared keys such as `retry` that the Quran screens also use) |
| `docs/architecture/02-domain-rules.quran.md` | Section 26 ("القرآن") of the platform's domain rules, whole and unchanged, plus every other line of that doc that mentions the Quran |
| `docs/architecture/other-docs.quran.md` | Every line about the Quran in the platform's other docs (03, 04, READMEs, runbooks, acceptance) |
| `docs/CLAUDE.quran.md` | The platform `CLAUDE.md`'s Quran rules (lines 80–87, unchanged) and the Quran sentences of its other bullets |
| `openapi-quran.json` | The 22 Quran paths of the platform's OpenAPI spec with the schemas they reference |
| `integration-points/` | Whole copies of the platform files that wire the Quran in, at their platform paths, with `integration-points/INDEX.md` listing the Quran lines of each |

---

## Integration points it needs from the platform

The module "sits on top": nothing in the platform depends on it, and it reaches the platform only through these.
Copies of every file named here are under `integration-points/`.

### Contracts the platform defines and the Quran binds (do-nothing defaults stay in the platform)

| Contract | Default in the platform | Quran's binding | What it carries |
|---|---|---|---|
| `Learning\Contracts\LearningQuran` | `NoLearningQuran` | `Bridges\QuranLearning` | `homework.expected` (what to recite), each recording's check for the teacher, the report form's Quran fields, the way from `StudentProgress` to the hifz map |
| `Learning\Contracts\JourneyQuran` | `NoJourneyQuran` | `Bridges\QuranJourney` | `hifz: {due, done_today, daily}` on `GET learning/journey/map` |
| `SharedKernel\Quran\LessonQuran` | `NoLessonQuran` | `Bridges\QuranLessons` | The mushaf panel beside the room on the class page (`classPanel`) |
| `SharedKernel\Text\QuranSource` | `NoQuranSource` | `Texts\QuranFiles` | The console's copy of the text (fetch, status) |
| `SharedKernel\Ai\RecitationEngine` | `SpeechRecitation` (speech to text + `Text\WordAlignment`) | — (uses it) | The recitation check of homework and of the daily review |

Bindings: `LearningServiceProvider` (`bindIf` for the two Learning contracts), `SharedKernelServiceProvider`
(`bindIf`/`singletonIf` for `LessonQuran` and `QuranSource`), `QuranServiceProvider::register` (the real ones).

### Platform services and contracts it calls

- **Tenancy** — `SharedKernel\Tenancy\TenantContext`, `BelongsToTenant`, `Database\TenantTable` (every Quran table is tenant-scoped with row level security).
- **Plans** — `SharedKernel\Plans\AcademyPlan::has(Feature::Quran)` through `Support\QuranArea`; the `plan.feature:quran` route middleware; the `"quran"` entry in Platform's `saas_plans.features` (data migration `add_quran_to_plans` copied under `apps/api/modules/Platform/…`); the academy's modules list (`apps/web/src/lib/modules.ts` area `quran`, `apps/mobile/lib/core/auth/modules.dart` `Feature.quran`).
- **Authorisation** — `SharedKernel\Authorization\Ability` (`quran.manage`, `quran.board`, `quran.teach`, `quran.examine`), Identity's `AbilityMatrix` (who holds them), Learning's `LearningAccess`.
- **Identity** — `IdentityApi`, `PersonalChannel` (signed personal links, the family's private channel).
- **People** — `PeopleApi`, `FamilyView`, `LearnerStage`, `DTOs\Learner` (kids' / middle / teen looks, guardians).
- **Enrollment** — `EnrollmentApi`, `EnrollmentStatus`, `DTOs\EnrollmentData` (which course a plan and a hifz map follow).
- **Catalog** — `CatalogApi::subjectKind` / `subjectsOfKind`; `subjects.kind` and `quran_track` (Catalog's migration `2027_04_20_100000_add_kind_to_subjects`, saved only through Catalog's `SaveSubject`).
- **Scheduling** — `AssessmentLessons` (`BookAssessmentLesson` for exams), `AttendanceApi`, `DTOs\LessonCard`, `DTOs\AssessmentBooking`.
- **Classroom** — `Contracts\ClassPage` (the lesson's channel and viewer for the mushaf beside the room; `class/{session}/mushaf`).
- **Learning** — `LearningApi` (`lessonReport`, `reportIdsOf`, `reportHandedIn`), events `SessionReportSubmitted` and `HomeworkSubmitted`, Learning's `homework.expected` column.
- **Communication** — `NotificationsApi` (templates `quran.exam_*`, `quran.certificate_issued`), `NotificationLinks` (panel links and personal signed links).
- **Platform** — `BrandingApi` (certificate page), `TenantDirectory`; the console plugin's Quran page.
- **AI** — `SharedKernel\Ai\Capabilities` (the `recitation_check` capability), `AcademyAi`, `AudioClip`, `ExpectedText`, `AiFailed`; Platform's AI gateway routes and meters it.
- **Text** — `SharedKernel\Text\ArabicText` (comparisons in plain spelling), `WordAlignment`, `QuranFetchFailed`.
- **Privacy** — `SharedKernel\Privacy\PersonalData` (`Privacy\QuranData`: a learner's copy and erasure).
- **Setup** — `SharedKernel\Setup\SetupChecklist` (`Setup\QuranStep`, "Start here").
- **Realtime** — `SharedKernel\Realtime\LiveSignals` (`hifz`, `mushaf`, `lesson-mushaf`), the platform's Postgres functions `lms_live` and `lms_notify_family` used by its triggers.
- **Time** — `SharedKernel\Time\*` (learner's clock for the daily review, viewer's time zone).
- **Audit, Files, Filament** — `AuditTrail`, `CleanFile`, `NavGroup`.

### Where the platform registers it

- `apps/api/bootstrap/providers.php` — `QuranServiceProvider::class`.
- `apps/api/composer.json` — PSR-4 `Modules\Quran\` and `Modules\Quran\Database\Seeders\`.
- `apps/api/app/Providers/Filament/{Academy,Teacher,Family}PanelProvider.php` — `QuranPlugin`, `QuranTeacherPlugin`, `QuranFamilyPlugin`.
- `apps/api/modules/Platform/src/Filament/Console/ConsolePlugin.php` — the console's `QuranConsole` page.
- Seeders: `DatabaseSeeder`, `DemoCatchUpSeeder`, `E2eResetSeeder`, `LoadAcademySeeder`, the demo seeders of Catalog, Curriculum, Learning, Scheduling, Crm, People, Payroll, Billing, Site (Quran subjects, lessons and people in the demo).
- Arch tests: `tests/Arch/ModuleBoundariesTest.php` (nothing below may use `Modules\Quran`), `NavGroupTest.php`, `AiGatewayTest.php`.
- Portal: `src/lib/modules.ts`, `src/components/family/{nav,shell}.tsx`, `src/lib/family/nav-items.ts`, teach lesson and student pages, `teach/actions.ts`, `globals.css`, `lib/api/schema.ts` (generated).
- App: `app/router/router.dart`, `app/di/services.dart`, `app/bootstrap.dart`, `core/auth/modules.dart`, `pubspec.yaml` (font), the journey, schedule, dashboard, classroom and teaching screens that open Quran entries.
- Ops: `infra/deploy/deploy.sh` (`php artisan quran:text --fetch --if-missing`), `RUNBOOKS.md`, `.github/workflows/web.yml` (fetches the text for e2e), `academy-new.yml` (plan areas).

---

## Tables it owns

They are created by the migrations in `apps/api/modules/Quran/database/migrations/` and **still exist in the
platform's database** with their data. Nothing was dropped.

| Table | Migration |
|---|---|
| `submission_checks` | `2027_03_05_100000_create_submission_checks` (also adds `homework.expected`, a Learning column) |
| `hifz_pages`, `hifz_reviews`, `hifz_recitations` | `2027_03_12_100000_create_hifz_tables` (also added `learning_settings.hifz_daily_pages`, later moved to `quran_settings` by Learning's `2027_04_20_100300_drop_hifz_daily_pages`) |
| `lesson_mushaf`, `recitation_mistakes` | `2027_03_16_100000_create_lesson_mushaf` |
| `quran_settings`, `quran_lesson_passages` | `2027_04_20_100100_create_quran_settings_and_passages` |
| `quran_programs`, `quran_plans`, `quran_lesson_results` | `2027_05_01_100000_create_quran_programs_and_plans` |
| `quran_exams`, `quran_certificates` | `2027_05_10_100000_create_quran_exams_and_certificates` |

Columns it owns in platform tables: `homework.expected` (Learning), `subjects.kind` and `subjects.quran_track`
(Catalog), and the `"quran"` entry in `saas_plans.features` (Platform, a data migration). Triggers on its tables raise `lms_hifz_live`, `lms_mushaf_live`,
`lms_submission_check_live` and call the platform's `lms_live` / `lms_notify_family`.

The Quran's text itself is not in the database: it is Tanzil's files in the server's storage
(`storage/app/platform/quran`, fetched by `php artisan quran:text --fetch`).

---

## Plugging it back into the platform

1. Copy `apps/api/modules/Quran/` back to `apps/api/modules/Quran/` in the platform, and the files under
   `apps/api/modules/Platform/`, `apps/api/public/fonts/quran/` and `apps/api/tests/` to the same paths.
2. Restore the wiring listed above from `integration-points/` (compare each file with the platform's current one;
   `integration-points/INDEX.md` gives the Quran lines): `bootstrap/providers.php`, `composer.json` autoload, the
   three panel providers, `ConsolePlugin`, the seeder calls, the ability matrix, the arch tests.
3. Make sure the contracts and their defaults still exist in the platform (`LearningQuran`, `JourneyQuran`,
   `LessonQuran`, `QuranSource`, `RecitationEngine`, `Feature::Quran`, the `quran.*` abilities, `subjects.kind`).
   If the platform removed them, copy them back from `integration-points/`.
4. `composer dump-autoload`, then `php artisan migrate`. The tables already exist, so the migrations are already
   recorded and nothing is re-created.
5. `php artisan quran:text --fetch` if the server has no copy of the text.
6. Portal: copy `apps/web/` files back, merge `messages/{en,ar}.quran.json` into `messages/{en,ar}.json`, restore the
   `quran` area in `lib/modules.ts` and the nav entries, then regenerate the API types (`npm run api:types`).
7. App: copy `apps/mobile/` files back, merge `tool/strings.quran.py` rows into `tool/strings.py`, run
   `python3 tool/strings.py` and `flutter gen-l10n`, restore the routes in `app/router/router.dart` and
   `Feature.quran` in `core/auth/modules.dart`, and the font in `pubspec.yaml`.
8. Run the Quran tests: `tests/Feature/Quran`, `tests/Unit/Quran`, `DemoQuranTest`, the portal's Quran tests and
   `quran.spec.ts`, and the app's `quran_test`, `hifz_test`, `mushaf_test`, `recitation_check_test`.

## Growing it into its own app

1. **API** — start a fresh Laravel 13 app and put the module under `modules/Quran`. For each contract in the table
   above, either keep it (the platform calls this app over HTTP) or write a small local version (tenancy, plans,
   abilities, people and enrolments become this app's own tables or come from the platform's API).
2. **Identity** — decide who signs people in: the platform (this app trusts its tokens) or this app (its own users).
3. **Data** — move the tables listed above out of the platform's database with `pg_dump -t` for each table, keeping
   `academy_id` as the tenant key. Rows point at platform ids (`users`, `enrollments`, `sessions`, `lesson_groups`,
   `homework_submissions`, `curriculum_nodes`): keep them as foreign ids without database constraints, or copy what
   is needed.
4. **Events** — the hifz map listens to `SessionReportSubmitted`, the recitation check to `HomeworkSubmitted`, and
   exams book lessons through `AssessmentLessons`. Across two apps these become webhooks or a queue.
5. **Portal and app** — the portal files are Next.js App Router pages and components; the app files are Flutter
   features. Each needs the platform's shared UI (design system, API client, session) or its own.
6. **API types** — `openapi-quran.json` is the contract the released portal and app already call; keep its paths
   (`learning/hifz…`, `learning/lessons/{session}/mushaf`, `learning/mistakes`, `teacher/students/{enrollment}/hifz…`,
   `teacher/texts/quran`, `quran/…`) so they keep working.

---

## What is not cleanly separated

- **Direct reaches into other modules.** `Actions/Recitation/CheckRecitation.php` and
  `Listeners/QueueRecitationCheck.php` use Learning's models (`Homework`, `HomeworkSubmission`); several queries read
  platform tables with `DB::table` (`users`, `enrollments`, `sessions`, `session_participants`, `group_members`,
  `lesson_groups`, `subjects`, `homework`, `homework_submissions`, `curriculum_nodes`). The four demo seeders also call
  Scheduling's and Catalog's actions and models.
- **Recitation check engine.** `SpeechRecitation`, `RecitationEngine`, `ExpectedText`, `WordAlignment` and
  `ArabicText` live in SharedKernel and are shared with other features; they are copied under `integration-points/`,
  not moved.
- **Columns in platform tables** (`homework.expected`, `subjects.kind`/`quran_track`) and the `"quran"` plan feature in `saas_plans.features` belong to their
  modules' migrations; the platform's Learning migration `drop_hifz_daily_pages` is Quran history.
- **Mixed tests.** About 115 platform tests (Billing, Scheduling, Learning, Demo, Privacy, Security…) set up a Quran
  subject or check a Quran behaviour among other things. They are copied whole under `integration-points/apps/api/tests/`;
  their Quran lines are listed in `INDEX.md`.
- **Generated files.** `apps/web/src/lib/api/schema.ts` and the app's `lib/core/l10n/gen/*.dart` were not copied;
  regenerate them from `openapi-quran.json` and the strings.
- **Mixed screens.** The portal's teach lesson and student pages, the report editor, the marking page, the family
  shell and the journey screens, and the app's journey, schedule, teaching and classroom screens contain Quran entries
  inside platform screens. They are under `integration-points/` with their Quran lines in `INDEX.md`.

---

## ملخص بالعربية

هذا المستودع نسخة كاملة من كل ما يخص القرآن في منصة الأكاديمية، مأخوذة كما هي من المستودع الأصلي عند الـ commit
`84aca260` دون أي تعديل: موديول Laravel كاملًا (خريطة الحفظ وورد المراجعة، والمصحف المشترك في الحصة ودفتر الأخطاء،
وتصحيح التسميع، والبرامج والخطط، ونتائج الحصص، والاختبارات والشهادات، والإعدادات، ونسخة المنصة من النص)، واختباراته،
وشاشات القرآن في البوابة (Next.js)، وميزات القرآن في التطبيق (Flutter)، ووثائقه، وجزء القرآن من مواصفات OpenAPI
(`openapi-quran.json`).

- المسارات تطابق مسارات المنصة، فيعود كل ملف إلى مكانه نفسه.
- مجلد `integration-points/` فيه نسخ كاملة من ملفات المنصة التي تربط القرآن بها (العقود وربطاتها الافتراضية، وتسجيل
  الموديول، والقوائم، والـ seeders، والاختبارات المختلطة)، وملف `INDEX.md` يحدد أسطر القرآن في كل ملف.
- جداول القرآن (`hifz_*` و`lesson_mushaf` و`recitation_mistakes` و`submission_checks` و`quran_*`) **ما زالت في قاعدة
  بيانات المنصة ببياناتها**، ولم يُحذف منها شيء.
- المستودع لا يعمل وحده بعد؛ فهو يعتمد على عقود المنصة (المستأجر، والصلاحيات، والباقة `Feature::Quran`، والحصص،
  وغرفة الحصة، وواجبات التسميع، والإشعارات وغيرها). القسم الإنجليزي أعلاه يذكرها كلها، ويشرح خطوة بخطوة كيف يُعاد
  ربطه بالمنصة، أو كيف يُبنى منه تطبيق مستقل.
