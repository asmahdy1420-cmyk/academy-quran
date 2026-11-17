# Integration points (copies of platform files at 84aca260)

Each file below is a **whole copy** of a platform file that is not Quran code itself but wires the Quran in
(a contract with a do-nothing default, a binding, a menu entry, a route, a seeder call, a test that also covers Quran
behaviour). The copy sits at `integration-points/<same path as in the platform>`. Under each file are the lines that
mention the Quran, hifz, mushaf or recitation — those are the Quran parts; the rest of the file is platform code kept
only for context. Contracts are listed even when they mention the Quran only in their name.

Generated and translation files are not copied here; see `extracted/` (OpenAPI, portal messages, app strings, docs).

## API app, seeders, config (13 files)

### `apps/api/README.md`

Lines: 27

```text
27: | `modules/Quran` | Everything of the Quran, on top of everything (nothing depends on it) and switched on per academy by its SaaS plan (`Feature::Quran`): the platform's copy of th…
```

### `apps/api/app/Providers/Filament/AcademyPanelProvider.php`

Lines: 43, 124

```text
43: use Modules\Quran\Filament\QuranPlugin;
124: QuranPlugin::make(),
```

### `apps/api/app/Providers/Filament/FamilyPanelProvider.php`

Lines: 32, 89

```text
32: use Modules\Quran\Filament\Family\QuranFamilyPlugin;
89: QuranFamilyPlugin::make(),
```

### `apps/api/app/Providers/Filament/TeacherPanelProvider.php`

Lines: 32, 90

```text
32: use Modules\Quran\Filament\Teacher\QuranTeacherPlugin;
90: QuranTeacherPlugin::make(),
```

### `apps/api/bootstrap/providers.php`

Lines: 27, 60

```text
27: use Modules\Quran\Providers\QuranServiceProvider;
60: QuranServiceProvider::class,
```

### `apps/api/composer.json`

Lines: 82, 83

```text
82: "Modules\\Quran\\": "modules/Quran/src/",
83: "Modules\\Quran\\Database\\Seeders\\": "modules/Quran/database/seeders/",
```

### `apps/api/config/queue.php`

Lines: 65

```text
65: // The AI helpers' background work (a recitation check, a weekly note):
```

### `apps/api/database/seeders/DatabaseSeeder.php`

Lines: 48, 49, 50, 74, 122, 123, 124

```text
48: use Modules\Quran\Database\Seeders\DemoMistakesSeeder;
49: use Modules\Quran\Database\Seeders\DemoQuranPlansSeeder;
50: use Modules\Quran\Database\Seeders\DemoQuranSeeder;
74: * curricula, lesson reports with homework, the Quran program once the server has its text (plans, recorded lessons, an exam passed with its certificate and one to book), its public…
122: $this->call([DemoBrandingSeeder::class, DemoModulesSeeder::class, DemoPolicySeeder::class, DemoCommunicationSeeder::class, DemoLiveBoardSeeder::class, DemoConsentsSeeder::class, De…
123: // Last: the Quran's plans, recorded lessons and exams book people at moments the seeders above may use.
124: $this->call(DemoQuranPlansSeeder::class);
```

### `apps/api/database/seeders/DemoCatchUpSeeder.php`

Lines: 17, 20, 21, 22, 23, 31, 32, 33, 34, 38, 39, 66, 67, 69, 74, 75, 76, 78, 79, 88

```text
17: use Modules\Platform\Database\Seeders\DemoQuranAreaSeeder;
20: use Modules\Quran\Database\Seeders\DemoHifzSeeder;
21: use Modules\Quran\Database\Seeders\DemoMistakesSeeder;
22: use Modules\Quran\Database\Seeders\DemoQuranPlansSeeder;
23: use Modules\Quran\Database\Seeders\DemoQuranSeeder;
31: * this on every deploy. Once the Quran's text is on the server, the Juz'
32: * Amma lessons read their surahs, each Quran learner's last lesson has a few
33: * marked words, and the reports already handed in make their hifz maps; the
34: * demo's plan takes the AI helpers' and the Quran's areas; and its public page is on, with
38: * the Quran's text is there, its Quran program (DemoQuranPlansSeeder: exams and
39: * certificates on, two ready tracks, its Quran learners on plans, Yousef's last
66: // The Quran's area first: what follows writes the demo's Quran (its subject, its lessons' passages).
… 8 more lines
```

### `apps/api/database/seeders/DemoGroupsSeeder.php`

Lines: 44, 215, 217

```text
44: * Quran group forms with Sama, waiting for three more. Ziad and the other
215: // Mona's Quran group for children forms: Sama has her seat, it starts with four.
217: teacherId: (string) $this->user('mona'), subjectId: $subject('Quran memorisation'), sessionMinutes: 30,
```

### `apps/api/database/seeders/DemoRevenueSeeder.php`

Lines: 35, 37, 94, 100

```text
35: * (a child's Quran with Mahmoud, an adult's Arabic with Khaled, a teenager's
37: * Tajweed with Nour, an adult's English with Ahmed), spread so their
94: 'fahd' => ['name' => 'فهد العتيبي', 'age' => 11, 'guardian' => ['abdullah.otaibi', 'عبدالله العتيبي', 'father'], 'teacher' => 'mahmoud', 'subject' => 'Quran memorisation',
100: 'tamim' => ['name' => 'تميم الدوسري', 'age' => 9, 'guardian' => ['munira.dosari', 'منيرة الدوسري', 'mother'], 'teacher' => 'nour', 'subject' => 'Tajweed',
```

### `apps/api/database/seeders/E2eResetSeeder.php`

Lines: 35, 36, 37, 38, 39, 40, 86, 139, 151, 266, 269, 315, 327, 836, 837, 839, 840, 844, 848, 849, 852, 854, 877, 881

```text
35: use Modules\Quran\Actions\Settings\SaveQuranSettings;
36: use Modules\Quran\Domain\Certificates\CertificateNumber;
37: use Modules\Quran\Models\QuranCertificate;
38: use Modules\Quran\Models\QuranLessonResult;
39: use Modules\Quran\Programs\Plans;
40: use Modules\Quran\Support\QuranArea;
86: * a report of it to write, and the family's sign-ins; with `quran`: Yousef's Quran course, a lesson of it to record
139: $quran = $this->quran();
151: return ['homework' => ['hand_in' => self::HAND_IN, 'to_mark' => self::TO_MARK], 'group' => $group, 'quran' => $quran];
266: * to this run (its own number) whose child (9, the kids' look) took a Tajweed trial with Sara two days ago, as
269: * family whose child missed a Quran trial yesterday, for the "book again" link. The academy gives both the
315: $trial = $family("+2010{$number}", 'أم ليان', 'ليان', $subject('Tajweed'), 2, true);
… 12 more lines
```

### `apps/api/database/seeders/LoadAcademySeeder.php`

Lines: 96, 224, 229

```text
96: ['Quran memorisation', 'قرآن · حفظ', 30], ['Tajweed', 'تجويد', 20], ['Arabic', 'لغة عربية', 20],
224: ['unit' => 'hour', 'amount' => '60'], ['subject_id' => $subjects['Quran memorisation'], 'unit' => 'hour', 'amount' => '70'],
229: $groups = [['Quran memorisation', 'Tajweed'], ['Tajweed', 'Quran memorisation'], ['Arabic', 'Arabic grammar'], ['English', 'Arabic'], ['Quran memorisation', 'Arabic']];
```

## API module Billing (3 files)

### `apps/api/modules/Billing/database/seeders/DemoDiscountsSeeder.php`

Lines: 88, 89

```text
88: $quran = (string) DB::table('subjects')->where('name_en', 'Quran memorisation')->value('id');
89: $enroll->handle($batch, $laila, $quran, new EnrollmentTerms($plan->id, $father, $region->id), $owner);
```

### `apps/api/modules/Billing/lang/en/plans.php`

Lines: 58

```text
58: 'credit_scope' => 'A shared package is one balance for a student in any subject (say 12 lessons a month across Quran and Arabic). Each new course of theirs on it draws on the same …
```

### `apps/api/modules/Billing/src/Queries/InvoiceCourses.php`

Lines: 62

```text
62: /** @param  list<array{student: string, subject: string}>  $courses  "Ziad · Quran", or "Ziad · Quran، Maryam · Arabic" for a family invoice */
```

## API module Catalog (11 files)

### `apps/api/modules/Catalog/database/migrations/2026_11_24_100000_create_subject_levels_and_categories.php`

Lines: 30

```text
30: // A subject's own categories: its tracks (memorising, tajweed,
```

### `apps/api/modules/Catalog/database/migrations/2027_04_20_100000_add_kind_to_subjects.php`

Lines: 9, 10, 11, 12, 20, 23, 24, 30

```text
9: * A subject's kind (docs/architecture/02, section 26): general, or quran with
10: * its track (hifz: memorization, tilawa: recitation and tajweed, talqin:
11: * dictation for children, noorani: the Noorani Qaida). A Quran subject's
12: * courses are the Quran module's to follow; changed only through SaveSubject.
20: $table->string('quran_track', 10)->nullable();
23: (kind = 'general' and quran_track is null)
24: or (kind = 'quran' and quran_track in ('hifz', 'tilawa', 'talqin', 'noorani')))");
30: Schema::table('subjects', fn (Blueprint $table) => $table->dropColumn(['kind', 'quran_track']));
```

### `apps/api/modules/Catalog/database/seeders/DemoCatalogSeeder.php`

Lines: 16, 17, 20

```text
16: 'Quran memorisation' => [
17: [['القاعدة النورانية', 'Noorani Qaida'], ['جزء عمّ', 'Juz Amma'], ['جزء تبارك', 'Juz Tabarak'], ['5 أجزاء', '5 juz'], ['10 أجزاء', '10 juz'], ['القرآن كامل', 'The whole Quran']],
20: 'Tajweed' => [
```

### `apps/api/modules/Catalog/lang/ar/subjects.php`

Lines: 24, 35, 36, 39, 40

```text
24: 'quran_track' => 'المسار',
35: 'kinds' => ['general' => 'عامة', 'quran' => 'قرآن'],
36: 'tracks' => ['hifz' => 'الحفظ', 'tilawa' => 'التلاوة والتجويد', 'talqin' => 'التلقين للأطفال', 'noorani' => 'القاعدة النورانية'],
39: 'quran_track' => 'اختر مسار القرآن.',
40: 'quran_off' => 'باقة الأكاديمية لا تشمل القرآن، فلا يمكن جعل المادة مادة قرآن.',
```

### `apps/api/modules/Catalog/lang/en/subjects.php`

Lines: 6, 23, 24, 32, 35, 36, 38, 39, 40

```text
6: 'subtitle' => 'Each subject with its levels in order and its categories (tracks such as memorising and tajweed, or curricula such as British and Saudi). A teacher takes a range of …
23: 'kind_hint' => 'A Quran subject is followed by the Quran section: the hifz map, the mushaf in the lesson and the recitation check.',
24: 'quran_track' => 'Track',
32: 'categories_hint' => "The subject's tracks or curricula, such as memorising, tajweed, foundations, conversation, British curriculum.",
35: 'kinds' => ['general' => 'General', 'quran' => 'The Quran'],
36: 'tracks' => ['hifz' => 'Memorisation', 'tilawa' => 'Recitation and tajweed', 'talqin' => 'Dictation for children', 'noorani' => 'Noorani Qaida'],
38: 'kind' => 'Choose general or the Quran.',
39: 'quran_track' => 'Choose the Quran track.',
40: 'quran_off' => "The academy's plan does not include the Quran, so a subject cannot be made a Quran subject.",
```

### `apps/api/modules/Catalog/src/Actions/SaveSubject.php`

Lines: 23, 25, 67, 69, 81, 83, 84, 85, 87, 88, 89, 92

```text
23: public const KINDS = ['general', 'quran'];
25: public const QURAN_TRACKS = ['hifz', 'tilawa', 'talqin', 'noorani'];
67: * The subject's kind and track as kept: a Quran subject has a track (hifz when none is said), a general one none.
69: * @return array{kind?: string, quran_track?: ?string}
81: return ['kind' => 'general', 'quran_track' => null];
83: $track = $track ?: ($subject->quran_track ?? 'hifz');
84: if (! in_array($track, self::QURAN_TRACKS, true)) {
85: throw ValidationException::withMessages(['quran_track' => __($e.'quran_track')]);
87: $already = $subject->exists && $subject->kind === 'quran' && $subject->quran_track === $track;
88: if (! $already && ! $this->plan->has(Feature::Quran)) {
89: throw ValidationException::withMessages(['kind' => __($e.'quran_off')]);
92: return ['kind' => 'quran', 'quran_track' => $track];
```

### `apps/api/modules/Catalog/src/CatalogService.php`

Lines: 39, 41

```text
39: $subject = Subject::query()->find($subjectId, ['id', 'kind', 'quran_track']);
41: return $subject === null ? null : ['kind' => $subject->kind, 'quran_track' => $subject->quran_track];
```

### `apps/api/modules/Catalog/src/Contracts/CatalogApi.php` — contract

Lines: 21, 23

```text
21: * A subject's kind (general, or quran with its track: hifz, tilawa, talqin, noorani); null when there is no such subject.
23: * @return ?array{kind: string, quran_track: ?string}
```

### `apps/api/modules/Catalog/src/Filament/Subjects/SubjectResource.php`

Lines: 95, 97, 98, 99, 100, 101, 102, 108, 109, 111, 127, 156, 172

```text
95: // The kind, as two cards: general, or the Quran (its courses are the Quran module's), offered while the plan has it.
97: ->options(['general' => __('catalog::subjects.kinds.general'), 'quran' => __('catalog::subjects.kinds.quran')])
98: ->icons(['general' => Heroicon::OutlinedBookOpen, 'quran' => Heroicon::OutlinedSparkles])
99: ->visible(fn (Get $get) => self::quranOffered() || $get('kind') === 'quran'),
100: Select::make('quran_track')->label(__($l.'quran_track'))->native(false)->default('hifz')->required(fn (Get $get) => $get('kind') === 'quran')
101: ->options(collect(SaveSubject::QURAN_TRACKS)->mapWithKeys(fn (string $t) => [$t => __('catalog::subjects.tracks.'.$t)])->all())
102: ->visible(fn (Get $get) => $get('kind') === 'quran'),
108: /** Whether a subject may become the Quran: the academy's plan has it. */
109: public static function quranOffered(): bool
111: return app(AcademyPlan::class)->has(Feature::Quran);
127: ->state(fn (Subject $s) => $s->kind === 'quran' ? __('catalog::subjects.kinds.quran').' · '.__('catalog::subjects.tracks.'.$s->quran_track) : null),
156: 'quran_track' => $subject->quran_track,
… 1 more lines
```

### `apps/api/modules/Catalog/src/Models/Subject.php`

Lines: 15, 16, 23

```text
15: * @property string $kind general | quran (its courses the Quran module's to follow)
16: * @property ?string $quran_track hifz | tilawa | talqin | noorani, for a Quran subject
23: protected $fillable = ['name_ar', 'name_en', 'kind', 'quran_track'];
```

### `apps/api/modules/Catalog/src/Models/SubjectCategory.php`

Lines: 10

```text
10: * A subject's track or curriculum (memorising, tajweed; British, Saudi).
```

## API module Classroom (3 files)

### `apps/api/modules/Classroom/resources/views/class.blade.php`

Lines: 200

```text
200: {{-- What another module puts beside the room (SharedKernel's LessonQuran). --}}
```

### `apps/api/modules/Classroom/src/Contracts/ClassPage.php` — contract

Lines: 9

```text
9: * (SharedKernel's LessonQuran): who is looking, and the lesson's own live
```

### `apps/api/modules/Classroom/src/Http/Controllers/ClassroomPageController.php`

Lines: 21, 41, 56, 57

```text
21: use Modules\SharedKernel\Quran\LessonQuran;
41: public function show(Request $request, string $session, LearningApi $learning, BrandingApi $branding, TenantContext $tenant, RecordingState $recording, LessonQuran $quran): View
56: // What another module puts beside the room for this seat (LessonQuran), none for a hidden observer.
57: $side = $seat->role === 'observer' ? null : $quran->classPanel($lesson->id, $seat->userId, [
```

## API module Crm (2 files)

### `apps/api/modules/Crm/database/seeders/DemoCrmSeeder.php`

Lines: 52, 63, 64, 72, 79, 86, 88, 90, 92, 113

```text
52: [$quran, $tajweed, $arabic] = [$subject('Quran memorisation'), $subject('Tajweed'), $subject('Arabic')];
63: 'learner_name' => 'عمر', 'learner_birth_year' => 2018, 'subject_id' => $quran, 'preferred_days' => [6, 7, 1], 'preferred_from' => 16, 'preferred_to' => 20,
64: 'source' => 'instagram', 'utm_source' => 'instagram', 'utm_medium' => 'paid', 'utm_campaign' => 'hifz-autumn', 'notes' => 'تريد معلّمة، وعمر يحفظ جزء عمّ.']), 3);
72: 'learner_name' => 'كريم', 'learner_birth_year' => 2015, 'subject_id' => $tajweed, 'preferred_days' => [7, 2, 4], 'preferred_from' => 17, 'preferred_to' => 21]);
79: 'learner_name' => 'سارة', 'learner_birth_year' => 2016, 'subject_id' => $quran, 'preferred_days' => [2, 3, 4, 5, 6, 7, 1], 'preferred_from' => 18, 'preferred_to' => 22,
86: 'learner_name' => 'يحيى', 'learner_birth_year' => 2017, 'subject_id' => $quran, 'preferred_days' => [1, 3], 'preferred_from' => 17, 'preferred_to' => 20, 'source' => 'facebook']);
88: 'learner_name' => 'جنى', 'learner_birth_year' => 2013, 'subject_id' => $tajweed, 'preferred_days' => [6, 1], 'preferred_from' => 18, 'preferred_to' => 21, 'source' => 'google']);
90: 'learner_name' => 'تميم', 'learner_birth_year' => 2016, 'subject_id' => $quran, 'preferred_days' => [7, 3], 'preferred_from' => 17, 'preferred_to' => 21, 'source' => 'tiktok']);
92: foreach ([[$yahya, $nour, $quran, 1], [$jana, $sara, $tajweed, 3], [$tamim, $sara, $quran, 5]] as [$l, $teacher, $subj, $days]) {
113: 'learner_name' => 'مالك', 'learner_birth_year' => 2014, 'subject_id' => $quran, 'source' => 'facebook']);
```

### `apps/api/modules/Crm/database/seeders/DemoTrialReportSeeder.php`

Lines: 16

```text
16: * gives a free second trial with another teacher; Jana's assessed Tajweed
```

## API module Curriculum (4 files)

### `apps/api/modules/Curriculum/database/migrations/2027_03_02_100000_add_text_source_to_curriculum_nodes.php`

Lines: 10, 12, 19, 24

```text
10: * typed, or a passage of the Quran by surah and verses (its words always
12: * passage a recitation is checked against.
19: $table->jsonb('text_source')->nullable();      // {kind: text, text} | {kind: quran, surah, from, to}
24: or (kind = 'lesson' and text_source->>'kind' = 'quran' and jsonb_typeof(text_source->'surah') = 'number'
```

### `apps/api/modules/Curriculum/database/seeders/DemoCurriculumSeeder.php`

Lines: 47, 61

```text
47: 'Quran memorisation' => ['حفظ جزء عمّ', 'Juz\' Amma memorisation', true, [
61: 'Tajweed' => ['نور البيان', 'Nour Al-Bayan', true, [
```

### `apps/api/modules/Curriculum/database/seeders/DemoMaterialsSeeder.php`

Lines: 21, 24, 27, 29, 31, 34, 36, 38, 48, 52

```text
21: ['Quran memorisation', 'Al-Fatiha', [
24: ['link', 'الفاتحة على quran.com', 'Al-Fatiha on quran.com', 'all', 'https://quran.com/1'],
27: ['Quran memorisation', 'An-Nas and Al-Falaq', [
29: ['link', 'سورة الناس على quran.com', 'An-Nas on quran.com', 'all', 'https://quran.com/114'],
31: ['Quran memorisation', 'Al-Kawthar and Al-Ma\'un', [
34: ['link', 'سورة الكوثر على quran.com', 'Al-Kawthar on quran.com', 'all', 'https://quran.com/108'],
36: ['Quran memorisation', 'Quraysh and Al-Fil', [
38: ['link', 'سورة قريش على quran.com', 'Quraysh on quran.com', 'all', 'https://quran.com/106'],
48: ['Tajweed', 'Izhar', [
52: ['Tajweed', 'Idgham', [
```

### `apps/api/modules/Curriculum/database/seeders/DemoPracticeSeeder.php`

Lines: 14, 22, 33, 42, 49, 90, 105, 121

```text
14: * a tajweed rule and its example, a letter and its name, and English words
22: ['Quran memorisation', 'Al-Fatiha', [
33: ['Quran memorisation', 'An-Nas and Al-Falaq', [
42: ['Quran memorisation', 'Al-Kawthar and Al-Ma\'un', [
49: ['Quran memorisation', 'Quraysh and Al-Fil', [
90: ['Tajweed', 'Single letters', [
105: ['Tajweed', 'Izhar', [
121: ['Tajweed', 'Idgham', [
```

## API module Identity (2 files)

### `apps/api/modules/Identity/src/Authorization/AbilityMatrix.php`

Lines: 76, 77, 78, 79, 80, 81

```text
76: // The Quran module: its settings and programs are the academy's setup; the board is for who follows the teachers;
77: // a teacher teaches the Quran; examining is for who oversees the teachers until the academy chooses examiners.
78: Ability::ManageQuran => [Role::Owner, Role::Admin],
79: Ability::ViewQuranBoard => [Role::Owner, Role::Admin, Role::Supervisor],
80: Ability::TeachQuran => [Role::Teacher],
81: Ability::ExamineQuran => [Role::Owner, Role::Admin, Role::Supervisor],
```

### `apps/api/modules/Identity/src/Http/V1/Resources/UserResource.php`

Lines: 55

```text
55: // as SharedKernel\Plans\Feature values: crm, online_payments, import, custom_branding, payroll, ai, quran, groups,
```

## API module Import (1 files)

### `apps/api/modules/Import/lang/en/examples.php`

Lines: 5, 13

```text
5: ['name' => 'Sara Mahmoud', 'email' => 'sara.m@example.com', 'phone' => '01012345678', 'gender' => 'female', 'timezone' => 'Egypt', 'subjects' => 'Quran, Tajweed', 'languages' => 'A…
13: ['student_name' => 'Yousef Ahmed', 'contact' => '+447700900123', 'teacher' => 'sara.m@example.com', 'subject' => 'Quran', 'duration' => '30', 'times' => 'Saturday 18:00, Tuesday 18…
```

## API module Learning (22 files)

### `apps/api/modules/Learning/database/migrations/2026_11_08_100000_create_report_templates.php`

Lines: 12

```text
12: * every lesson has (pages memorised, tajweed mistakes, new words…). Each
```

### `apps/api/modules/Learning/database/migrations/2027_04_20_100300_drop_hifz_daily_pages.php`

Lines: 8, 9, 15, 20

```text
8: * The daily review's pages moved to the academy's Quran settings
9: * (quran_settings, copied there before this runs).
15: Schema::table('learning_settings', fn (Blueprint $table) => $table->dropColumn('hifz_daily_pages'));
20: Schema::table('learning_settings', fn (Blueprint $table) => $table->unsignedSmallInteger('hifz_daily_pages')->default(3));
```

### `apps/api/modules/Learning/database/seeders/DemoLearningSeeder.php`

Lines: 34, 111, 114, 115, 117, 163, 166

```text
34: * voice recordings. The academy's own questions for three subjects (Quran
111: $q('التجويد', 'Tajweed', 'choice', $choices([['ممتاز', 'Excellent'], ['جيد', 'Good'], ['يحتاج إلى عمل', 'Needs work']])),
114: 'Quran memorisation' => $memorisation,
115: 'Tajweed' => [
117: $q('القراءة من المصحف', 'Reading from the Mushaf', 'choice', $choices([['من دون أخطاء', 'No mistakes'], ['أخطاء قليلة', 'A few mistakes'], ['تحتاج إلى تدريب', 'Needs practice']])),
163: if ($key === 'yousef' && $i === 3 && $subject('Quran memorisation') !== '') {
166: $templates->handle($subject('Quran memorisation'), [...ReportTemplate::currentFor($subject('Quran memorisation'))->fields,
```

### `apps/api/modules/Learning/lang/en/digest.php`

Lines: 25, 38

```text
25: 'title' => ':student recites',
38: 'what' => "It holds: lessons attended and missed, the lessons and how they went, the teacher's words for the family, the academy's questions families see, homework, practice and th…
```

### `apps/api/modules/Learning/lang/en/notifications.php`

Lines: 45

```text
45: 'weekly_digest_voice' => ['title' => ":student's week", 'body' => ':body Hear :student recite from this week: :link'],
```

### `apps/api/modules/Learning/lang/en/templates.php`

Lines: 6

```text
6: 'subtitle' => 'Your own questions in each subject\'s lesson report, after the stars and notes every report has: pages memorised, tajweed, new words… Each save is a new version: rep…
```

### `apps/api/modules/Learning/resources/views/filament/teacher/submissions.blade.php`

Lines: 1

```text
1: {{-- What the student handed in: text, a recording that plays here, or a file; what the homework asks to recite and each recording's check, when the Quran module adds them (Learnin…
```

### `apps/api/modules/Learning/src/Actions/SubmitSessionReport.php`

Lines: 15, 39, 56, 59, 150

```text
15: use Modules\Learning\Contracts\LearningQuran;
39: private readonly LearningQuran $recitation,
56: // What the homework asks to recite, for the teacher's check: left as it is unless the form says.
59: ? ['value' => $this->recitation->recitationTarget($given['expected'], (string) ($given['accepts'] ?? 'any'), $report->homework()->first()?->expected)]
150: * @param  array{value?: ?array<string, mixed>}  $expected  what to recite, when the form says (LearningQuran)
```

### `apps/api/modules/Learning/src/Contracts/DTOs/LessonReport.php`

Lines: 8

```text
8: * A lesson report as another module reads it (the Quran's hifz map): which
```

### `apps/api/modules/Learning/src/Contracts/JourneyQuran.php` — contract

Lines: 6, 7, 9, 12, 13

```text
6: * The Quran on a learner's journey (docs/architecture/02, section 26), which
7: * the Quran module binds; the journey is whole without it (NoJourneyQuran).
9: interface JourneyQuran
12: * Today's hifz review for the journey's card: pages left today, done today and a day's pages; null when the
13: * learner has none (no hifz map, or the academy's plan leaves the Quran out).
```

### `apps/api/modules/Learning/src/Contracts/LearningQuran.php` — contract

Lines: 9, 11, 12, 13, 15, 17, 18, 21, 29, 32, 55, 63, 71, 81

```text
9: * What the Quran module adds to Learning's own screens and answers
11: * has the Quran; without it (NoLearningQuran) reports and homework are
12: * whole and simply ask nothing of the Quran. Homework keeps what it asks to
13: * recite in homework.expected, which only this reads and checks.
15: interface LearningQuran
17: /** Whether a report's homework may ask what to recite now (the teacher's check of recited homework). */
18: public function recitationOffered(): bool;
21: * What a homework asks to recite, from the report's form (null: none), as homework.expected keeps it. What
29: public function recitationTarget(mixed $input, string $accepts, ?array $current): ?array;
32: * What a homework asks to recite, as forms and answers show it.
55: * Each recording's check against what the homework asks to recite, by submission, for the teacher alone.
63: * The report form's fields for what the homework asks to recite (state homework.recite, homework.expected.*).
… 2 more lines
```

### `apps/api/modules/Learning/src/Contracts/NoJourneyQuran.php` — contract

Lines: 5, 6

```text
5: /** No Quran on the journey: the module is not there. */
6: final class NoJourneyQuran implements JourneyQuran
```

### `apps/api/modules/Learning/src/Contracts/NoLearningQuran.php` — contract

Lines: 7, 8, 10, 15, 17

```text
7: /** Reports and homework without the Quran: nothing to recite, check or show. */
8: final class NoLearningQuran implements LearningQuran
10: public function recitationOffered(): bool
15: public function recitationTarget(mixed $input, string $accepts, ?array $current): ?array
17: // Nothing new is asked to recite; taking it off stays possible.
```

### `apps/api/modules/Learning/src/Digest/WeekFacts.php`

Lines: 163

```text
163: /** The recording of the week a guardian may hear: the best recited one handed in, when its check or mark says it went well. */
```

### `apps/api/modules/Learning/src/Filament/Family/FamilyHomework.php`

Lines: 23

```text
23: * a file or a recording made right here (reciting, reading), or
```

### `apps/api/modules/Learning/src/Filament/Teacher/HomeworkToMark.php`

Lines: 22, 31, 124, 125

```text
22: use Modules\Learning\Contracts\LearningQuran;
31: * what to recite (for the teacher alone). Follows the teacher's `homework` signal.
124: 'target' => app(LearningQuran::class)->targetView($h->expected),
125: 'checks' => array_map(fn (array $c) => app(LearningQuran::class)->checkView($c), app(LearningQuran::class)->checks($h->id, $h->expected)),
```

### `apps/api/modules/Learning/src/Filament/Teacher/StudentProgress.php`

Lines: 11, 19, 51

```text
11: use Modules\Learning\Contracts\LearningQuran;
19: * (the Quran's hifz map) is a way out from the header (LearningQuran).
51: return app(LearningQuran::class)->studentActions($this->enrollment);
```

### `apps/api/modules/Learning/src/Filament/Teacher/WriteReport.php`

Lines: 30, 55, 56, 85, 86, 88, 110, 111, 112, 113, 114, 115, 118, 135, 136, 226, 271, 272, 274, 278, 282, 284, 411, 412, 413, 414, 418, 429, 430

```text
30: use Modules\Learning\Contracts\LearningQuran;
55: * homework handed in by voice may say what to recite where the Quran module
56: * adds it (LearningQuran), so each recording is checked word by word for the
85: /** What the report's lessons ask to recite, as it reads (null: none, or the homework has its own; LearningQuran). */
86: public ?string $reciteSuggestion = null;
88: /** What the words marked in this lesson suggest reciting (surah, from, to, title), offered with one tap (LearningQuran). */
110: $quran = app(LearningQuran::class);
111: // What to recite: the homework's own, else what the report's lessons ask, ready for when the teacher turns it on.
112: $recite = $quran->presentTarget($homework?->expected);
113: if ($recite === null && $this->sessionReport->kind === 'lesson') {
114: $recite = $quran->targetFromLessons(array_column(app(ReportFormQuery::class)->items($this->sessionReport), 'node_id'));
115: $this->reciteSuggestion = $recite['title'] ?? null;
… 17 more lines
```

### `apps/api/modules/Learning/src/Http/V1/Controllers/JourneyController.php`

Lines: 9, 159, 160, 286, 287, 289

```text
9: use Modules\Learning\Contracts\JourneyQuran;
159: /** The hifz review today (GET learning/hifz has it in full): pages left today, done today and a day's pages; null until the learner has pages on their hifz map, or while the acade…
160: 'hifz' => $this->hifzToday($learner),
286: /** @return ?array{due: int, done_today: int, daily: int} the Quran module's (JourneyQuran) */
287: private function hifzToday(string $learner): ?array
289: return app(JourneyQuran::class)->today($learner);
```

### `apps/api/modules/Learning/src/Http/V1/Controllers/TeacherReportsController.php`

Lines: 15, 40, 73, 74, 75, 86, 89, 92, 94, 95, 96, 97, 168, 179, 191, 192, 196, 199, 200, 203

```text
15: use Modules\Learning\Contracts\LearningQuran;
40: private readonly LearningQuran $recitation,
73: * Homework handed in by voice may say what to recite (`homework.expected`: surah, from, to) when
74: * `assist.recitation_check`; `expected_suggestion` is the passage of the report's lessons' text, and
75: * `mistakes_suggestion` the verses with the words marked in the lesson's shared mushaf.
86: 'homework' => $homework ? $this->recited($homework) : null,
89: // and a check of recited homework against what it asks to recite (homework.expected).
92: 'recitation_check' => $report->status !== 'reviewed' && $this->recitation->recitationOffered(),
94: // What the report's lessons ask to recite, to start homework.expected from (null: none).
95: 'expected_suggestion' => $report->kind === 'lesson' ? $this->recitation->targetFromLessons(array_column($items, 'node_id')) : null,
96: // The verses with the words marked in the lesson's shared mushaf (the surah with the most marks; null: none).
97: 'mistakes_suggestion' => $report->kind === 'lesson' ? $this->recitation->targetFromMistakes($report->session_id) : null,
… 8 more lines
```

### `apps/api/modules/Learning/src/Models/Homework.php`

Lines: 34

```text
34: * @property ?array<string, mixed> $expected what is to be recited, as the module that reads it keeps it (LearningQuran), checked word by word for the teacher
```

### `apps/api/modules/Learning/src/Providers/LearningServiceProvider.php`

Lines: 24, 26, 27, 28, 64, 65, 66

```text
24: use Modules\Learning\Contracts\JourneyQuran;
26: use Modules\Learning\Contracts\LearningQuran;
27: use Modules\Learning\Contracts\NoJourneyQuran;
28: use Modules\Learning\Contracts\NoLearningQuran;
64: // Reports, homework and the journey ask nothing of the Quran until the Quran module binds its own.
65: $this->app->bindIf(LearningQuran::class, NoLearningQuran::class);
66: $this->app->bindIf(JourneyQuran::class, NoJourneyQuran::class);
```

## API module Payroll (1 files)

### `apps/api/modules/Payroll/database/seeders/DemoPayrollSeeder.php`

Lines: 17, 43, 47

```text
17: * riyals (by the hour, Quran memorisation a little higher, trials a flat
43: $quran = DB::table('subjects')->where('name_en', 'Quran memorisation')->value('id');
47: $quran ? ['subject_id' => $quran, 'unit' => 'hour', 'amount' => '70'] : null,
```

## API module People (1 files)

### `apps/api/modules/People/database/seeders/DemoPeopleSeeder.php`

Lines: 34, 35, 36, 39

```text
34: 'mahmoud' => [['kids', 'middle'], 6, [$teaches('Quran memorisation', 'Noorani Qaida', '10 juz', ['New memorisation', 'Revision']), $teaches('Tajweed', 'Beginner', 'Intermediate')]]…
35: 'nour' => [[], 8, [$teaches('Quran memorisation', null, null), $teaches('Tajweed', null, null)]],
36: 'sara' => [['middle', 'teen', 'adults'], 6, [$teaches('Tajweed', 'Intermediate', null, ['Hafs', 'Al-Jazariyya']), $teaches('Quran memorisation', '5 juz', null, ['Revision', 'Ijazah…
39: 'mona' => [['kids'], 5, [$teaches('Arabic', 'Level 1', 'Level 3', ['Saudi curriculum']), $teaches('Quran memorisation', 'Noorani Qaida', 'Juz Tabarak', ['New memorisation'])]],
```

## API module Platform (19 files)

### `apps/api/modules/Platform/database/migrations/2026_12_14_100000_create_game_catalog.php`

Lines: 97

```text
97: $table->string('topic', 160)->default('');             // what the academies teach with it (Quran memorisation, Arabic letters, ...)
```

### `apps/api/modules/Platform/database/migrations/2027_03_01_100000_create_ai_tables.php`

Lines: 23

```text
23: $table->boolean('recitation_check')->default(false);
```

### `apps/api/modules/Platform/database/migrations/2027_08_20_100000_create_usage_ledger.php`

Lines: 31, 52

```text
31: *   wording 1, outline 5, recitation check 2 (a one-minute recording) and
52: 'recitation_check' => [0, 2], 'report_draft' => [2, 1],
```

### `apps/api/modules/Platform/database/seeders/DemoPlansSeeder.php`

Lines: 17, 28

```text
17: * second) and the AI helpers' and the Quran's areas added, and every academy counted for the
28: $change->handle($demo->id, $pro->id, 'اتفاق على 10 معلّمين فقط حتى تجديد العقد في يناير', ['teachers' => 10], [Feature::Ai->value, Feature::Quran->value]);
```

### `apps/api/modules/Platform/database/seeders/DemoUsageSeeder.php`

Lines: 26

```text
26: private const AI_DAY = ['practice_items' => 4, 'report_draft' => 9, 'digest_wording' => 2, 'recitation_check' => 6, 'curriculum_outline' => 5];
```

### `apps/api/modules/Platform/lang/ar/ai.php`

Lines: 30, 49

```text
30: 'recitation_check' => [
49: 'recitation_check' => 'بسم الله الرحمن الرحيم إذا جاء نصر الله والفتح ورأيت الناس يدخلون في دين الله أفواجا فسبح بحمد ربك واستغفره إنه كان توابا',
```

### `apps/api/modules/Platform/lang/ar/console.php`

Lines: 119

```text
119: 'quran' => [
```

### `apps/api/modules/Platform/lang/ar/settings.php`

Lines: 150

```text
150: 'quran' => [
```

### `apps/api/modules/Platform/lang/en/ai.php`

Lines: 30, 31, 40, 48, 49

```text
30: 'recitation_check' => [
31: 'what' => 'When a student hands in a recitation, the helper compares it with the expected text and marks missing or wrong words, for the teacher only.',
40: 'data' => 'Sent to :provider: the subject and its levels, the age group, the number of lessons and the goal you type. No one\'s name or details. For the Quran, lessons are surah an…
48: 'report_draft' => 'We finished An-Nasr and he knew it well, we reviewed Al-Kafirun and he needed focus. Homework: recite An-Nasr three times. Great engagement.',
49: 'recitation_check' => 'بسم الله الرحمن الرحيم إذا جاء نصر الله والفتح ورأيت الناس يدخلون في دين الله أفواجا فسبح بحمد ربك واستغفره إنه كان توابا',
```

### `apps/api/modules/Platform/lang/en/console.php`

Lines: 119, 120, 121, 122, 123, 127, 130

```text
119: 'quran' => [
120: 'nav' => 'Quran',
121: 'title' => 'The Quran',
122: 'subtitle' => 'The platform\'s copy of the Quran\'s text, and the academies whose plan has the Quran.',
123: 'tiles' => ['on' => 'Academies with the Quran', 'off' => 'Academies without it'],
127: 'academies' => 'Academies with the Quran',
130: 'none' => 'No academy has the Quran now.',
```

### `apps/api/modules/Platform/lang/en/games.php`

Lines: 22

```text
22: 'topic_placeholder' => 'Quran memorisation, Arabic letters, times tables, English words…',
```

### `apps/api/modules/Platform/lang/en/health.php`

Lines: 69

```text
69: 'assist' => 'The AI helpers\' worker is down or behind: recitation checks and weekly notes wait. docker compose logs worker.',
```

### `apps/api/modules/Platform/lang/en/settings.php`

Lines: 61, 150, 151, 152, 156, 157, 158, 199

```text
61: 'speech' => ['title' => 'Speech to text (ElevenLabs)', 'about' => 'Hears teachers\' voice notes and students\' recitations; nothing is sent until an academy turns a helper that lis…
150: 'quran' => [
151: 'title' => "The Quran's text",
152: 'about' => "Tanzil's Simple text and its metadata, fetched to the server and checked whole (114 surahs, 6,236 verses) before they are kept. Every word of the Quran a screen or a he…
156: 'fetched' => "The Quran's text is on the server, checked: 114 surahs, 6,236 verses.",
157: 'failed' => "The Quran's text was not fetched; the copy in use stays.",
158: 'missing' => 'Not on the server yet: lessons cannot name a passage of the Quran until it is.',
199: 'speech_none' => 'No ElevenLabs key yet: voice notes and recitation checks stay off.',
```

### `apps/api/modules/Platform/src/Ai/GeminiLanguageModel.php`

Lines: 27

```text
27: private const REFUSED = ['SAFETY', 'RECITATION', 'BLOCKLIST', 'PROHIBITED_CONTENT', 'SPII', 'IMAGE_SAFETY', 'LANGUAGE'];
```

### `apps/api/modules/Platform/src/Domain/Metering/CreditRates.php`

Lines: 14

```text
14: /** About 64 kbit/s, the voice notes and recitations the apps record. */
```

### `apps/api/modules/Platform/src/Filament/Console/ConsolePlugin.php`

Lines: 27, 34, 49

```text
27: use Modules\Platform\Filament\Console\Pages\QuranConsole;
34: /** The platform team's console: the academies, their use, plans and status, the plans on sale and what academies asked about theirs, the games studio, the audit log across them, t…
49: $panel->pages([Academies::class, AcademyOverview::class, Plans::class, PlanRequests::class, GameStudio::class, GameDraftPage::class, GameEditor::class, AuditLog::class, Health::cla…
```

### `apps/api/modules/Platform/src/Games/Designer/DesignerPrompt.php`

Lines: 23, 28, 38

```text
23: You are the game designer of an online academy platform. Academies on the platform teach children, teenagers and adults one-to-one (Quran memorisation and recitation, Arabic, maths…
28: The words, questions and answers always come from the learner's curriculum at run time, through the bridge, as items. A game never contains its own questions, answers, verses, word…
38: item.dir      'rtl' | 'ltr' | 'auto': the way the item's own words read. Academies teach many subjects and languages (the Quran, Arabic, English, ...), so an item may read the othe…
```

### `apps/api/modules/Platform/src/Http/V1/Controllers/BrandingController.php`

Lines: 29

```text
29: * ai, quran, groups, curriculum, games, messaging, announcements, support, evaluation, site); the core is always on and not listed.
```

### `apps/api/modules/Platform/src/Models/AiSettings.php`

Lines: 20, 40, 44

```text
20: * @property bool $recitation_check
40: protected $attributes = ['practice_items' => false, 'report_draft' => false, 'recitation_check' => false, 'digest_wording' => false, 'curriculum_outline' => false, 'disabled' => '[…
44: return ['practice_items' => 'boolean', 'report_draft' => 'boolean', 'recitation_check' => 'boolean', 'digest_wording' => 'boolean', 'curriculum_outline' => 'boolean', 'disabled' =>…
```

## API module Privacy (1 files)

### `apps/api/modules/Privacy/lang/en/legal.php`

Lines: 56

```text
56: 'AI services, only for the helpers the academy turns on (practice questions from a lesson\'s text, a report drafted from the teacher\'s voice note, checking a recited passage, the …
```

## API module Scheduling (6 files)

### `apps/api/modules/Scheduling/database/seeders/DemoEnrollmentsSeeder.php`

Lines: 105, 106, 112, 113

```text
105: $history('nour', 'yousef', 'Quran memorisation', [[6, '18:00'], [4, '19:00']], 30, 'GBP', 'TRX-40417');
106: $history('sara', 'maryam', 'Tajweed', [[2, '17:00'], [7, '19:00']], 45, 'SAR', 'SA-90542', studentMissed: 3);
112: ['sara', 'hamza', 'Quran memorisation', 7, '20:00', 30, 'AED', 'overdue'],
113: ['mahmoud', 'omar', 'Tajweed', 1, '19:00', 45, 'SAR', 'due'],
```

### `apps/api/modules/Scheduling/database/seeders/DemoFamilyBillingSeeder.php`

Lines: 28, 98, 101, 106, 107, 118

```text
28: * takes Quran twice a week with Mahmoud; Nada takes English twice a week
98: $quran = $course('mahmoud', $karim, 'Quran memorisation', [[6, '17:00'], [3, '17:00']], $twice->id);
101: foreach ([$quran, $english] as $i => $booked) {
106: $courses = [$quran->enrollmentId, $english->enrollmentId, $arabic->enrollmentId];
107: $student = [$quran->enrollmentId => $karim, $english->enrollmentId => $nada, $arabic->enrollmentId => $nada];
118: $fund->handle($quran->enrollmentId);
```

### `apps/api/modules/Scheduling/database/seeders/DemoLiveBoardSeeder.php`

Lines: 33, 34, 90, 94, 97, 100, 107

```text
33: 'tajweed' => $catalog->createSubject('تجويد', 'Tajweed'),
34: 'quran' => $catalog->createSubject('قرآن · حفظ', 'Quran memorisation'),
90: $rana = $book('nour', 'rana', 'quran', -120, 30);
94: $omar = $book('mahmoud', 'omar', 'tajweed', -3, 45);
97: $yousef = $book('nour', 'yousef', 'quran', -3, 30);
100: $maryam = $book('sara', 'maryam', 'tajweed', -33, 45);
107: $book('sara', 'hamza', 'quran', 27, 30, funding: 'unfunded');
```

### `apps/api/modules/Scheduling/database/seeders/DemoOpenHoursSeeder.php`

Lines: 27, 32

```text
27: * of those weeks, so three teaching days left the Quran and Tajweed teachers
32: * start with each of them; and Sara, who gave Jana (13) her Tajweed trial,
```

### `apps/api/modules/Scheduling/database/seeders/DemoShiftsSeeder.php`

Lines: 41, 42, 43, 46

```text
41: 'mahmoud' => ['male', ['ar'], 'مصرية', ['Quran memorisation', 'Tajweed']],
42: 'nour' => ['female', ['ar', 'en'], 'مصرية', ['Quran memorisation', 'Tajweed']],
43: 'sara' => ['female', ['ar'], 'مصرية', ['Tajweed', 'Quran memorisation']],
46: 'mona' => ['female', ['ar', 'en'], 'شامية', ['Arabic', 'Quran memorisation']],
```

### `apps/api/modules/Scheduling/src/Contracts/AssessmentLessons.php` — contract

Lines: 8

```text
8: * Assessment lessons (an exam another module holds: the Quran's), booked
```

## API module SharedKernel (24 files)

### `apps/api/modules/SharedKernel/lang/ar/ai.php`

Lines: 8, 15

```text
8: 'recitation_check' => 'تصحيح التسميع',
15: 'recitation_check' => 'عندما يسلّم الطالب تسميعًا بصوته، يقارنه المساعد بالنص المطلوب ويعلّم الكلمات الناقصة أو الخاطئة للمعلّم فقط.',
```

### `apps/api/modules/SharedKernel/lang/ar/audit.php`

Lines: 195, 196, 198, 200, 205, 224, 251, 252, 255, 270, 278

```text
195: // Kept for entries written before the Quran module (now quran.daily_pages_saved).
196: 'hifz_daily_saved' => 'أصبح ورد المراجعة :pages صفحة في اليوم على الأكثر',
198: 'quran' => [
200: 'settings_saved' => 'تعديل إعدادات القرآن: :quran_fields',
205: 'plan_adjusted' => 'تعديل خطة قرآن: :quran_fields',
224: 'quran_fetched' => 'تنزيل نص القرآن من Tanzil (:verses آية)',
251: 'quran_fields' => [
252: 'hifz_daily_pages' => 'الورد اليومي', 'riwaya' => 'الرواية', 'mushaf' => 'المصحف', 'default_unit' => 'الوحدة الافتراضية',
255: 'auto_recitation_check' => 'التسميع الآلي', 'exams_enabled' => 'الاختبارات', 'examiner' => 'المختبِر',
270: 'helpers' => ['practice_items' => 'اقتراح التدريبات', 'report_draft' => 'تقرير من رسالة صوتية', 'recitation_check' => 'تصحيح التسميع', 'digest_wording' => 'صياغة الرسالة الأسبوعية'…
278: 'capability' => ['practice_items' => 'اقتراح تدريبات للدرس', 'report_draft' => 'تقرير الحصة من رسالة صوتية', 'recitation_check' => 'تصحيح التسميع', 'digest_wording' => 'صياغة رسالة…
```

### `apps/api/modules/SharedKernel/lang/ar/chrome.php`

Lines: 9

```text
9: 'quran' => 'القرآن',
```

### `apps/api/modules/SharedKernel/lang/ar/plans.php`

Lines: 12, 30

```text
12: 'quran' => 'القرآن',
30: 'quran' => 'برامج الحفظ والمراجعة، والمصحف المشترك في الحصة، والاختبارات والشهادات.',
```

### `apps/api/modules/SharedKernel/lang/en/ai.php`

Lines: 8, 15

```text
8: 'recitation_check' => 'Recitation check',
15: 'recitation_check' => 'When a student hands in a recitation, the helper compares it with the expected text and marks missing or wrong words, for the teacher only.',
```

### `apps/api/modules/SharedKernel/lang/en/audit.php`

Lines: 195, 196, 198, 199, 200, 201, 202, 203, 204, 205, 206, 207, 208, 209, 210, 211, 224, 249, 251, 252, 255, 270, 278

```text
195: // Kept for entries written before the Quran module (now quran.daily_pages_saved).
196: 'hifz_daily_saved' => 'The daily hifz review is now :pages pages at most',
198: 'quran' => [
199: 'daily_pages_saved' => 'The daily hifz review is now :pages pages at most',
200: 'settings_saved' => 'Quran settings changed: :quran_fields',
201: 'program_saved' => 'Quran program :name saved',
202: 'program_archived' => 'Quran program :name archived',
203: 'program_restored' => 'Quran program :name brought back',
204: 'plan_started' => 'A Quran plan started on :program',
205: 'plan_adjusted' => 'A Quran plan changed: :quran_fields',
206: 'exam_suggested' => 'A Quran exam suggested (:stop_kind :stop_number)',
207: 'exam_booked' => 'A Quran exam booked (:stop_kind :stop_number)',
… 11 more lines
```

### `apps/api/modules/SharedKernel/lang/en/chrome.php`

Lines: 9

```text
9: 'quran' => 'The Quran',
```

### `apps/api/modules/SharedKernel/lang/en/plans.php`

Lines: 12, 30

```text
12: 'quran' => 'The Quran',
30: 'quran' => 'Memorisation and review programmes, the shared mushaf in lessons, exams and certificates.',
```

### `apps/api/modules/SharedKernel/src/Ai/AiFeature.php`

Lines: 14, 21, 27

```text
14: case RecitationCheck = 'recitation_check';
21: return $this !== self::RecitationCheck;
27: return $this === self::ReportDraft || $this === self::RecitationCheck;
```

### `apps/api/modules/SharedKernel/src/Ai/ExpectedText.php` — contract

Lines: 7, 8

```text
7: * Quran's, by surah and number) or one run of words, each with its words in
8: * order. A recitation engine compares what it hears with this; speech to
```

### `apps/api/modules/SharedKernel/src/Ai/RecitationEngine.php` — contract

Lines: 6, 7, 10, 13, 15

```text
6: * Hears a recitation and says, word by word, how it went against the text it
7: * was meant to be (RecitationResult). The recording is only read: never
10: * the words up here (SpeechRecitation); an engine that hears letters and
13: interface RecitationEngine
15: public function check(AiFeature|string $capability, AudioClip $clip, ExpectedText $expected): RecitationResult;
```

### `apps/api/modules/SharedKernel/src/Ai/RecitationResult.php` — contract

Lines: 13

```text
13: final readonly class RecitationResult
```

### `apps/api/modules/SharedKernel/src/Ai/SpeechRecitation.php` — contract

Lines: 8, 9, 11, 13, 17, 40

```text
8: * The default recitation engine: speech to text hears the recording (told
9: * only the language, never the text, so it cannot correct the reciter), and
11: * no rules of recitation.
13: final class SpeechRecitation implements RecitationEngine
17: public function check(AiFeature|string $capability, AudioClip $clip, ExpectedText $expected): RecitationResult
40: return new RecitationResult($verses, $lined['extra'], $heard->text, $heard->seconds, 'words:'.$heard->model);
```

### `apps/api/modules/SharedKernel/src/Authorization/Ability.php` — contract

Lines: 71, 72, 73, 74, 75, 85

```text
71: // The Quran module (docs/architecture/02, section 26): its settings and programs, teaching it, examining, the board.
72: case ManageQuran = 'quran.manage';
73: case TeachQuran = 'quran.teach';
74: case ExamineQuran = 'quran.examine';
75: case ViewQuranBoard = 'quran.board';
85: self::ManageQuran, self::TeachQuran, self::ExamineQuran, self::ViewQuranBoard => Feature::Quran,
```

### `apps/api/modules/SharedKernel/src/Filament/NavGroup.php`

Lines: 25, 43

```text
25: case Quran = 'quran';
43: self::Quran => Heroicon::OutlinedBookOpen,
```

### `apps/api/modules/SharedKernel/src/Plans/Feature.php` — contract

Lines: 25

```text
25: case Quran = 'quran';
```

### `apps/api/modules/SharedKernel/src/Providers/SharedKernelServiceProvider.php`

Lines: 27, 28, 48, 49, 57, 58, 98, 99, 100, 101, 102

```text
27: use Modules\SharedKernel\Ai\RecitationEngine;
28: use Modules\SharedKernel\Ai\SpeechRecitation;
48: use Modules\SharedKernel\Quran\LessonQuran;
49: use Modules\SharedKernel\Quran\NoLessonQuran;
57: use Modules\SharedKernel\Text\NoQuranSource;
58: use Modules\SharedKernel\Text\QuranSource;
98: $this->app->bindIf(RecitationEngine::class, SpeechRecitation::class);
99: // The Quran's text: none until the Quran module binds its copy.
100: $this->app->singletonIf(QuranSource::class, NoQuranSource::class);
101: // Nothing of the Quran beside a lesson until the Quran module binds its own.
102: $this->app->bindIf(LessonQuran::class, NoLessonQuran::class);
```

### `apps/api/modules/SharedKernel/src/Quran/LessonQuran.php` — contract

Lines: 3, 8, 10, 11, 14

```text
3: namespace Modules\SharedKernel\Quran;
8: * The Quran beside a lesson's room (docs/architecture/02, section 26): what
10: * lesson, drawn by the Quran module (which binds this) while the academy's
11: * plan has the Quran. Default: nothing (NoLessonQuran), and the page is a
14: interface LessonQuran
```

### `apps/api/modules/SharedKernel/src/Quran/NoLessonQuran.php` — contract

Lines: 3, 7, 8

```text
3: namespace Modules\SharedKernel\Quran;
7: /** No Quran beside any lesson: the module is not there, or the academy's plan leaves it out. */
8: final class NoLessonQuran implements LessonQuran
```

### `apps/api/modules/SharedKernel/src/Text/ArabicText.php` — contract

Lines: 10, 12, 13, 21

```text
10: * changed where it is kept (the Quran's least of all); this works on copies.
12: * The same rules as tools/course/listen.mjs, with the Quran's own marks.
13: * The Quran is compared in its plain spelling (Tanzil's simple text), as
21: /** Marks that do not change the letters: harakat, tanwin, shadda, sukun, dagger alef, Quranic signs, tatweel. */
```

### `apps/api/modules/SharedKernel/src/Text/NoQuranSource.php` — contract

Lines: 5, 6, 15

```text
5: /** No module keeps the Quran's text: nothing to show or fetch. */
6: final class NoQuranSource implements QuranSource
15: throw new QuranFetchFailed('No module keeps the Quran\'s text.');
```

### `apps/api/modules/SharedKernel/src/Text/QuranFetchFailed.php` — contract

Lines: 7, 8

```text
7: /** The Quran's files were not fetched or did not pass their checks; the message says why, in the reader's words. */
8: final class QuranFetchFailed extends RuntimeException {}
```

### `apps/api/modules/SharedKernel/src/Text/QuranSource.php` — contract

Lines: 6, 10, 26

```text
6: * Where the platform's copy of the Quran comes from (the Quran module binds it:
10: interface QuranSource
26: * @throws QuranFetchFailed with the reason in the reader's words
```

### `apps/api/modules/SharedKernel/src/Text/WordAlignment.php` — contract

Lines: 16, 27

```text
16: * one extra word and a recitation stopped early leaves the rest missing.
27: /** Words heard at most: more than this is not a recitation of a passage this size. */
```

## API module Site (1 files)

### `apps/api/modules/Site/database/seeders/DemoSiteSeeder.php`

Lines: 14, 22, 25, 26, 35, 44

```text
14: * hours, and "help me choose" starts with Quran memorisation. Once: a page
22: $quran = Subject::query()->where('name_en', 'Quran memorisation')->value('id');
25: if ($existing->updated_by === null && $existing->default_trial_subject_id === null && $quran !== null) {
26: $existing->forceFill(['default_trial_subject_id' => $quran])->save();
35: 'quote_en' => 'Yousef looks forward to his Quran lesson now, and the report after each one tells me he is on track.'],
44: 'trial_booking' => 'family', 'response_hours' => 4, 'default_trial_subject_id' => $quran]);
```

## API tests (mixed: other subjects with Quran parts) (115 files)

### `apps/api/tests/Arch/AiGatewayTest.php`

Lines: 30

```text
30: ->expect(['Modules\Curriculum', 'Modules\Learning', 'Modules\Quran', 'Modules\Games', 'Modules\Crm', 'Modules\Support', 'Modules\Messaging', 'App'])
```

### `apps/api/tests/Arch/ModuleBoundariesTest.php`

Lines: 9, 83, 275, 276, 290, 292, 294, 295, 296, 347, 383, 389, 391

```text
9: const MODULES_ABOVE_KERNEL = ['Modules\Platform', 'Modules\Identity', 'Modules\Communication', 'Modules\Catalog', 'Modules\People', 'Modules\Curriculum', 'Modules\Credits', 'Module…
83: ->expect(['Modules\People', 'Modules\Learning', 'Modules\Billing', 'Modules\Scheduling', 'Modules\Crm', 'Modules\Evaluation', 'Modules\Payroll', 'Modules\Import', 'Modules\Support'…
275: arch('the Quran sits on top: learning, lessons, courses, people, the catalog, the classroom, messages and branding through their contracts and the tables it reads, and nothing depe…
276: ->expect('Modules\Quran')
290: ->ignoring('Modules\Quran\Database')
292: ->not->toUse('Modules\Quran');
294: arch('the Quran\'s rules are pure: the hifz map\'s spaced repetition, programs, portions and grades from dates, numbers and verse ranges only')
295: ->expect('Modules\Quran\Domain')
296: ->toOnlyUse(['Carbon\CarbonImmutable', 'Modules\Quran\Domain', 'Modules\Quran\Contracts\DTOs\VerseRange', 'InvalidArgumentException']);
347: ->expect(['Modules\Identity\Privacy', 'Modules\People\Privacy', 'Modules\Communication\Privacy', 'Modules\Learning\Privacy', 'Modules\Scheduling\Privacy', 'Modules\Enrollment\Priva…
383: 'Modules\Quran\Models', 'Modules\Quran\Actions',
389: 'Modules\Credits\Actions', 'Modules\Enrollment\Actions', 'Modules\Billing\Actions', 'Modules\Curriculum\Actions', 'Modules\Learning\Actions', 'Modules\Communication\Actions', 'Modu…
… 1 more lines
```

### `apps/api/tests/Arch/NavGroupTest.php`

Lines: 42, 43, 44, 45, 46, 47, 48, 87, 88

```text
42: use Modules\Quran\Filament\Pages\HifzOverview;
43: use Modules\Quran\Filament\Pages\QuranCertificates;
44: use Modules\Quran\Filament\Pages\QuranExams;
45: use Modules\Quran\Filament\Pages\QuranHomePage;
46: use Modules\Quran\Filament\Pages\QuranPrograms;
47: use Modules\Quran\Filament\Pages\QuranSettingsPage;
48: use Modules\Quran\Filament\Pages\QuranStudents;
87: 'Quran' => [QuranHomePage::class, QuranStudents::class, HifzOverview::class, QuranPrograms::class,
88: QuranExams::class, QuranCertificates::class, QuranSettingsPage::class],
```

### `apps/api/tests/Feature/Announcements/AnnouncementsTest.php`

Lines: 38, 39, 77, 79, 130, 145, 281, 288, 295, 296

```text
38: * Huda with Ziad (an adult whose Quran course ended); a guardian whose
39: * account is off and an erased student. Omar learns Quran (running), Lina
77: $this->quran = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
79: foreach ([[$this->omar, $this->quran, 'active'], [$this->lina, $this->quran, 'paused'], [$this->adam, $this->quran, 'active'], [$this->ziad, $this->quran, 'ended'], [$this->yousef,…
130: ->and(reached(Audience::of('subject', null, $this->quran)))->toBe(['Lina', 'Omar', 'Sara', 'Tom'])
145: $a = announce($this->owner, Audience::of('subject', null, $this->quran), ['push'], 'Eid holiday', "Closed Tuesday to Thursday.\n\nLessons are back on Friday.");
281: ->fillForm(['audience' => 'subject', 'subject_id' => $this->quran])
288: $page->fillForm(['title' => 'Quran exam', 'body' => "On Sunday.\nBring your mushaf.", 'channels' => ['email']])
295: expect([$a->audience, $a->subject_id, $a->channels, $a->recipients_count, $a->sent_by])->toBe(['subject', $this->quran, ['email'], 4, $this->admin->id]);
296: $page->assertSee('Quran exam')->assertSee('Amr')->assertSee('4 announcements left today');
```

### `apps/api/tests/Feature/Api/CourseStatusApiTest.php`

Lines: 63, 83

```text
63: expect($lessons->json('notices.0'))->toBe('Quran is paused until Saturday 24 October.')
83: expect($lessons->json('notices'))->toContain('Quran has ended.')
```

### `apps/api/tests/Feature/Api/JourneyApiTest.php`

Lines: 13, 15, 26

```text
13: use Tests\Support\QuranProgram;
15: uses(EnrolledStudent::class, QuranProgram::class);
26: app(EnrollmentApi::class)->attachCurriculum($this->booked->enrollmentId, $this->publishQuranProgram($this->quran)->id);
```

### `apps/api/tests/Feature/Billing/AutoRenewTest.php`

Lines: 279

```text
279: $second = app(EnrollStudent::class)->handle($batch, $sibling->id, $this->quran, new EnrollmentTerms($plan->id, $this->payer->id, PriceRegion::query()->sole()->id), $this->admin->id…
```

### `apps/api/tests/Feature/Billing/CollectionTimelineTest.php`

Lines: 40

```text
40: * where the paying guardian lives); an adult Quran student's first block
```

### `apps/api/tests/Feature/Billing/DiscountsTest.php`

Lines: 48, 84

```text
48: $this->quran = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
84: return app(EnrollStudent::class)->handle($batch, $student, $t->quran, new EnrollmentTerms($t->plan->id, $t->guardian->id, $t->gulf->id, $coupon), $t->scheduler->id);
```

### `apps/api/tests/Feature/Billing/EndedCourseBillingTest.php`

Lines: 45, 104, 105, 129, 148, 151, 152, 155, 159, 161, 165, 168, 170, 177, 178, 208, 209

```text
45: $this->quran = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
104: $ziad = endedEnrol(0, $this->quran, hour: 16);
105: $maryam = endedEnrol(1, $this->quran, hour: 17);
129: $ziad = endedEnrol(0, $this->quran);
148: $quran = endedEnrol(0, $this->quran, $this->package->id, hour: 16);
151: expect(app(EndEnrollment::class)->preview($quran->enrollmentId, '2026-10-05')['billing']->outcome)->toBe('shared');
152: $done = app(EndEnrollment::class)->handle($quran->enrollmentId, '2026-10-05', 'Quran elsewhere', $this->scheduler->id);
155: ->and(Invoice::query()->find($quran->invoice->id)->status)->toBe('issued')
159: endedPay($quran->invoice->id);
161: ->and(Enrollment::query()->find($quran->enrollmentId)->status)->toBe(EnrollmentStatus::Ended)
165: ->and(app(SiblingRank::class)->of(endedSubscription($quran)->billing_account_id, $this->kids[0]->id))->toBe(1);
168: $renewal = app(IssueRenewal::class)->handle(endedSubscription($quran)->refresh());
… 5 more lines
```

### `apps/api/tests/Feature/Billing/EnrollmentLoopTest.php`

Lines: 44, 78

```text
44: $this->quran = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
78: return app(EnrollStudent::class)->handle($batch, $t->student->id, $t->quran, new EnrollmentTerms($planId ?? $t->plan->id, $t->guardian->id, $t->gulf->id), $t->scheduler->id);
```

### `apps/api/tests/Feature/Billing/FamilyBillingTest.php`

Lines: 41, 112, 113, 128, 149, 150, 167, 168, 185, 186, 205, 206, 217, 228, 234, 238, 239, 240, 247, 249, 252, 263, 267, 268, 274, 285, 291, 292, 298, 308, 314

```text
41: $this->quran = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
112: $ziad = familyEnrol(0, $this->quran, hour: 16);
113: $maryam = familyEnrol(1, $this->quran, hour: 17);
128: ->and($blocks->pluck('description_en')->all())->toBe(['Maryam · Quran — 8 sessions (block 2)', 'Ziad · Quran — 8 sessions (block 2)'])
149: $ziad = familyEnrol(0, $this->quran, hour: 16);
150: $maryam = familyEnrol(1, $this->quran, hour: 17);
167: $ziad = familyEnrol(0, $this->quran, hour: 16);
168: $maryam = familyEnrol(1, $this->quran, hour: 17);
185: $ziad = familyEnrol(0, $this->quran, hour: 16);
186: $maryam = familyEnrol(1, $this->quran, hour: 17);
205: $ziad = familyEnrol(0, $this->quran, hour: 16);
206: $maryam = familyEnrol(1, $this->quran, hour: 17);
… 19 more lines
```

### `apps/api/tests/Feature/Billing/GroupPlanScreenTest.php`

Lines: 83, 84, 87

```text
83: $quran = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
84: $enrollment = app(EnrollmentApi::class)->create(new NewEnrollment($student->id, $quran, $teacher->id, CarbonImmutable::now()));
87: app(BillingApi::class)->subscribe(new NewSubscription($enrollment, $student->id, $account, $group->id, $student->id, $this->gulf->id, 'قرآن', 'Quran'));
```

### `apps/api/tests/Feature/Billing/InvoiceWritingTest.php`

Lines: 39, 58, 62

```text
39: $this->quran = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
58: $enrollment = app(EnrollmentApi::class)->create(new NewEnrollment($student->id, $t->quran, $t->teacher->id, CarbonImmutable::parse('2026-10-06')));
62: return new NewSubscription($enrollment, $student->id, $account, $planId ?? $t->plan->id, $payerId ?? $t->guardian->id, $regionId ?? $t->gulf->id, 'قرآن', 'Quran', $t->admin->id);
```

### `apps/api/tests/Feature/Billing/ManualTransferTest.php`

Lines: 46, 54, 73, 164, 184

```text
46: * (Quran) and Maryam (Arabic), each on 8 lessons for 400 SAR (15% VAT
54: $this->quran = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
73: $this->ziad = transferEnrol(0, $this->quran, 16);
164: ->and($rows('subjects'))->toEqualCanonicalizing([$this->quran => 80000, $this->arabic => 80000])
184: $own = app(IssueBlockInvoice::class)->handle(transferCourse($this->ziad), 2, 'قرآن', 'Quran', $this->admin->id);
```

### `apps/api/tests/Feature/Billing/MoneyConcurrencyTest.php`

Lines: 204, 207

```text
204: $enrollment = app(EnrollmentApi::class)->create(new NewEnrollment($student->id, $this->quran, $this->teacher->id, CarbonImmutable::parse('2026-10-06')));
207: app(SubscribeEnrollment::class)->handle(new NewSubscription($enrollment, $student->id, $credit, Plan::query()->value('id'), $guardian->id, PriceRegion::query()->value('id'), 'قرآن'…
```

### `apps/api/tests/Feature/Billing/PlanAndCouponScreensTest.php`

Lines: 35, 49, 52

```text
35: $this->quran = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
49: $enrollment = app(EnrollmentApi::class)->create(new NewEnrollment($student->id, $t->quran, $t->teacher->id, CarbonImmutable::now()));
52: app(BillingApi::class)->subscribe(new NewSubscription($enrollment, $student->id, $account, $plan->id, $student->id, $t->gulf->id, 'قرآن', 'Quran', couponCode: $coupon));
```

### `apps/api/tests/Feature/Billing/RevenueForecastBatchTest.php`

Lines: 32, 67

```text
32: $this->quran = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
67: $booked = app(EnrollStudent::class)->handle($batch, $student, $t->quran, new EnrollmentTerms($t->plan->id, $t->guardian->id, $t->gulf->id, $coupon), $t->scheduler->id);
```

### `apps/api/tests/Feature/Billing/RevenueTest.php`

Lines: 37, 98, 139, 161, 174, 176, 194, 196, 223, 229, 231, 256, 300, 317

```text
37: $this->quran = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
98: $ziad = revenueEnrol(0, $this->quran, hour: 16);
139: $ziad = revenueEnrol(0, $this->quran, hour: 16);
161: ->and($rows('subjects'))->toBe([$this->quran => 40000 + 20000, $this->arabic => 36000 + 18000])
174: $ziad = revenueEnrol(0, $this->quran, hour: 16);
176: $yousef = revenueEnrol(2, $this->quran, hour: 18, regionId: $this->usa->id);
194: $ziad = revenueEnrol(0, $this->quran, hour: 16, regionId: $kuwait->id);
196: $yousef = revenueEnrol(2, $this->quran, hour: 18);
223: expect($kwd)->toEqualCanonicalizing([$this->quran => 12345 + 4093, $this->arabic => 11110 + 3684])
229: $ziad = revenueEnrol(0, $this->quran, hour: 16);
231: $yousef = revenueEnrol(2, $this->quran, hour: 18);
256: $ziad = revenueEnrol(0, $this->quran, hour: 16);
… 2 more lines
```

### `apps/api/tests/Feature/Billing/ZatcaTest.php`

Lines: 60, 81, 87, 106

```text
60: $invoice = app(IssueBlockInvoice::class)->handle($this->subscription, 2, 'قرآن', 'Quran');
81: $usd = app(IssueBlockInvoice::class)->handle($this->subscription->fresh(), 2, 'قرآن', 'Quran');
87: $invoice = app(IssueBlockInvoice::class)->handle($this->subscription, 2, 'قرآن', 'Quran');
106: $invoice = app(IssueBlockInvoice::class)->handle($this->subscription, 2, 'قرآن', 'Quran');
```

### `apps/api/tests/Feature/Classroom/ClassroomJoinTest.php`

Lines: 41

```text
41: $this->childLesson = app(ScheduleSession::class)->handle(new NewSession($this->teacher->id, $this->child->id, $this->quran, CarbonImmutable::parse('2026-10-06 16:00 UTC'), 30, 'Afr…
```

### `apps/api/tests/Feature/Classroom/ClassroomTest.php`

Lines: 181

```text
181: expect($teacher->getContent())->toContain("dispatchEvent(new CustomEvent('lms:room'")   // the mushaf hears the room
```

### `apps/api/tests/Feature/Communication/NotificationsTest.php`

Lines: 42, 55, 67, 119

```text
42: channels: ['push', 'whatsapp', 'email'], sample: ['subject' => 'Quran', 'when' => 'Tue 18:00', 'status' => 'moved'],
55: 'subject' => 'Quran', 'when' => CarbonImmutable::parse('2026-10-06 15:00', 'UTC'), 'status' => new Translatable('test.moved'),
67: ->and($tom->body)->toBe('Quran moves to Tue 6 Oct · 16:00 (moved).')
119: 'subject' => 'Quran', 'when' => CarbonImmutable::parse('2026-10-06 15:00', 'UTC'), 'status' => 'moved',
```

### `apps/api/tests/Feature/Communication/WiredNotificationsTest.php`

Lines: 25, 27, 60, 69

```text
25: use Tests\Support\QuranProgram;
27: uses(EnrolledStudent::class, QuranProgram::class);
60: app(EnrollmentApi::class)->attachCurriculum($this->booked->enrollmentId, $this->publishQuranProgram($this->quran)->id);
69: 'homework' => ['title' => 'Recite lesson 1', 'accepts' => 'text'],
```

### `apps/api/tests/Feature/Crm/CrmTest.php`

Lines: 45, 61, 70, 146, 225, 245, 246, 260

```text
45: * teacher and a Riyadh teacher teach Quran on Tuesdays and Saturdays
61: 'for_child' => true, 'learner_name' => 'Yousef', 'learner_birth_year' => 2017, 'subject_id' => test()->quran,
70: return app(ConfirmBooking::class)->trial($batch, $learnerId, test()->quran, test()->admin->id);
146: 'mode' => 'trial', 'student' => $learner, 'subject' => $this->quran, 'tz' => 'Asia/Riyadh',
225: $booked = app(EnrollStudent::class)->handle($batch, $learner, $this->quran, new EnrollmentTerms(Plan::query()->value('id'), $lead->refresh()->contact_id, PriceRegion::query()->valu…
245: $trial = app(FindTeachersQuery::class)->run(new TeacherSearch($this->quran, $pref, forTrial: true));
246: $series = app(FindTeachersQuery::class)->run(new TeacherSearch($this->quran, $pref));
260: 'for_child' => false, 'subject_id' => $this->quran, 'preferred_days' => [6], 'preferred_from' => 18, 'preferred_to' => 20, 'source' => 'instagram',
```

### `apps/api/tests/Feature/Crm/NextTrialTest.php`

Lines: 37, 72, 76

```text
37: * teacher (a man, 18:00–22:00 Riyadh) teach Quran on Tuesdays and Saturdays.
72: 'for_child' => true, 'learner_name' => 'Yara', 'learner_birth_year' => 2017, 'subject_id' => test()->quran, 'source' => 'website',
76: $session = app(ConfirmBooking::class)->trial($batch, $learner, test()->quran, test()->admin->id);
```

### `apps/api/tests/Feature/Crm/OwnTrialTest.php`

Lines: 47, 100, 108, 214, 233, 372, 374, 375, 376, 438, 498

```text
47: * teaches Quran on Tuesdays and Saturdays 17:00–21:00 and has a lesson at
100: 'subject_id' => test()->quran, 'for_child' => true, 'child_name' => 'Yara', 'child_birth_year' => 2017,
108: $answer = noor('GET', 'site/trial-slots?'.http_build_query($query + ['subject_id' => test()->quran, 'timezone' => 'Asia/Riyadh', 'birth_year' => 2017]))->assertOk();
214: noor('GET', 'site/trial-slots?subject_id='.$this->quran)->assertNotFound();
233: noor('GET', 'site/trials/pick/'.$m[1])->assertOk()->assertJsonPath('data.child_name', 'Yara')->assertJsonPath('data.subject.id', $this->quran);
372: SiteSettings::query()->update(['default_trial_subject_id' => $this->quran]);
374: expect(JoinRequest::query()->where('phone', '+966500000008')->value('subject_id'))->toBe($this->quran)
375: ->and(Lead::query()->where('phone_e164', '+966500000008')->value('subject_id'))->toBe($this->quran);
376: noor('GET', 'site')->assertOk()->assertJsonPath('data.trials', ['booking' => 'family', 'response_hours' => 4, 'notice_hours' => 3, 'help_choose_subject' => true, 'help_choose_subje…
438: noor('GET', 'site/trial-slots?'.http_build_query(['subject_id' => $this->quran, 'timezone' => 'Europe/London', 'from' => '2026-10-20', 'birth_year' => 2017]))->json('data'));
498: noor('GET', 'site/trial-slots?subject_id='.$this->quran)->assertNotFound();
```

### `apps/api/tests/Feature/Crm/TrialReportTest.php`

Lines: 58, 102, 106, 147, 191

```text
58: * Cairo teacher (a woman) and a Riyadh teacher (a man) teach Quran on
102: 'for_child' => true, 'learner_name' => 'Yara Salem', 'learner_birth_year' => 2017, 'subject_id' => test()->quran, 'source' => 'website',
106: $session = app(ConfirmBooking::class)->trial($batch, $learner, test()->quran, test()->admin->id);
147: return app(EnrollStudent::class)->handle($batch, $trial->lead->learner_id, test()->quran,
191: ->and($report['subject']['name'])->toBe('Quran')
```

### `apps/api/tests/Feature/Curriculum/CurriculumOutlineTest.php`

Lines: 47, 55, 113, 114, 120, 169, 173

```text
47: * files. (The Quran's outlines and tracks are the Quran module's.)
55: $this->subject = app(CatalogApi::class)->createSubject('تحفيظ القرآن', 'Quran');
113: $rows[] = ['kind' => 'level', 'depth' => 0, 'title_ar' => 'قرآن', 'title_en' => 'Quran'];
114: $rows[] = ['kind' => 'lesson', 'depth' => 1, 'title_ar' => 'سورة 112', 'title_en' => 'Surah 112', 'quran' => ['surah' => 112, 'from' => 1, 'to' => 3]];   // no longer a curriculum'…
120: 'level Quran', '> lesson Surah 112',
169: expect($model->prompt->user)->toContain('Subject: Quran')->toContain('children aged 6 to 9')->toContain('about 10')->toContain('قراءة الحروف')
173: ->and($model->prompt->system)->not->toContain('Quran');
```

### `apps/api/tests/Feature/Curriculum/LessonMaterialsTest.php`

Lines: 28, 31, 36, 66, 67, 73, 82, 200, 203, 205

```text
28: use Tests\Support\QuranProgram;
31: uses(EnrolledStudent::class, QuranProgram::class);
36: $this->program = $this->publishQuranProgram($this->quran);
66: $audio = lrAdd($this->first, ['kind' => 'file', 'audience' => 'all'], UploadedFile::fake()->create('fatiha-recitation.mp3', 900, 'audio/mpeg'));
67: $link = lrAdd($this->first, ['kind' => 'link', 'title_en' => 'Recitation video', 'url' => 'https://www.youtube.com/watch?v=abc']);
73: ->and([$audio->title_ar, $audio->title_en])->toBe(['fatiha-recitation', 'fatiha-recitation']) // no name: the file's
82: app(UpdateNodeResource::class)->handle($link, ['title_ar' => 'فيديو التلاوة', 'title_en' => 'Recitation', 'audience' => 'teachers', 'url' => 'https://youtu.be/xyz']);
200: ->callAction('addMaterial', ['url' => 'https://quran.com/1', 'title_ar' => 'الفاتحة على quran.com', 'audience' => 'all'], ['node' => $this->first->id, 'kind' => 'link'])
203: ->assertSee('الفاتحة على quran.com');
205: expect(NodeResource::query()->where('node_id', $this->first->id)->value('url'))->toBe('https://quran.com/1');
```

### `apps/api/tests/Feature/Curriculum/LessonTextTest.php`

Lines: 27, 29, 35, 36, 42, 94, 95, 96

```text
27: use Tests\Support\QuranProgram;
29: uses(QuranProgram::class);
35: * and saves nothing until a person does. (A passage of the Quran is the
36: * Quran module's, never a curriculum's text.)
42: $this->program = $this->publishQuranProgram(app(CatalogApi::class)->createSubject('قرآن', 'Quran'));
94: expect(textRefusal(fn () => setText($this->lesson, ['kind' => 'quran', 'surah' => 2, 'from' => 1, 'to' => 2])))->toBe('text_source')
95: ->and(TextSource::fromArray(['kind' => 'quran', 'surah' => 2, 'from' => 1, 'to' => 2]))->toBeNull()
96: ->and(fn () => DB::table('curriculum_nodes')->where('id', $this->lesson->id)->update(['text_source' => json_encode(['kind' => 'quran', 'surah' => 2, 'from' => 1, 'to' => 2])]))
```

### `apps/api/tests/Feature/Curriculum/PracticeItemsTest.php`

Lines: 14, 17, 29

```text
14: use Tests\Support\QuranProgram;
17: uses(EnrolledStudent::class, QuranProgram::class, StarterGames::class);
29: $this->program = $this->publishQuranProgram($this->quran);
```

### `apps/api/tests/Feature/Demo/DemoAutoRenewTest.php`

Lines: 19, 29, 30

```text
19: use Modules\Quran\Texts\QuranText;
29: 'features' => ['crm', 'online_payments', 'import', 'custom_branding', 'payroll', 'quran', 'groups', 'curriculum', 'games', 'messaging', 'announcements', 'support', 'evaluation', 's…
30: app()->instance(QuranText::class, new QuranText(base_path('tests/Fixtures/none')));
```

### `apps/api/tests/Feature/Demo/DemoCatchUpTest.php`

Lines: 13, 14, 15, 20, 23, 24, 26, 30, 33, 41, 58, 59, 62, 65, 66, 67, 77, 84, 86, 87, 97, 98, 99, 100, 101, 102, 104, 108, 121, 122

```text
13: use Modules\Quran\Contracts\DTOs\VerseRange;
14: use Modules\Quran\Contracts\QuranApi;
15: use Modules\Quran\Texts\QuranText;
20: * A server's demo was made before its lessons could read the Quran (the text
23: * the Juz' Amma lessons read their surahs, each Quran learner's last lesson
24: * has a few marked words, the reports already handed in make their hifz
26: * text here is made up in Tanzil's shape, never the Quran.
30: function catchUpQuranFiles(string $dir): void
33: $xml = "<?xml version=\"1.0\" encoding=\"utf-8\" ?>\n<quran>\n<suras alias=\"chapters\">\n";
41: $text .= "\n#  A file in the shape of Tanzil's text, with made-up words: not the Quran.\n#  Tanzil Quran Text (Simple, Version Test)\n";
58: File::put($dir.'/'.QuranText::TEXT_FILE, $text);
59: File::put($dir.'/'.QuranText::DATA_FILE, $xml."</suras>\n".$place('juzs', 'juz', 30).$place('pages', 'page', 604)."</quran>\n");
… 18 more lines
```

### `apps/api/tests/Feature/Demo/DemoCollectionTest.php`

Lines: 14, 25, 26

```text
14: use Modules\Quran\Texts\QuranText;
25: 'features' => ['crm', 'online_payments', 'import', 'custom_branding', 'payroll', 'quran', 'groups', 'curriculum', 'games', 'messaging', 'announcements', 'support', 'evaluation', 's…
26: app()->instance(QuranText::class, new QuranText(base_path('tests/Fixtures/none')));
```

### `apps/api/tests/Feature/Demo/DemoGroupsTest.php`

Lines: 21, 57, 66, 74

```text
21: * children's group (a child sees how many are with her) and her Quran group
57: 'features' => ['crm', 'online_payments', 'import', 'custom_branding', 'payroll', 'quran', 'groups', 'curriculum', 'games', 'messaging', 'announcements', 'support', 'evaluation', 's…
66: [$khaled, $monaKids, $monaQuran] = [$demo['groups'][0], ...collect($demo['groups'])->where('teacher', 'mona@demo.test')->sortBy('status', SORT_STRING, true)->values()->all()];
74: ->and($monaQuran)->toMatchArray(['status' => 'forming', 'capacity' => 6, 'min' => 4, 'members' => ['sama@demo.test'], 'held' => 0, 'ahead' => 0])
```

### `apps/api/tests/Feature/Demo/DemoSelfStartTest.php`

Lines: 13, 24, 26, 32, 33, 61, 68, 82, 96

```text
13: use Modules\Quran\Texts\QuranText;
24: * lesson that day, said with the time), the Quran and Tajweed teachers work
26: * her Tajweed trial, teaches middle school: Jana's mother can start the plans
32: 'features' => ['crm', 'online_payments', 'import', 'custom_branding', 'payroll', 'quran', 'groups', 'curriculum', 'games', 'messaging', 'announcements', 'support', 'evaluation', 's…
33: app()->instance(QuranText::class, new QuranText(base_path('tests/Fixtures/none')));
61: /** The weekdays (on Jana's mother's clock) on which a teacher can take Jana's Tajweed course on a 30-minute plan of so many lessons a week, and the suggested pattern. */
68: $slots = janaMother('family/start/slots?'.http_build_query(['learner_id' => $jana, 'subject_id' => DB::table('subjects')->where('name_en', 'Tajweed')->value('id'),
82: it('lets Jana\'s mother start Tajweed with Sara, two or three lessons a week', function () {
96: // The other Tajweed teachers too, past the holiday and Nour's leave.
```

### `apps/api/tests/Feature/Demo/DemoSetupTest.php`

Lines: 20

```text
20: 'features' => ['crm', 'online_payments', 'import', 'custom_branding', 'payroll', 'quran', 'groups', 'curriculum', 'games', 'messaging', 'announcements', 'support', 'evaluation', 's…
```

### `apps/api/tests/Feature/Deploy/LoadAcademySeederTest.php`

Lines: 36

```text
36: 'features' => ['crm', 'online_payments', 'import', 'custom_branding', 'payroll', 'quran', 'groups', 'curriculum', 'games', 'messaging', 'announcements', 'support', 'evaluation', 's…
```

### `apps/api/tests/Feature/Enrollment/EnrollmentTest.php`

Lines: 38, 62

```text
38: $this->enrol = fn (string $student) => app(EnrollmentApi::class)->create(new NewEnrollment($student, $this->quran, $this->teacher->id, CarbonImmutable::now()));
62: [(string) Str::uuid(), $theirs, $this->quran, $this->teacher->id, '2026-10-05'],
```

### `apps/api/tests/Feature/Games/GamesEdgesTest.php`

Lines: 42, 45, 59

```text
42: use Tests\Support\QuranProgram;
45: uses(EnrolledStudent::class, QuranProgram::class, StarterGames::class);
59: app(EnrollmentApi::class)->attachCurriculum($this->booked->enrollmentId, $this->publishQuranProgram($this->quran)->id);
```

### `apps/api/tests/Feature/Games/GamesTest.php`

Lines: 47, 50, 64

```text
47: use Tests\Support\QuranProgram;
50: uses(EnrolledStudent::class, QuranProgram::class, StarterGames::class);
64: app(EnrollmentApi::class)->attachCurriculum($this->booked->enrollmentId, $this->publishQuranProgram($this->quran)->id);
```

### `apps/api/tests/Feature/Identity/OnboardCommandTest.php`

Lines: 31, 52, 57, 61, 70, 110

```text
31: $this->growth = SaasPlan::query()->create(['code' => 'growth', 'name_ar' => 'النمو', 'name_en' => 'Growth', 'features' => ['crm', 'quran', 'payroll']]);
52: 'plan' => 'growth', 'features_off' => ['quran'], 'hidden' => ['games', 'messaging', 'evaluation'],
57: it('opens an academy with its owner, its plan without the Quran, three areas hidden, and the welcome by email, never printing the link', function () {
61: ->and($out)->toContain('nibras.lms.test')->toContain('growth')->toContain('quran')
70: ->and($current->features_off)->toBe(['quran'])
110: 'a paid area hidden' => [['hidden' => ['quran']], 'Only optional modules'],
```

### `apps/api/tests/Feature/Import/ImportTest.php`

Lines: 33, 178, 283

```text
33: * CSV/Excel"). The fixture: academy "noor" on Cairo's clock, a Quran
178: ['مريم أحمد', '+447700900123', $teacherContact, 'Quran', '30 دقيقة', 'الاثنين 5 م، الخميس 5 م', 'الطالب', '1', '8 حصص'],
283: $csv = "name,email,mobile,gender,subjects\nSara Mahmoud,sara.m@example.com,01012345678,female,Quran\nNo Contact,,,male,Quran\n";
```

### `apps/api/tests/Feature/Learning/ChallengesTest.php`

Lines: 25, 27, 40

```text
25: use Tests\Support\QuranProgram;
27: uses(EnrolledStudent::class, QuranProgram::class);
40: app(EnrollmentApi::class)->attachCurriculum($this->booked->enrollmentId, $this->publishQuranProgram($this->quran)->id);
```

### `apps/api/tests/Feature/Learning/CurriculumTest.php`

Lines: 17, 19, 23, 60

```text
17: use Tests\Support\QuranProgram;
19: uses(QuranProgram::class);
23: $this->subject = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
60: $this->publishQuranProgram($this->subject);
```

### `apps/api/tests/Feature/Learning/GroupReportsTest.php`

Lines: 60, 62, 71, 76

```text
60: 'homework' => ['title' => 'Recite Al-Fil twice', 'due_days' => 3],
62: ['student_id' => $this->a->id, 'engagement' => 5, 'overall' => 4, 'notes_for_student' => 'Lovely tajweed.'],
71: ->and($after[$this->a->id]->overall)->toBe(4)->and($after[$this->a->id]->notes_for_student)->toBe('Lovely tajweed.')
76: ->and(Homework::query()->where('student_id', $this->b->id)->value('title'))->toBe('Recite Al-Fil twice');
```

### `apps/api/tests/Feature/Learning/HomeworkEdgesTest.php`

Lines: 25, 27, 42, 75, 91, 107

```text
25: use Tests\Support\QuranProgram;
27: uses(EnrolledStudent::class, QuranProgram::class);
42: app(EnrollmentApi::class)->attachCurriculum($this->booked->enrollmentId, $this->publishQuranProgram($this->quran)->id);
75: app(SubmitHomework::class)->handle($late, $this->student->id, null, UploadedFile::fake()->create('recitation.m4a', 300, 'audio/mp4'));
91: $v1 = app(SaveReportTemplate::class)->handle($this->quran, [
107: $v2 = app(SaveReportTemplate::class)->handle($this->quran, $fields, $this->admin->id);
```

### `apps/api/tests/Feature/Learning/JourneyEdgesTest.php`

Lines: 133, 145, 150, 170, 205, 210, 223, 233, 262, 394

```text
133: // The Quran course follows no program; English has only a draft.
145: expect($lesson)->toMatchArray(['enrollment_id' => $this->booked->enrollmentId, 'station_id' => null, 'island_id' => null, 'title' => 'Quran'])
150: [$programId, $short] = jeProgram($this->quran, 'Short', 1, 3);
170: [$programId, $lessons] = jeProgram($this->quran, 'Juz Amma', 2, 3);
205: [$programId, $quran] = jeProgram($this->quran, 'Quran', 4, 15);
210: foreach (array_slice($quran, 0, 4) as $id) {
223: 'engagement' => 4, 'overall' => 4, 'items' => [['node_id' => $quran[$n], 'outcome' => 'mastered', 'score' => 5]],
233: expect($missions)->toHaveCount(4)->and($missions->pluck('station_id')->all())->toBe(array_slice($quran, 0, 4));
262: expect($subjects)->toBe([['Quran'], ['Maths'], ['Science']]);
394: SQL, [$this->other->id, $this->quran]);
```

### `apps/api/tests/Feature/Learning/JourneyMapTest.php`

Lines: 32, 35, 51, 264

```text
32: use Tests\Support\QuranProgram;
35: uses(EnrolledStudent::class, QuranProgram::class, StarterGames::class);
51: app(EnrollmentApi::class)->attachCurriculum($this->booked->enrollmentId, $this->publishQuranProgram($this->quran)->id);
264: // The Quran academy's student sees nothing of it, and its levels are three islands in turn.
```

### `apps/api/tests/Feature/Learning/LearningApiTest.php`

Lines: 14, 17, 22, 63, 97

```text
14: use Tests\Support\QuranProgram;
17: uses(EnrolledStudent::class, QuranProgram::class);
22: $this->publishQuranProgram($this->quran);
63: 'homework' => ['title' => 'Recite the letters', 'accepts' => 'audio'],
97: 'homework' => ['title' => 'Recite the letters', 'accepts' => 'audio'],
```

### `apps/api/tests/Feature/Learning/ReportDraftTest.php`

Lines: 28, 31, 43, 47

```text
28: use Tests\Support\QuranProgram;
31: uses(EnrolledStudent::class, QuranProgram::class);
43: $this->publishQuranProgram($this->quran);
47: app(SaveReportTemplate::class)->handle($this->quran, [
```

### `apps/api/tests/Feature/Learning/ReportTemplatesTest.php`

Lines: 25, 28, 32, 38, 39, 43, 81, 88, 90, 95, 102, 105, 114, 127, 142, 158, 181, 220, 228, 238, 242, 250

```text
25: use Tests\Support\QuranProgram;
28: uses(EnrolledStudent::class, QuranProgram::class);
32: $this->publishQuranProgram($this->quran);
38: /** Pages memorised (a number), tajweed (a choice), a note for the academy only (text). */
39: function rtQuranQuestions(): array
43: ['label_ar' => 'التجويد', 'label_en' => 'Tajweed', 'type' => 'choice', 'options' => [
81: $v1 = $save->handle($this->quran, rtQuranQuestions(), $this->admin->id);
88: expect($save->handle($this->quran, $same, $this->admin->id)->id)->toBe($v1->id);
90: // Words changed, the tajweed choices reordered with one dropped and one added, the note now a yes/no.
95: $v2 = $save->handle($this->quran, $fields, $this->admin->id);
102: ->and(ReportTemplate::currentFor($this->quran)->id)->toBe($v2->id);
105: $v3 = $save->handle($this->quran, [$v2->fields[0], ['label_ar' => 'التركيز', 'type' => 'rating']], $this->admin->id);
… 10 more lines
```

### `apps/api/tests/Feature/Learning/ReportsAndProgressTest.php`

Lines: 28, 30, 34, 146, 149, 154, 162

```text
28: use Tests\Support\QuranProgram;
30: uses(EnrolledStudent::class, QuranProgram::class);
34: $this->publishQuranProgram($this->quran);
146: $report = handIn(closeLesson(0), [], ['homework' => ['title' => 'Recite lesson 1', 'accepts' => 'audio', 'due_days' => 2]]);
149: expect($homework->title)->toBe('Recite lesson 1')->and($homework->accepts)->toBe('audio')
154: $voice = UploadedFile::fake()->create('recitation.m4a', 300, 'audio/mp4');
162: app(ReviewHomework::class)->handle($homework, $this->teacher->id, 5, 'Beautiful tajweed');
```

### `apps/api/tests/Feature/Learning/WeeklyDigestTest.php`

Lines: 62, 238

```text
62: 'homework' => ['title' => 'Recite the surah', 'accepts' => 'audio', 'due_days' => 2],
238: $html = $this->get('http://noor.lms.test'.$page)->assertOk()->assertSee($this->first)->assertSee('Recite the surah')->getContent();
```

### `apps/api/tests/Feature/Panel/CourseStopScreensTest.php`

Lines: 120

```text
120: Livewire::test(FamilyLessons::class)->assertSee('Quran is paused until Saturday 24 October.')
```

### `apps/api/tests/Feature/Panel/FamilyAreaTest.php`

Lines: 29, 31, 117, 127, 134, 139, 171

```text
29: use Tests\Support\QuranProgram;
31: uses(EnrolledStudent::class, QuranProgram::class);
117: $program = $this->publishQuranProgram($this->quran);
127: Livewire::test(FamilyProgress::class)->assertSee('Quran')->assertSee('0%')->assertSee('Lesson 1');
134: 'title' => 'Recite Al-Fatiha', 'accepts' => 'any', 'due_at' => now()->addDays(2), 'status' => 'assigned',
139: ->assertSee('Recite Al-Fatiha')
171: Livewire::test(NextLessonsWidget::class)->assertSee('Quran')->assertSee(__('scheduling::family.tomorrow'));
```

### `apps/api/tests/Feature/Panel/JourneyScreensTest.php`

Lines: 45, 48, 62

```text
45: use Tests\Support\QuranProgram;
48: uses(EnrolledStudent::class, QuranProgram::class, StarterGames::class);
62: app(EnrollmentApi::class)->attachCurriculum($this->booked->enrollmentId, $this->publishQuranProgram($this->quran)->id);
```

### `apps/api/tests/Feature/Panel/LearningScreensTest.php`

Lines: 26, 28, 33, 86, 93, 110

```text
26: use Tests\Support\QuranProgram;
28: uses(EnrolledStudent::class, QuranProgram::class);
33: $this->program = $this->publishQuranProgram($this->quran);
86: ->set('data.homework.title', 'Recite lesson 1')->set('data.homework.accepts', 'audio')
93: ->and(Homework::query()->value('title'))->toBe('Recite lesson 1');
110: 'homework' => ['title' => 'Recite', 'accepts' => 'audio'],
```

### `apps/api/tests/Feature/Panel/MoneyScreensTest.php`

Lines: 27, 35

```text
27: $subject = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
35: $this->invoiceId = app(BillingApi::class)->subscribe(new NewSubscription($this->enrollmentId, $student->id, $account, $plan->id, $student->id, $region->id, 'قرآن', 'Quran'))->id;
```

### `apps/api/tests/Feature/Panel/StartHereTest.php`

Lines: 41, 144

```text
41: const SETUP_OPTIONAL = ['platform.modules', 'identity.team', 'site.page', 'quran.programs', 'curriculum.program', 'import.people'];
144: $subject = app(SaveSubject::class)->handle(null, 'قرآن', 'Quran');
```

### `apps/api/tests/Feature/Panel/StudentStagesTest.php`

Lines: 32, 34, 46

```text
32: use Tests\Support\QuranProgram;
34: uses(EnrolledStudent::class, QuranProgram::class);
46: app(EnrollmentApi::class)->attachCurriculum($this->booked->enrollmentId, $this->publishQuranProgram($this->quran)->id);
```

### `apps/api/tests/Feature/Panel/TeacherAreaTest.php`

Lines: 47

```text
47: Livewire::test(MyStudents::class)->assertSee($this->student->name)->assertSee('Quran');
```

### `apps/api/tests/Feature/Payroll/GroupPayTest.php`

Lines: 44, 46, 47, 48, 49

```text
44: $quran = new RateLine('quran', null, 'lesson', 12000);
46: expect(Pay::pick([$private, $group, $quran], 'quran', 'regular', 'group'))->toBe($group)
47: ->and(Pay::pick([$private, $group, $quran], 'quran', 'regular'))->toBe($quran)
48: ->and(Pay::pick([$private, $quran], 'quran', 'regular', 'group'))->toBe($quran)
49: ->and(Pay::pick([$group], 'quran', 'regular'))->toBeNull();
```

### `apps/api/tests/Feature/Payroll/PayrollTest.php`

Lines: 113, 118, 343, 389

```text
113: ['subject_id' => $this->quran, 'unit' => 'hour', 'amount' => '150'],
118: expect(payLines(teachForPay('2026-10-06')->id)->sole()->amount_minor)->toBe(7500)       // Quran beats "regular lessons"
343: ->and(array_slice($sheets['Lessons'][1], 1, 13))->toEqual(['2026-10-06', '18:00', $this->student->name, 'Quran', 'Regular', 'Taught', 30, 1, 120, 'hour', 60, 'EGP', ''])
389: ->callAction('create', ['name' => 'Gulf', 'currency' => 'SAR', 'is_default' => false, 'lines' => [['subject_id' => $this->quran, 'session_type' => 'trial', 'unit' => 'lesson', 'amo…
```

### `apps/api/tests/Feature/People/DirectoryTest.php`

Lines: 53, 55, 56, 57, 71, 75, 82, 84, 85, 88, 97, 109, 121, 122, 123, 126, 141, 157

```text
53: $this->quran = app(SaveSubject::class)->handle(null, 'قرآن', 'Quran',
55: [['name_ar' => 'حفظ', 'name_en' => 'Memorising'], ['name_ar' => 'تجويد', 'name_en' => 'Tajweed']]);
56: $this->levels = $this->quran->levels->pluck('id')->all();
57: $this->tracks = $this->quran->categories->pluck('id')->all();
71: $subject = $save->handle($this->quran->id, 'قرآن', 'Quran', [
75: ], $this->quran->categories->map(fn ($c) => ['id' => $c->id, 'name_ar' => $c->name_ar, 'name_en' => $c->name_en])->all());
82: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($teacher->id, 'female', subjects: [new TeacherSubjectData($this->quran->id, $amma, $amma)]));
84: expect(fn () => $save->handle($this->quran->id, 'قرآن', 'Quran', $without($amma)))->toThrow(ValidationException::class, 'Juz Amma');
85: expect($save->handle($this->quran->id, 'قرآن', 'Quran', $without($advanced))->levels)->toHaveCount(2);
88: expect(fn () => $save->handle(null, 'QURAN', null))->toThrow(ValidationException::class)
97: ->assertSee('Quran')->assertSee('Noorani')->assertSee('Tajweed')
109: [new TeacherSubjectData($this->quran->id, $noorani, $amma, [$this->tracks[1]])]);
… 6 more lines
```

### `apps/api/tests/Feature/People/GuardianConsentTest.php`

Lines: 267

```text
267: $lesson = new LessonCard('s1', 'scheduled', CarbonImmutable::now(), CarbonImmutable::now()->addHour(), $teacher->id, 'Ahmed', $this->yousef->id, 'Yousef', 'قرآن', 'Quran', null);
```

### `apps/api/tests/Feature/People/TeacherGroupsFormTest.php`

Lines: 27, 31, 59

```text
27: $this->quran = app(SaveSubject::class)->handle(null, 'قرآن', 'Quran');
31: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($t->id, 'female', ['ar'], [$this->quran->id]));
59: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($this->teacher->id, 'female', ['ar'], [$this->quran->id], acceptsGroups: true, maxGroupSize: 5));
```

### `apps/api/tests/Feature/Platform/AiGatewayTest.php`

Lines: 384, 406

```text
384: ->and(app(Routes::class)->resolve('recitation_check', 'speech')->steps[0]->engine->key)->toBe('a-speech-key');
406: gatewayRoute('recitation_check', 'default', [$ears], 'speech');
```

### `apps/api/tests/Feature/Platform/AiHelpersTest.php`

Lines: 110, 181, 182, 194, 261, 276, 281

```text
110: ->and($ai->why(AiFeature::RecitationCheck))->toBe('off')
181: ->assertSee(__('platform::ai.settings.helpers.recitation_check.data'))
182: ->assertFormSet(['practice_items' => false, 'report_draft' => false, 'recitation_check' => false, 'digest_wording' => false])
194: ->assertDontSee(__('platform::ai.settings.helpers.recitation_check.data'));
261: $heard = app(ElevenLabsSpeechToText::class)->transcribe(AiFeature::RecitationCheck, aiClip());
276: expect(DB::table('ai_usage')->sole())->toMatchArray(['provider' => 'elevenlabs', 'feature' => 'recitation_check', 'audio_seconds' => 3, 'outcome' => 'ok'])
281: app(ElevenLabsSpeechToText::class)->transcribe(AiFeature::RecitationCheck, aiClip());
```

### `apps/api/tests/Feature/Platform/PlatformSiteTest.php`

Lines: 52

```text
52: 'country' => 'sa', 'students' => '21-50', 'plan' => 'growth', 'message' => "We teach Quran.\nTen teachers.", 'utm_source' => 'google', 'utm_campaign' => 'launch',
```

### `apps/api/tests/Feature/Platform/UsageLedgerTest.php`

Lines: 109, 207, 208, 226, 495

```text
109: app(SaveAiSettings::class)->handle(['practice_items' => true, 'report_draft' => true, 'digest_wording' => true, 'curriculum_outline' => true, 'recitation_check' => true], test()->o…
207: // The recitation check: 2 a minute of what was heard (the demo hears half a second a word: one minute).
208: $speech->transcribe(AiFeature::RecitationCheck, usageRecording());
226: expect($rows->pluck('subject')->unique()->sort()->values()->all())->toBe(['curriculum_outline', 'digest_wording', 'practice_items', 'recitation_check', 'report_draft'])
495: foreach ([['practice_items', 0], ['practice_items', 0], ['report_draft', 50], ['report_draft', 0], ['recitation_check', 130]] as [$feature, $audio]) {
```

### `apps/api/tests/Feature/Privacy/PersonalDataSourcesTest.php`

Lines: 67, 68, 180, 182, 183, 185, 187, 189, 191, 192, 194, 199, 203, 206, 258, 259, 260, 261, 262, 264, 265, 266, 344, 393, 394, 395, 397, 398

```text
67: // The hifz map, the mistakes notebook and the checks of recited homework (the Quran module's).
68: 'quran' => ['copy' => ['student'], 'erases' => true],
180: DB::table('hifz_pages')->insert(['id' => $id(), 'student_id' => $s->id, 'page' => 582, 'state' => 'memorized', 'stability' => 10, 'difficulty' => 5,
182: DB::table('hifz_reviews')->insert(['id' => $id(), 'student_id' => $s->id, 'page' => 582, 'grade' => 3, 'source' => 'teacher', 'source_id' => $id(), 'reviewed_at' => $now, 'created_…
183: DB::table('hifz_recitations')->insert(['id' => $id(), 'student_id' => $s->id, 'page' => 582, 'status' => 'ready', 'grade' => 3, 'recited_by' => $g->id,
185: DB::table('recitation_mistakes')->insert(['id' => $id(), 'student_id' => $s->id, 'session_id' => $lesson, 'teacher_id' => $tr->id, 'surah' => 78, 'verse' => 3, 'word' => 2,
187: // The Quran program: the student's plan and a lesson's result (its teacher's note is never in the copy).
189: DB::table('quran_programs')->insert(['id' => $program, 'name' => 'Juz Amma', 'track' => 'talqin', 'scope_from_surah' => 78, 'scope_from_verse' => 1, 'scope_to_surah' => 114,
191: $quranPlan = $id();
192: DB::table('quran_plans')->insert(['id' => $quranPlan, 'program_id' => $program, 'enrollment_id' => $t->booked->enrollmentId, 'student_id' => $s->id,
194: DB::table('quran_lesson_results')->insert(['id' => $id(), 'session_id' => $lesson, 'student_id' => $s->id, 'plan_id' => $quranPlan, 'recorded_by' => $tr->id,
199: DB::table('quran_exams')->insert(['id' => $failed, 'plan_id' => $quranPlan, 'program_id' => $program, 'student_id' => $s->id, 'enrollment_id' => $t->booked->enrollmentId,
… 16 more lines
```

### `apps/api/tests/Feature/Realtime/LiveUpdatesTest.php`

Lines: 37

```text
37: $this->subject = app(CatalogApi::class)->createSubject('تجويد', 'Tajweed');
```

### `apps/api/tests/Feature/Scheduling/AcademyCalendarTest.php`

Lines: 68, 85, 103, 134, 214

```text
68: ->and($rows[0]->teacher)->toBe($this->teacher->name)->and($rows[0]->student)->toBe($this->student->name)->and($rows[0]->subject_en)->toBe('Quran')
85: ->and($count(new CalendarFilter(subjectId: $this->quran)))->toBe(2)
103: ->and($calendar->bySubject(new CalendarFilter, ...calendarWeek('Africa/Cairo', 'month'))[0]['name'])->toBe(app()->getLocale() === 'ar' ? 'قرآن' : 'Quran');
134: ->assertSee(e('/admin/calendar?student='.$this->student->id.'&subject='.$this->quran), false);
214: ->and($lessons[1])->toEqual(['2026-10-06', '18:00', '18:30', 30, $this->teacher->name, $this->student->name, 'Quran', 'Regular', 'Booked', 'Awaiting payment', '', ''])
```

### `apps/api/tests/Feature/Scheduling/AttendanceSegmentsTest.php`

Lines: 20, 80

```text
20: $subject = app(CatalogApi::class)->createSubject('تجويد', 'Tajweed');
80: expect($card->teacherName)->toBe('Sara')->and($card->studentName)->toBe('Omar')->and($card->subject('en'))->toBe('Tajweed')->and($card->isOpen())->toBeTrue()
```

### `apps/api/tests/Feature/Scheduling/ConcurrencyTest.php`

Lines: 92, 103, 113, 115, 137, 186, 211, 253, 263

```text
92: $this->rivalCommitsBefore('insert into "session_participants"', fn () => $this->rivalBooks($this->teacher->id, $this->second->id, $this->quran, $at));
103: $this->rivalCommitsBefore('insert into "session_participants"', fn () => $this->rivalBooks($this->teacher->id, $this->second->id, $this->quran, $extraAt));
113: $this->rivalCommitsBefore('insert into "session_participants"', fn () => $this->rivalBooks($this->teacher->id, $this->second->id, $this->quran, $trialAt));
115: expect(fn () => app(ConfirmBooking::class)->trial($hold, $third->id, $this->quran, $this->admin->id))->toThrow(ValidationException::class)
137: expect(fn () => app(EnrollStudent::class)->handle($hold, $this->second->id, $this->quran, new EnrollmentTerms(Plan::query()->value('id'), $this->second->id, PriceRegion::query()->v…
186: $other = app(ScheduleSession::class)->handle(new NewSession($this->other->id, $this->second->id, $this->quran, $lesson->starts_at, 30, 'Asia/Riyadh'));
211: $this->rivalBooks($slot->teacher_id, $slot->student_id, $this->quran, $start, 30, ['enrollment_id' => $slot->enrollment_id, 'slot_id' => $slot->id, 'occurrence_key' => $key]);
253: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($third->id, 'female', ['ar'], [$this->quran]));
263: $this->rivalBooks($taken, $this->second->id, $this->quran, $lesson->starts_at);
```

### `apps/api/tests/Feature/Scheduling/CourseStopTest.php`

Lines: 123, 224, 356

```text
123: expect(app(FamilyNotices::class)->courses($this->student->id))->toBe(['Quran is paused from Tuesday 13 October until Saturday 24 October.']);
224: app(EnrollmentApi::class)->create(new NewEnrollment(User::factory()->withRole(Role::Student)->create()->id, $this->quran, $this->teacher->id, CarbonImmutable::now()));
356: $existing = fn () => app(BringExistingSchedule::class)->exists($this->student->id, $this->teacher->id, $this->quran);
```

### `apps/api/tests/Feature/Scheduling/DstZonesTest.php`

Lines: 41

```text
41: $t->subject = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
```

### `apps/api/tests/Feature/Scheduling/FindTeacherExactTest.php`

Lines: 47, 62, 74, 100

```text
47: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($this->layla->id, 'female', ['ar'], [$this->quran]));
62: ->fillForm(array_diff_key($data, ['timezone' => true]) + ['subject_id' => test()->quran, 'start_date' => '2026-11-03', 'per_week' => 2]);
74: $free = app(FreeTimesQuery::class)->run(new TeacherSearch($this->quran, $pref));
100: $page = Livewire::withQueryParams(['subject' => $this->quran, 'days' => '6,7', 'from' => '0', 'to' => '24'])->test(FindTeacher::class)
```

### `apps/api/tests/Feature/Scheduling/FindTeacherFiltersTest.php`

Lines: 35, 38, 42, 44, 48, 61, 68, 85, 95, 109

```text
35: $subject = app(SaveSubject::class)->handle($this->quran, 'قرآن', 'Quran',
38: [$this->memorising, $this->tajweed] = $subject->categories->pluck('id')->all();
42: subjects: [new TeacherSubjectData($this->quran, $this->noorani, $this->amma, [$this->memorising])]));
44: subjects: [new TeacherSubjectData($this->quran, $this->advanced)]));
48: $this->find = fn (...$filters) => collect(app(FindTeachersQuery::class)->run(new TeacherSearch($this->quran, $pref, ...$filters)))
61: ->and(($this->find)(categoryId: $this->tajweed))->toBe([$this->other->id])
68: subjects: [new TeacherSubjectData($this->quran)]));
85: ->fillForm(['subject_id' => $this->quran])
95: ->set('data.student_id', $this->student->id)->set('data.subject_id', $this->quran)->set('data.duration', 25)
109: ->set('data.student_id', $this->student->id)->set('data.subject_id', $this->quran)->set('data.duration', 25)
```

### `apps/api/tests/Feature/Scheduling/FindTeacherStepsTest.php`

Lines: 39, 74, 97

```text
39: 'subject_id' => test()->quran, 'timezone' => 'Asia/Riyadh', 'start_date' => '2026-10-06', 'per_week' => 2,
74: Livewire::withQueryParams(['subject' => $this->quran, 'days' => '2', 'from' => '19', 'to' => '21'])->test(FindTeacher::class)
97: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($this->teacher->id, 'female', maxDailyLessons: 1, subjects: [new TeacherSubjectData($this->quran)]));
```

### `apps/api/tests/Feature/Scheduling/FindTeacherTest.php`

Lines: 26, 34, 48, 65, 95, 108

```text
26: $this->quran = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
34: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($this->{$key}->id, $gender, ['ar', 'en'], [$this->quran]));
48: return app(FindTeachersQuery::class)->run(new TeacherSearch(test()->quran, $pref, $gender, searcherId: $searcher));
65: app(ScheduleSession::class)->handle(new NewSession($this->nour->id, User::factory()->withRole(Role::Student)->create()->id, $this->quran, CarbonImmutable::parse('2026-10-24 18:00',…
95: $trial = app(ConfirmBooking::class)->trial($batch, $this->student->id, $this->quran, $this->coordinator->id);
108: expect(fn () => app(ConfirmBooking::class)->trial($batch, $this->student->id, $this->quran, $this->coordinator->id))
```

### `apps/api/tests/Feature/Scheduling/FreeTimesQueryTest.php`

Lines: 38, 71, 106

```text
38: return app(FreeTimesQuery::class)->run(new TeacherSearch(test()->quran, $pref, forMinor: $forMinor));
71: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($this->teacher->id, 'female', maxDailyLessons: 1, subjects: [new TeacherSubjectData($this->quran)]));
106: $search = new TeacherSearch($this->quran, new StudentPreference('Europe/London', [], 1, 30, CarbonImmutable::parse('2026-10-06'), 2, 2));
```

### `apps/api/tests/Feature/Scheduling/GroupJoiningTest.php`

Lines: 173, 203

```text
173: expect($refusal(fn () => app(EnrollStudent::class)->handle($batch, $student->id, $this->quran, new EnrollmentTerms($this->groupPlan->id, $this->payer->id, $this->region->id), $this…
203: ->saveTeacherProfile(new TeacherProfileData($t->id, 'male', ['ar'], [$this->quran], acceptsGroups: true, maxGroupSize: 4)))->id);
```

### `apps/api/tests/Feature/Scheduling/GroupLessonsTest.php`

Lines: 62, 72, 74, 226, 231

```text
62: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($other->id, 'male', ['ar'], [$this->quran]));
72: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($this->teacher->id, 'female', ['ar'], [$this->quran]));
74: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($this->teacher->id, 'female', ['ar'], [$this->quran], acceptsGroups: false, maxGroupSize: 9));
226: ->saveTeacherProfile(new TeacherProfileData($t->id, 'male', ['ar'], [$this->quran], acceptsGroups: true, maxGroupSize: 2)))->id);
231: $open = app(OpenGroups::class)->handle($this->quran, studentTimezone: 'Europe/London');
```

### `apps/api/tests/Feature/Scheduling/GroupOutcomesTest.php`

Lines: 240

```text
240: $this->teacher->id, $this->quran, 30, [['weekday' => 1, 'start' => '18:00'], ['weekday' => 4, 'start' => '18:00']], capacity: 3, minToStart: 2,
```

### `apps/api/tests/Feature/Scheduling/GroupPanelsTest.php`

Lines: 141, 146

```text
141: expect($body->title)->toContain('Quran group')->toContain('6:00 PM')->not->toContain('Amira')
146: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($this->teacher->id, 'female', ['ar'], [$this->quran], acceptsGroups: true, maxGroupSize: 5));
```

### `apps/api/tests/Feature/Scheduling/GroupScreensTest.php`

Lines: 136, 151, 205, 207, 214, 237, 245

```text
136: $page = Livewire::withQueryParams(['mode' => 'group', 'student' => $late->id, 'subject' => $this->quran])->test(FindTeacher::class)->assertOk()
151: Livewire::withQueryParams(['mode' => 'group', 'subject' => $this->quran])->test(FindTeacher::class)
205: Livewire::withQueryParams(['mode' => 'group', 'subject' => $this->quran, 'student' => $third->id])->test(FindTeacher::class)
207: Livewire::withQueryParams(['mode' => 'group', 'subject' => $this->quran, 'student' => $third->id])->test(FindTeacher::class)
214: $page = Livewire::withQueryParams(['mode' => 'group', 'student' => $student->id, 'subject' => $this->quran])->test(FindTeacher::class)
237: Livewire::withQueryParams(['mode' => 'group', 'subject' => $this->quran])->test(FindTeacher::class)
245: $page = Livewire::withQueryParams(['subject' => $this->quran])->test(FindTeacher::class)
```

### `apps/api/tests/Feature/Scheduling/GroupSurfacesTest.php`

Lines: 154, 158, 162

```text
154: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($other->id, 'male', ['ar'], [$this->quran]));
158: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($other->id, 'male', ['ar'], [$this->quran], acceptsGroups: true, maxGroupSize: 2));
162: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($other->id, 'male', ['ar'], [$this->quran], acceptsGroups: true, maxGroupSize: 5));
```

### `apps/api/tests/Feature/Scheduling/MinorsGuardTest.php`

Lines: 61, 77, 103, 106

```text
61: return app(EnrollStudent::class)->handle($hold, test()->child->id, test()->quran, new EnrollmentTerms(Plan::query()->value('id'), test()->parent->id, PriceRegion::query()->value('i…
77: ->and(fn () => app(ConfirmBooking::class)->trial($trial, $this->child->id, $this->quran, $coordinator->id))->toThrow(ValidationException::class, $this->paused)
103: $schedule = fn (User $student) => new ExistingSchedule($student->id, $this->teacher->id, $this->quran, 30, [['weekday' => 2, 'time' => '19:00'], ['weekday' => 6, 'time' => '19:00']…
106: ->and(app(ScheduleImport::class)->exists($this->child->id, $this->teacher->id, $this->quran))->toBeFalse()
```

### `apps/api/tests/Feature/Scheduling/SessionLifecycleTest.php`

Lines: 33

```text
33: $this->subject = app(CatalogApi::class)->createSubject('تجويد', 'Tajweed');
```

### `apps/api/tests/Feature/Scheduling/ShiftProposalTest.php`

Lines: 160, 182

```text
160: $subject = app(CatalogApi::class)->createSubject('تجويد', 'Tajweed');
182: $subject = app(CatalogApi::class)->createSubject('تجويد', 'Tajweed');
```

### `apps/api/tests/Feature/Scheduling/ShiftProposalsScreenTest.php`

Lines: 277

```text
277: $subject = app(CatalogApi::class)->createSubject('تجويد', 'Tajweed');
```

### `apps/api/tests/Feature/Scheduling/ShiftSlotTimesTest.php`

Lines: 68

```text
68: app(ScheduleSession::class)->handle(new NewSession($this->other->id, $this->student->id, $this->quran, CarbonImmutable::parse('2026-10-20 19:00', 'Africa/Cairo'), 30, 'Asia/Riyadh'…
```

### `apps/api/tests/Feature/Scheduling/StartOwnCourseTest.php`

Lines: 63, 101, 105, 137, 147, 153, 159, 198, 323, 349, 355, 375, 378, 384, 389, 390, 433, 434, 437, 453, 460, 514, 573, 591, 693, 698

```text
63: * teacher (a woman) and a Riyadh teacher (a man) teach Quran on Tuesdays and
101: 'for_child' => true, 'learner_name' => 'Yara Salem', 'learner_birth_year' => 2017, 'subject_id' => test()->quran, 'source' => 'website',
105: $session = app(ConfirmBooking::class)->trial($batch, $learner, test()->quran, test()->admin->id);
137: return j3Api('GET', 'family/start/slots?'.http_build_query(['learner_id' => test()->yara, 'subject_id' => test()->quran, 'plan_id' => test()->plan->id,
147: 'learner_id' => test()->yara, 'subject_id' => test()->quran, 'plan_id' => test()->plan->id, 'price_minor' => 40000, 'currency' => 'SAR',
153: $data = j3Api('GET', 'family/start/options?'.http_build_query(['learner_id' => $this->yara, 'subject_id' => $this->quran]))->assertOk()->json('data');
159: ->and(collect($data['subjects'])->firstWhere('id', $this->quran))->toMatchArray(['can_start' => true, 'course' => null, 'why_not' => null])
198: app(ConfirmBooking::class)->trial($batch, $this->yara, $this->quran, $this->admin->id);
323: app(EnrollStudent::class)->handle($batch, $brother->id, $this->quran, new EnrollmentTerms($this->plan->id, $this->mother->id, $this->region->id), $this->admin->id);
349: j3Api('GET', 'family/start/slots?'.http_build_query(['learner_id' => $this->yara, 'subject_id' => $this->quran, 'plan_id' => $this->plan->id, 'teacher_id' => $this->teacher->id]))
355: $options = j3Api('GET', 'family/start/options?'.http_build_query(['learner_id' => $this->yara, 'subject_id' => $this->quran]))->assertOk()->json('data');
375: // The office enrolled the adult student of the fixture; for him, his guardian starts nothing new in Quran.
… 14 more lines
```

### `apps/api/tests/Feature/Scheduling/TimeOffTest.php`

Lines: 45

```text
45: * (15:00 UTC) with a Cairo teacher; a Riyadh teacher teaches Quran too and
```

### `apps/api/tests/Feature/Security/AbilityMatrixTest.php`

Lines: 79, 80, 81, 82, 98

```text
79: 'quran.manage' => [$o, $a],
80: 'quran.teach' => [$t],
81: 'quran.examine' => [$o, $a, $su],
82: 'quran.board' => [$o, $a, $su],
98: 'quran.manage' => 'quran', 'quran.teach' => 'quran', 'quran.examine' => 'quran', 'quran.board' => 'quran',
```

### `apps/api/tests/Feature/Security/TeacherContactPrivacyTest.php`

Lines: 20

```text
20: 'features' => ['crm', 'online_payments', 'import', 'custom_branding', 'payroll', 'quran', 'groups', 'curriculum', 'games', 'messaging', 'announcements', 'support', 'evaluation', 's…
```

### `apps/api/tests/Feature/Security/TenantIsolationSweepTest.php`

Lines: 35, 85, 86, 87, 88, 238, 239, 243, 245, 246, 263, 264, 286

```text
35: 'features' => ['crm', 'online_payments', 'import', 'custom_branding', 'payroll', 'quran', 'groups', 'curriculum', 'games', 'messaging', 'announcements', 'support', 'evaluation', 's…
85: // The Quran's exams and certificates (the certificate by its public code).
86: 'exam' => $one('quran_exams'),
87: 'code' => (string) $platform->table('quran_certificates')->where('academy_id', $this->demo)->orderBy('id')->value('code'),
88: 'certificate' => $one('quran_certificates'),
238: // The academy's hifz: its own courses only; the demo's student, asked for by course, is not found.
239: 'admin/hifz', 'admin/hifz/{enrollment}',
243: 'teacher' => ['teach/reports/{report}', 'teach/reports/{report}/game', 'teach/students/{enrollment}', 'teach/students/{enrollment}/hifz', 'class/{session}', 'class/{session}/go', '…
245: 'guardian' => ['my', 'class/{session}', 'class/{session}/mushaf', 'learning/files/{submission}', 'support/files/{message}', 'billing/proofs/{proof}/file'],
246: 'student' => ['class/{session}', 'class/{session}/go', 'class/{session}/mushaf', 'learning/files/{submission}'],
263: // The shared mushaf and the lesson's own channel, asked with what would pass on the demo's host.
264: 'class/{session}/mushaf' => ['change' => 'turn', 'page' => 1],
… 1 more lines
```

### `apps/api/tests/Feature/Site/PublicSiteTest.php`

Lines: 40, 78, 79, 80, 81, 82, 92, 94, 136, 150, 151, 156

```text
40: 'subject_id' => test()->quran, 'for_child' => true, 'child_name' => 'Yara', 'child_birth_year' => now()->year - 9,
78: expect($subjects->keys()->sort()->values()->all())->toBe(['Arabic', 'Quran'])
79: ->and($subjects['Quran']['id'])->toBe($this->quran)
80: ->and($subjects['Quran']['levels'])->toBe(['Beginner', 'Intermediate', 'Advanced'])
81: ->and($subjects['Quran']['categories'])->toBe(['Memorising', 'Tajweed'])
82: ->and($subjects['Quran']['programs'])->toBe([['name' => 'Nour Al-Bayan', 'description' => 'From the letters to reading']])
92: 'id' => $sara, 'name' => 'Ms Sara', 'bio' => 'Sara Fathy teaches Quran.', 'photo_url' => null, 'gender' => 'female',
94: 'subjects' => [['name' => 'Quran', 'level_from' => 'Beginner', 'level_to' => 'Intermediate']], 'accepts_trials' => true, 'accepts_groups' => false,
136: 'subject_id' => $this->quran, 'for_child' => true, 'child_name' => 'Yara', 'utm_source' => 'instagram', 'utm_medium' => 'paid', 'utm_campaign' => 'ramadan', 'status' => 'new',
150: 'kind' => 'teach', 'name' => 'Ahmed Zaki', 'phone' => '+20 100 222 3333', 'subject_ids' => [$this->quran, $this->arabic, $this->quran], 'years_teaching' => 6,
151: 'subject_id' => $this->quran, 'for_child' => true,
156: 'kind' => 'teach', 'phone' => '+201002223333', 'subject_ids' => [$this->quran, $this->arabic], 'years_teaching' => 6, 'subject_id' => null, 'for_child' => false, 'child_name' => nu…
```

### `apps/api/tests/Feature/Site/SiteAdminTest.php`

Lines: 99, 104, 168

```text
99: ->set('data.hero.title_en', 'Learn Quran at home')
104: ->and(SiteSettings::current()->content['hero']['title_en'])->toBe('Learn Quran at home')
168: $teach = siteRequest('teach', ['subject_ids' => [$this->quran], 'years_teaching' => 6, 'phone' => '+201002223333']);
```

### `apps/api/tests/Feature/Site/SiteLeadsTest.php`

Lines: 40, 52, 100

```text
40: 'kind' => 'trial', 'name' => 'Marwa Salem', 'phone' => '+966501234567', 'country' => 'KW', 'subject_id' => test()->quran,
52: 'learner_name' => 'Yara', 'learner_birth_year' => now()->year - 9, 'subject_id' => $this->quran, 'utm_source' => 'instagram', 'utm_medium' => 'paid',
100: $this->postJson('http://noor.lms.test/api/v1/site/requests', trialForm(['kind' => 'teach', 'subject_ids' => [$this->quran]]))->assertCreated();
```

### `apps/api/tests/Feature/Site/TeacherCardTest.php`

Lines: 44, 52, 124, 128

```text
44: ->set('data.bio', "Ten years teaching Quran.\n\n\n\nPatient with beginners.")
52: 'display_name' => 'Mr Omar', 'bio' => "Ten years teaching Quran.\n\nPatient with beginners.", 'shown' => true, 'hidden_by_academy' => false, 'photo_path' => null,
124: $card = app(SaveTeacherCard::class)->handle($this->omar->id, ['display_name' => 'Mr Omar', 'bio' => 'Quran teacher', 'shown' => true], UploadedFile::fake()->image('me.webp', 100, 1…
128: expect($copy)->toMatchArray(['display_name' => 'Mr Omar', 'bio' => 'Quran teacher', 'photo' => $card->photo_path, 'shown' => true, 'hidden_by_academy' => false]);
```

### `apps/api/tests/Support/AcademySite.php`

Lines: 24, 25, 44, 46, 47, 49, 51, 68, 69, 71

```text
24: * owner, an admin, sales, a scheduler and an accountant; Quran (levels
25: * Beginner to Advanced, tracks Memorising and Tajweed, a published program
44: $quran = app(SaveSubject::class)->handle(null, 'قرآن', 'Quran',
46: [['name_ar' => 'حفظ', 'name_en' => 'Memorising'], ['name_ar' => 'تجويد', 'name_en' => 'Tajweed']]);
47: $this->quran = $quran->id;
49: $levels = $quran->levels->sortBy('ordinal')->pluck('id')->values()->all();
51: $program = app(SaveProgram::class)->handle(null, ['subject_id' => $this->quran, 'name_ar' => 'نور البيان', 'name_en' => 'Nour Al-Bayan',
68: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($teacher->id, $gender, ['ar', 'en'], [$this->quran], ageGroups: ['kids', 'teen'],
69: subjects: [new TeacherSubjectData($this->quran, $levels[0], $levels[1])]));
71: TeacherPublicCard::query()->create(['teacher_id' => $teacher->id, 'display_name' => 'Ms '.explode(' ', $name)[0], 'bio' => "{$name} teaches Quran.",
```

### `apps/api/tests/Support/EnrolledStudent.php`

Lines: 20, 31, 42, 61

```text
20: * Monday 5 October 2026, 10:00 in Cairo: an adult Quran student in London enrolled
31: $this->quran = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
42: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($t->id, $gender, ['ar'], [$this->quran]));
61: return $this->booked = app(EnrollStudent::class)->handle($batch, $this->student->id, $this->quran, new EnrollmentTerms($plan->id, $guardian->id, $region->id), $this->admin->id);
```

### `apps/api/tests/Support/GroupLessons.php`

Lines: 34, 38, 62, 74, 75

```text
34: $this->quran = app(CatalogApi::class)->createSubject('قرآن', 'Quran');
38: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($this->teacher->id, 'female', ['ar'], [$this->quran], acceptsGroups: true, maxGroupSize: $teacherMax));
62: subjectId: $this->quran,
74: app(PeopleApi::class)->saveTeacherProfile(new TeacherProfileData($teacher->id, 'male', ['ar'], [$this->quran], acceptsGroups: true, maxGroupSize: 4));
75: $group = app(CreateGroup::class)->handle(new NewGroup($teacher->id, $this->quran, 30, [['weekday' => 1, 'start' => '19:00'], ['weekday' => 4, 'start' => '19:00']], capacity: 3), $t…
```

### `apps/api/tests/Unit/Curriculum/OutlineRulesTest.php`

Lines: 32

```text
32: ->and($long)->not->toHaveKey('quran')
```

### `apps/api/tests/Unit/Curriculum/PublishReadinessTest.php`

Lines: 11

```text
11: * without practice, or (in a curriculum that reads the Quran) without a text is
```

### `apps/api/tests/Unit/Deploy/ServerEnvTest.php`

Lines: 13

```text
13: 'STRIPE_CONNECT_REDIRECT', 'TAP_API_BASE', 'WHATSAPP_META_API_VERSION', 'QURAN_TEXT_URL', 'QURAN_DATA_URL',
```

### `apps/api/tests/Unit/Learning/ReportDraftMergeTest.php`

Lines: 50, 60, 61

```text
50: new TemplateField('f3', 'التجويد', 'Tajweed', 'rating', required: true),
60: $said = ['homework' => ['title' => 'Recite', 'accepts' => 'practice', 'due_days' => 0]];
61: expect(draftMerge([], $said)['report']['homework'])->toBe(['title' => 'Recite', 'instructions' => null, 'accepts' => 'any', 'due_days' => 1, 'practice' => false])
```

### `apps/api/tests/Unit/Platform/MeteringRulesTest.php`

Lines: 99

```text
99: // practice 1, weekly-note wording 1, outline 5, recitation 2 a minute, report draft 2 and 1 a minute.
```

### `apps/api/tests/Unit/Scheduling/BoardClassifierTest.php`

Lines: 33

```text
33: subjectEn: 'Tajweed',
```

### `apps/api/tests/Unit/SharedKernel/ArabicTextTest.php`

Lines: 6, 11, 13

```text
6: * Arabic as it is compared (the recitation check, quotations in a model's
11: it('drops the marks, the Quran\'s own signs and tatweel, and keeps the letters', function () {
13: // The Quran in its plain spelling (Tanzil's simple text): a dagger alef left there is one it does not write.
```

### `apps/api/tests/Unit/SharedKernel/WordAlignmentTest.php`

Lines: 7, 25, 45

```text
7: * help with recited homework). Ordinary sentences here, never the Quran.
25: it('reads a whole recitation as said, whatever the marks and alef forms', function () {
45: it('leaves the rest missing when the reciter stopped early', function () {
```

## App (apps/mobile) (38 files)

### `apps/mobile/README.md`

Lines: 22, 23, 37

```text
22: | `lib/core` | `network/` (dio: `X-Academy`, Bearer, `Accept-Language`, `X-Timezone` on every call; RFC 7807 errors as `ApiProblem`, with a type's own members in `extra`; offline r…
23: | `lib/features/<x>` | `data/` (a typed repository over the API), `domain/` (models from JSON), `presentation/` (pages, widgets, cubits): `auth` (a code that finds the accounts in …
37: flutter test            # unit, widget (sign-in with the privacy notice and terms before it, cancelling a lesson, a substitute turned down, rating, the kids' look without them, joi…
```

### `apps/mobile/lib/app/bootstrap.dart`

Lines: 29

```text
29: yield LicenseEntryWithLineBreaks(const ['Amiri Quran'], await rootBundle.loadString('assets/fonts/OFL-AmiriQuran.txt'));
```

### `apps/mobile/lib/app/di/services.dart`

Lines: 16, 22, 30, 55, 56, 57, 94, 96, 97, 99, 100, 149, 150, 151

```text
16: import '../../features/hifz/data/hifz_repository.dart';
22: import '../../features/quran/data/quran_repository.dart';
30: import '../../features/mushaf/data/mushaf_repository.dart';
55: hifz = HifzRepository(api),
56: mushaf = MushafRepository(api),
57: quran = QuranRepository(api),
94: final HifzRepository hifz;
96: /// A Quran lesson's shared mushaf and the mistakes notebook.
97: final MushafRepository mushaf;
99: /// The Quran program: plans and portions, lessons' results, exams and certificates.
100: final QuranRepository quran;
149: RepositoryProvider.value(value: hifz),
… 2 more lines
```

### `apps/mobile/lib/app/router/router.dart`

Lines: 32, 33, 40, 45, 46, 47, 136, 137, 143, 144, 240, 241, 246, 247, 480, 495

```text
32: import '../../features/hifz/presentation/hifz_page.dart';
33: import '../../features/hifz/presentation/student_hifz_page.dart';
40: import '../../features/mushaf/presentation/mushaf_page.dart';
45: import '../../features/quran/presentation/examiner_page.dart';
46: import '../../features/quran/presentation/lesson_page.dart';
47: import '../../features/quran/presentation/quran_page.dart';
136: // A look's journey with the creatures' album (an island's creatures, a creature just named), the hifz map and the
137: // Quran (plans, exams, certificates) under it.
143: page('hifz', (_) => const HifzPage()),
144: page('quran', (_) => QuranPage(base: path)),
240: // A Quran lesson's shared mushaf, over any look's tabs (beside a lesson on Zoom or Meet too).
241: page('/lessons/:id/mushaf', (s) => LessonMushafPage(lessonId: s.pathParameters['id']!)),
… 4 more lines
```

### `apps/mobile/lib/core/auth/modules.dart`

Lines: 12, 73, 74

```text
12: quran('quran'),
73: // Everything of the Quran: the hifz map and the Quran under a journey, a lesson's mushaf and portion, the exams.
74: if (has('hifz') || has('mushaf') || has('quran') || has('quran-exams')) return Feature.quran;
```

### `apps/mobile/lib/core/realtime/live.dart`

Lines: 60, 61, 63, 64

```text
60: /// A learner's hifz map: a page reviewed, marked or recited (and a recited page's check done).
61: static const hifz = 'hifz.changed';
63: /// A lesson's shared mushaf: its teacher turned the page or marked a word (the teacher, the student, the guardians).
64: static const mushaf = 'mushaf.changed';
```

### `apps/mobile/lib/features/classroom/presentation/pages/classroom_page.dart`

Lines: 14, 15, 16, 36, 38, 72, 73, 74, 75, 83, 90, 102, 107, 108, 109, 112, 115, 117, 309, 312, 313, 321, 322, 334

```text
14: import '../../../mushaf/data/mushaf_repository.dart';
15: import '../../../mushaf/domain/mushaf.dart';
16: import '../../../mushaf/presentation/widgets/mushaf_pane.dart';
36: /// Quran lesson has its shared mushaf a tap away, the main picture small over
38: /// `mushaf` topic, heard only from the teacher's seat), and the mushaf signal
72: /// The lesson's shared mushaf, once the API says it has one; shown over the video while [_showMushaf].
73: late final _place = MushafPlace(widget.lessonId);
74: LoadCubit<LessonMushaf>? _mushaf;
75: bool _showMushaf = false;
83: if (isMushafSignal(topic: e.topic, metadata: e.participant?.metadata)) unawaited(_mushaf?.load());
90: unawaited(_findMushaf());
102: unawaited(_mushaf?.close());
… 12 more lines
```

### `apps/mobile/lib/features/classroom/presentation/widgets/room/room_controls.dart`

Lines: 34, 85, 128, 130

```text
34: /// The lesson has its shared mushaf, and it is open now.
85: /// camera, the other camera, the mushaf, audio only, the layout, recording
128: id: 'mushaf-toggle',
130: label: s.panelOpen ? l.mushafShowVideo : l.mushafShow,
```

### `apps/mobile/lib/features/classroom/presentation/widgets/room/room_view.dart`

Lines: 52, 225, 240, 243, 246

```text
52: /// The side panel (the lesson's mushaf), shown instead of the stage while [RoomControlsState.panelOpen].
225: key: const Key('classroom-mushaf'),
240: message: context.l10n.mushafBackToVideo,
243: label: context.l10n.mushafBackToVideo,
246: key: const Key('mushaf-pip'),
```

### `apps/mobile/lib/features/dashboard/presentation/widgets/next_lesson_card.dart`

Lines: 7, 8, 17, 18, 22, 26, 27, 174, 193, 194

```text
7: import '../../../mushaf/presentation/widgets/mushaf_entry.dart';
8: import '../../../quran/presentation/widgets/quran_entry.dart';
17: /// the room opens, before that the time it opens (and, in a Quran lesson,
18: /// its shared mushaf under it, and for its teacher its portion). The countdown is drawn
22: const NextLessonCard({required this.lesson, this.quran = false, super.key});
26: /// The teacher's: the way to the lesson's Quran portion and record, once it follows a Quran plan.
27: final bool quran;
174: MushafEntry(
193: if (quran)
194: QuranLessonEntry(
```

### `apps/mobile/lib/features/homework/domain/homework.dart`

Lines: 2, 66, 133, 142, 143

```text
2: import 'recitation.dart';
66: /// What it asks to recite, checked word by word for the teacher (teacher answers only).
133: check: RecitationCheck.fromJson(json['check']),
142: /// The recording's check against what the homework asks to recite (teacher answers only).
143: final RecitationCheck? check;
```

### `apps/mobile/lib/features/journey/domain/journey.dart`

Lines: 33, 48, 75, 76, 133, 135, 136, 138, 139

```text
33: this.hifz,
48: hifz: _map(json['hifz']) == null ? null : JourneyHifz.fromJson(_map(json['hifz'])!),
75: /// Today's hifz review (null until the learner has pages on their hifz map).
76: final JourneyHifz? hifz;
133: /// Today's hifz review in short (`GET learning/hifz` has it in full): the pages left today, those done today, and a
135: class JourneyHifz {
136: const JourneyHifz({required this.due, required this.doneToday, required this.daily});
138: factory JourneyHifz.fromJson(Map<String, dynamic> json) =>
139: JourneyHifz(due: _int(json['due']), doneToday: _int(json['done_today']), daily: _int(json['daily']));
```

### `apps/mobile/lib/features/journey/presentation/calm/calm_journey.dart`

Lines: 16, 17, 96, 97

```text
16: import '../../../quran/presentation/widgets/quran_entry.dart';
17: import '../widgets/hifz_card.dart';
96: if (_m.hifz case final hifz?) HifzJourneyCard(hifz: hifz, place: widget.place),
97: QuranJourneyCard(base: widget.place.base),
```

### `apps/mobile/lib/features/journey/presentation/guardian/guardian_journey.dart`

Lines: 17, 18, 85, 86

```text
17: import '../../../quran/presentation/widgets/quran_entry.dart';
18: import '../widgets/hifz_card.dart';
85: if (_m.hifz case final hifz?) HifzJourneyCard(hifz: hifz, place: widget.place),
86: QuranJourneyCard(base: widget.place.base),
```

### `apps/mobile/lib/features/journey/presentation/journey_page.dart`

Lines: 20, 36, 57, 149, 193

```text
20: import '../../quran/presentation/widgets/quran_entry.dart';
36: /// the lessons, homework and Quran a tap away.
57: refreshOn: c.read<Live>().on({Live.practice, Live.homework, Live.lessons, Live.hifz}),
149: /// and the lessons, homework, a family's reports and the Quran still a tap away.
193: QuranJourneyCard(base: place.base),
```

### `apps/mobile/lib/features/journey/presentation/kids/kids_journey.dart`

Lines: 20, 21, 228, 229

```text
20: import '../../../quran/presentation/widgets/quran_entry.dart';
21: import '../widgets/hifz_card.dart';
228: if (_m.hifz case final hifz?) HifzJourneyCard(hifz: hifz, place: widget.place, kids: true),
229: QuranJourneyCard(base: widget.place.base, kids: true),
```

### `apps/mobile/lib/features/journey/presentation/middle/middle_journey.dart`

Lines: 15, 16, 86, 87

```text
15: import '../../../quran/presentation/widgets/quran_entry.dart';
16: import '../widgets/hifz_card.dart';
86: if (_m.hifz case final hifz?) HifzJourneyCard(hifz: hifz, place: widget.place),
87: QuranJourneyCard(base: widget.place.base),
```

### `apps/mobile/lib/features/schedule/presentation/widgets/lesson_card.dart`

Lines: 8, 13, 140, 141

```text
8: import '../../../mushaf/presentation/widgets/mushaf_entry.dart';
13: /// its state, and what can be done now (join, open its mushaf in a Quran
140: if (mushafWorthAsking(l0, next: highlight))
141: MushafEntry(
```

### `apps/mobile/lib/features/schedule/presentation/widgets/lesson_row.dart`

Lines: 9, 10, 16, 26, 27, 174, 324, 326, 332, 333, 335

```text
9: import '../../../mushaf/presentation/widgets/mushaf_entry.dart';
10: import '../../../quran/presentation/widgets/quran_entry.dart';
16: const LessonActions({this.cancel, this.refuse, this.rate, this.dispute, this.report, this.quran = false});
26: /// The teacher's way to its Quran portion and record, shown once the lesson follows a Quran plan.
27: final bool quran;
174: /// opens), its shared mushaf in a Quran lesson, and what else may be done
324: MushafEntry(
326: onOpen: _after(context, () => openMushaf(host, x.id)),
332: if (actions.quran && !x.cancelled)
333: QuranLessonEntry(
335: onOpen: _after(context, () => openQuranLesson(host, x.id)),
```

### `apps/mobile/lib/features/teaching/data/teaching_repository.dart`

Lines: 10, 98, 100

```text
10: import '../../homework/domain/recitation.dart';
98: /// The Quran's surahs, to choose what homework asks to recite (empty until the platform has its copy).
100: for (final s in (await _api.get('teacher/texts/quran'))['data'] as List<dynamic>) Surah.fromJson(s as Map<String, dynamic>),
```

### `apps/mobile/lib/features/teaching/domain/reports.dart`

Lines: 3, 173, 196, 225, 226, 228, 231

```text
3: import '../../homework/domain/recitation.dart';
173: this.recitationCheck = false,
196: recitationCheck: (json['assist'] as Map<String, dynamic>?)?['recitation_check'] == true,
225: /// The academy turned on the recitation check: homework handed in by voice may say what to recite.
226: final bool recitationCheck;
228: /// The passage of the report's lessons' text, to start what to recite from.
231: /// The verses with the words marked in the lesson's shared mushaf (the surah with the most marks), to recite again.
```

### `apps/mobile/lib/features/teaching/presentation/pages/marking_page.dart`

Lines: 17, 22, 141, 145

```text
17: import '../widgets/recitation_check_view.dart';
22: /// recite); give a grade and a word. The marked ones stay one tap away.
141: if (h.expected?.title case final title?) Text(l.reciteWhat(title), style: context.text.bodySmall),
145: if (s.check case final check?) RecitationCheckView(check: check),
```

### `apps/mobile/lib/features/teaching/presentation/pages/more_page.dart`

Lines: 13, 160

```text
13: import '../../../quran/presentation/widgets/quran_entry.dart';
160: const QuranExaminerGroup(),
```

### `apps/mobile/lib/features/teaching/presentation/pages/report_page.dart`

Lines: 17, 33, 34, 58, 59, 115, 144, 145, 146, 147, 148, 149, 202, 203, 213, 214, 288, 289, 290, 292, 293, 294, 304, 534, 535, 536, 537, 988, 989, 990, 991, 992, 993, 996, 997, 999, 1007, 1009, 1010, 1011, 1012, 1016, 1018, 1019, 1022, 1023, 1025, 1027, 1028, 1037, 1039, 1048, 1049, 1052, 1058, 1059, 1063, 1090, 1140

```text
17: import '../../../homework/domain/recitation.dart';
33: /// say what to recite (the lesson's text, or the verses with the words marked
34: /// in its mushaf), for a check of each recording. Sending and keeping a
58: // The surahs to choose what homework asks to recite, when the form may ask it.
59: final surahs = form.recitationCheck || form.homework?.expected != null ? await repository.surahs() : const <Surah>[];
115: /// The Quran's surahs, when the form may ask what homework is to recite.
144: /// What homework handed in by voice asks to recite: its own passage, else the lessons'.
145: late final Expected? _recited = f.homework?.expected ?? f.expectedSuggestion;
146: late bool _reciteOn = d == null ? f.homework?.expected != null : d!['recite_on'] == true;
147: late int? _reciteSurah = d == null ? _recited?.surah : (d!['recite_surah'] as num?)?.toInt();
148: late final _reciteFrom = TextEditingController(text: d == null ? _recited?.from.toString() : d!['recite_from'] as String?);
149: late final _reciteTo = TextEditingController(text: d == null ? _recited?.to.toString() : d!['recite_to'] as String?);
… 47 more lines
```

### `apps/mobile/lib/features/teaching/presentation/pages/students_page.dart`

Lines: 15, 16, 192, 262, 269, 270, 271, 272, 278, 281, 282, 285, 286, 288, 289, 293, 294

```text
15: import '../../../hifz/data/hifz_repository.dart';
16: import '../../../hifz/domain/hifz.dart';
192: /// open their hifz map).
262: _HifzEntry(enrollmentId: s.enrollmentId, onOpen: after(() => context.push('/teach/students/${s.enrollmentId}/hifz'))),
269: /// The way to the student's hifz map, shown once there is a map to show
270: /// (the platform has the Quran's text).
271: class _HifzEntry extends StatefulWidget {
272: const _HifzEntry({required this.enrollmentId, required this.onOpen});
278: State<_HifzEntry> createState() => _HifzEntryState();
281: class _HifzEntryState extends State<_HifzEntry> {
282: late final Future<StudentHifz> _hifz = context.read<HifzRepository>().student(widget.enrollmentId);
285: Widget build(BuildContext context) => FutureBuilder<StudentHifz>(
… 5 more lines
```

### `apps/mobile/lib/features/teaching/presentation/pages/today_page.dart`

Lines: 90

```text
90: NextLessonCard(lesson: next, quran: true)
```

### `apps/mobile/lib/features/teaching/presentation/widgets/teacher_lessons.dart`

Lines: 77

```text
77: quran: true,
```

### `apps/mobile/pubspec.yaml`

Lines: 90, 94, 96, 98

```text
90: - assets/fonts/OFL-AmiriQuran.txt
94: # Quran's own face for its text, the class page's (OFL, see assets/fonts/OFL-AmiriQuran.txt).
96: - family: AmiriQuran
98: - asset: assets/fonts/AmiriQuran-Regular.ttf
```

### `apps/mobile/test/features/academy_modules_test.dart`

Lines: 61, 73

```text
61: final some = Modules.fromJson(['curriculum', 'quran']);
73: expect(featureAt('/family/journey/hifz'), Feature.quran);
```

### `apps/mobile/test/features/classroom_room_test.dart`

Lines: 278, 289, 291

```text
278: testWidgets('the mushaf takes the stage with the main picture small on it; a tap on it goes back', (tester) async {
289: expect(find.byKey(const Key('classroom-mushaf')), findsOneWidget);
291: await tester.tap(find.byKey(const Key('mushaf-pip')));
```

### `apps/mobile/test/features/report_questions_test.dart`

Lines: 9

```text
9: /// Pages memorised (a number, required), tajweed (a choice), revision (yes or no), a note only the academy reads.
```

### `apps/mobile/test/features/small_phone_test.dart`

Lines: 7, 303, 308, 309, 310, 311, 319, 331, 332, 334, 343, 347, 351, 352, 355, 356

```text
7: import '../fixtures/hifz.dart';
303: testWidgets('a hifz map, a page of its review and its check fit a $width dp phone with large text', (tester) async {
308: ..on('GET', 'learning/journey/map', fxJourney(stage: 'kids', viewer: 'guardian', hifz: fxHifzToday))
309: ..on('GET', 'learning/hifz', fxHifzBoard(latest: fxRecitation(status: 'ready')))
310: ..on('GET', 'learning/hifz/recitations/rc1', {'data': fxRecitation(status: 'ready')})
311: ..onWith('GET', 'learning/hifz/pages/*', (r) => (200, fxQuranPage(int.parse(r.path.split('/').last))));
319: await _go(tester, '/family/journey/hifz');
331: await tester.ensureVisible(find.byKey(const Key('hifz-latest')));
332: await tester.tap(find.byKey(const Key('hifz-latest')));
334: expect(find.byKey(const Key('recited-words')), findsOneWidget);
343: testWidgets('a student\'s hifz map and saying what they know fit a $width dp phone with large text', (tester) async {
347: app.api.on('GET', 'teacher/students/e1/hifz', fxStudentHifz());
… 4 more lines
```

### `apps/mobile/test/features/trial_cubit_test.dart`

Lines: 35, 41, 254, 264

```text
35: /// A parent for an eight-year-old in the Quran: up to the wishes.
41: ..chooseSubject('sub-quran');
254: subjectId: 'sub-quran',
264: 'subject_id': 'sub-quran',
```

### `apps/mobile/test/features/trial_test.dart`

Lines: 71, 74, 168, 190, 219, 240, 480, 489

```text
71: /// The Quran, no wishes: up to the times.
74: await _tap(tester, find.byKey(const Key('trial-subject-sub-quran')));
168: expect(asked['subject_id'], 'sub-quran');
190: await _tap(tester, find.byKey(const Key('trial-subject-sub-quran')));
219: await _tap(tester, find.byKey(const Key('trial-subject-sub-quran')));
240: 'subject_id': 'sub-quran',
480: final app = await _open(tester, helpSubject: 'sub-quran');
489: expect(app.api.sent('GET', 'site/trial-slots').single.queryParameters['subject_id'], 'sub-quran');
```

### `apps/mobile/test/fixtures/journey.dart`

Lines: 100, 295

```text
100: Map<String, Object?>? hifz,
295: 'hifz': hifz,
```

### `apps/mobile/test/fixtures/start.dart`

Lines: 9, 40

```text
9: /// A plan as `family/start/options` prices it: Tajweed, two 45-minute lessons a week, 8 in a block.
40: /// What Jana's mother may start: Jana (waiting for consent) and Omar, Tajweed (and Arabic, running already), a private
```

### `apps/mobile/test/fixtures/trial.dart`

Lines: 16

```text
16: 'id': 'sub-quran',
```

### `apps/mobile/test/fixtures/trial_report.dart`

Lines: 28

```text
28: /// Jana's Tajweed trial report, as the API answers it for her mother: the
```

## Portal (apps/web) (41 files)

### `apps/web/README.md`

Lines: 5, 6, 52, 53, 54, 58, 73, 82, 92

```text
5: - **The teacher's portal** (phase A, `/teach`): today, the week, lesson reports, marking homework (recordings play in the page), students and their roadmap, trial lessons, my hours…
6: - **The family's portal** (phase B, `/family`), for students and guardians, in the look of the person signed in, as in the app and the `/my` panel: a student's own stage (kids, mid…
52: | `src/app/[locale]/family/hifz`, `src/components/hifz`, `src/lib/hifz` | The hifz map (`GET learning/hifz`): the parts as rows of pages in their strength (`map.tsx`, the academy's…
53: | `src/app/[locale]/family/quran`, `src/app/[locale]/teach/lessons/[id]/quran`, `src/app/[locale]/teach/students/[enrollment]/quran`, `src/app/[locale]/teach/exams`, `src/component…
54: | `src/app/[locale]/certificates/[code]`, `src/components/site/certificate.tsx` | A Quran certificate's public check (`GET quran/certificates/{code}`, open in `proxy.ts`; the certi…
58: | `src/components/mushaf`, `src/lib/mushaf` | A Quran lesson's shared mushaf (`GET learning/lessons/{session}/mushaf`) in the class page (`teach/classroom.tsx`): beside the LiveKit…
73: - `components/live-refresh.tsx`: `LiveRefresh` listens for `lessons.changed`, `homework.changed`, `inbox.changed`, `payments.changed`, `practice.changed` (a round, a creature or a …
82: npm test                 # unit (vitest): days and zones, clocks in 12 or 24 hours, safe redirects, notification targets, form problems, each look's places and what it allows, the …
92: The end-to-end tests sign in (password, code, staff, a refused token, the privacy notice and terms under the portal's and every panel's sign-in), then as Khaled: every page at phon…
```

### `apps/web/e2e/backend.ts`

Lines: 55, 56, 62, 192, 195

```text
55: * The demo's Quran (docs/architecture/02, section 26; DemoQuranSeeder and
56: * E2eResetSeeder): a Quran course with a plan, its teacher's lesson whose
62: quran: {
192: /** The report's link (Arabic, English): an assessed Tajweed trial two days ago, an open offer, a second trial to book. */
195: /** Another family's "book again" link after a Quran trial its child missed yesterday. */
```

### `apps/web/e2e/pages.ts`

Lines: 7, 8, 9

```text
7: /** Every place in a look's menu (lib/family/nav-items; the demo's plan has the Quran), the menu itself and the album, under /{locale}. */
8: export function familyPages(stage: Stage, { money = false, guardian = false, quran = true } = {}): string[] {
9: return [...new Set([...itemsOf(stage, money, guardian, quran).all.map((item) => item.href), '/family/more', '/family/games/album'])];
```

### `apps/web/e2e/start-course.spec.ts`

Lines: 14

```text
14: * to the run (E2eResetSeeder::trialAfter): a 9-year-old's Tajweed trial two
```

### `apps/web/playwright.config.ts`

Lines: 50, 51

```text
50: // The Quran program (the demo's Quran course): its teacher, family and the public certificate check, each signed in apart.
51: { name: 'quran', testMatch: /quran\.spec\.ts/, dependencies: ['setup'], use: { ...devices['Pixel 7'] } },
```

### `apps/web/src/app/[locale]/family/actions.ts`

Lines: 233, 237, 239, 249, 250, 253, 257, 259

```text
233: * Says how a hifz page went (1 forgot, 2 hard, 3 good, 4 easy): the page's
237: export async function gradeHifzPage(learnerId: string, page: number, grade: number, key: string): Promise<Result> {
239: await send('post', '/v1/learning/hifz/pages/{page}/grade', {
249: * Recites a hifz page (`audio`, a recording made in the browser): it is heard
250: * and checked in the background, and the hifz signal brings the result to the
253: export async function reciteHifzPage(learnerId: string, page: number, form: FormData): Promise<Result & { id?: string; off?: boolean }> {
257: sent.set('audio', audio, audio.name || 'recitation.webm');
259: const done = await send<{ data: { id: string } }>('post', '/v1/learning/hifz/pages/{page}/recitations', { params: { page: String(page) }, form: sent });
```

### `apps/web/src/app/[locale]/family/lessons/[id]/page.tsx`

Lines: 10, 16, 17, 21, 52

```text
10: import { lessonMushaf } from '@/lib/mushaf/server';
16: * go in. A Quran lesson of a course the hifz map belongs to brings its shared
17: * mushaf, following the teacher's page.
21: const [t, f, locale, format, fam, mushaf] = await Promise.all([getTranslations('family'), getTranslations('format'), getLocale(), viewerTimeFormat(), family(), lessonMushaf(id)]);
52: mushaf={mushaf}
```

### `apps/web/src/app/[locale]/family/more/page.tsx`

Lines: 13, 20

```text
13: import { quranInPlan } from '@/lib/quran/quran';
20: const { all, tabs } = itemsOf(fam.stage, seesMoney(fam.stage), isGuardian(fam.learners), quranInPlan(modulesOf(person)), modulesOf(person));
```

### `apps/web/src/app/[locale]/teach/actions.ts`

Lines: 5, 6, 40, 41, 143, 150, 151, 156, 157, 161, 162, 167, 173, 174, 175, 178, 179, 180, 184, 185, 201, 202, 207, 208, 209, 213, 214, 217, 218, 219

```text
5: import type { MushafPage, MushafResult, WordRef } from '@/lib/mushaf/types';
6: import type { PartKey, PartRecord } from '@/lib/quran/types';
40: /** One student's record of a Quran lesson: the parts they recited. */
41: export type QuranStudentRecord = { student_id: string; parts: Partial<Record<PartKey, PartRecord>> };
143: export type HifzChoice = { juz?: number[]; surahs?: number[]; pages?: number[] };
150: export async function markHifz(enrollment: string, choice: HifzChoice, strength: 'strong' | 'good' | 'weak'): Promise<Result & { count?: number }> {
151: const done = await send<{ data: { marked: number } }>('post', '/v1/teacher/students/{enrollment}/hifz/memorized', { params: { enrollment }, body: { ...choice, strength } });
156: export async function clearHifz(enrollment: string, choice: HifzChoice): Promise<Result & { count?: number }> {
157: const done = await send<{ data: { cleared: number } }>('post', '/v1/teacher/students/{enrollment}/hifz/clear', { params: { enrollment }, body: choice });
161: function mushafOf(outcome: Outcome<{ data: MushafPage }>): MushafResult {
162: if (outcome.ok) return { ok: true, mushaf: outcome.data.data };
167: * The lesson's shared mushaf: the teacher turns its pages and marks words
… 18 more lines
```

### `apps/web/src/app/[locale]/teach/lessons/[id]/page.tsx`

Lines: 8, 9, 10, 20, 21, 22, 26, 29, 33, 34, 36, 37, 66, 79

```text
8: import { lessonMushaf } from '@/lib/mushaf/server';
9: import { dataOf, quranRead } from '@/lib/quran/server';
10: import type { LessonPortion } from '@/lib/quran/types';
20: * page loads or is prefetched. A Quran lesson of a course the hifz map
21: * belongs to brings its shared mushaf, at the page the teacher has open;
22: * one with a Quran plan, the way to its panel (the portion and its record).
26: const [t, f, q, locale, format, { data: lesson }, mushaf, quran] = await Promise.all([
29: getTranslations('quran'),
33: lessonMushaf(id),
34: quranRead<LessonPortion>('/v1/quran/lessons/{session}/portion', { params: { session: id } }).then(dataOf),
36: // A Quran lesson with a plan: its portion and record on its own page (a lesson without one, or the Quran off, shows nothing).
37: const portion = quran?.plan ? quran : null;
… 2 more lines
```

### `apps/web/src/app/[locale]/teach/marking/page.tsx`

Lines: 5, 51, 59

```text
5: import { RecitationCheck } from '@/components/teach/recitation-check';
51: {h.expected?.title ? <p className="mt-1 text-sm text-muted">{t('reciteWhat', { title: h.expected.title })}</p> : null}
59: {s.check ? <RecitationCheck check={s.check} /> : null}
```

### `apps/web/src/app/[locale]/teach/reports/[id]/page.tsx`

Lines: 8, 30, 31

```text
8: import type { Surah } from '@/lib/teach/recitation';
30: // The surahs to choose what homework asks to recite, when the form may ask it.
31: const surahs = form.assist?.recitation_check || form.homework?.expected ? (await get<{ data: Surah[] }>('/v1/teacher/texts/quran')).data : [];
```

### `apps/web/src/app/[locale]/teach/students/[enrollment]/page.tsx`

Lines: 3, 6, 9, 10, 13, 14, 17, 20, 21, 23, 29, 30, 31, 35, 37, 38, 43, 45, 46, 48, 63, 75, 76, 79

```text
3: import { TeacherHifzSection } from '@/components/hifz/teacher';
6: import { MistakesNotebook } from '@/components/mushaf/notebook';
9: import type { TeacherHifz } from '@/lib/hifz/types';
10: import { teacherNotebook } from '@/lib/mushaf/server';
13: import { dataOf, quranRead } from '@/lib/quran/server';
14: import type { StudentPlan } from '@/lib/quran/types';
17: * The student's hifz map, on a course it follows (the curriculum reads the Quran, or pages are on the map already). An extra on the
20: async function hifzOf(enrollment: string): Promise<TeacherHifz | null> {
21: const response = await call('get', '/v1/teacher/students/{enrollment}/hifz', { params: { enrollment } }).catch(() => null);
23: const { data } = (await response.json()) as { data: TeacherHifz };
29: * here, or still to come; then their hifz map and, with it, their mistakes
30: * notebook (the words marked in their lessons' shared mushaf); a course
… 12 more lines
```

### `apps/web/src/app/globals.css`

Lines: 39, 40, 44

```text
39: * The Quran's words (the shared mushaf, the mistakes notebook) in Amiri Quran,
40: * whose variable only those parts carry (components/mushaf/font.ts); inline,
44: --font-quran: var(--font-amiri-quran), 'Amiri Quran', serif;
```

### `apps/web/src/components/family/homes.tsx`

Lines: 3, 142, 198

```text
3: import { HifzCard } from '@/components/hifz/card';
142: /** A guardian's (or an adult student's) home: the next lesson, each course's balance and what is owed, the journey's card (and today's hifz review), homework, and notices. */
198: {journey?.hifz ? <HifzCard hifz={journey.hifz} /> : null}
```

### `apps/web/src/components/family/nav.tsx`

Lines: 16, 23

```text
16: export function SideNav({ stage, money, guardian = false, quran = false, modules, unread, chats }: { stage: Stage; money: boolean; guardian?: boolean; quran?: boolean; modules?: re…
23: {itemsOf(stage, money, guardian, quran, modules).all.map((item) => (
```

### `apps/web/src/components/family/shell.tsx`

Lines: 13, 34, 47

```text
13: import { quranInPlan } from '@/lib/quran/quran';
34: const quran = quranInPlan(modules);
47: <SideNav stage={fam.stage} money={money} guardian={guardian} quran={quran} modules={modules} unread={live.unread} chats={live.chats} />
```

### `apps/web/src/components/journey/calm.tsx`

Lines: 23, 56

```text
23: export function CalmJourney({ map, title, autoplay, look, hifz }: { map: JourneyMap; title: string; autoplay: PlayTarget | null; look: string; hifz?: ReactNode }) {
56: {hifz}
```

### `apps/web/src/components/journey/guardian.tsx`

Lines: 25, 65

```text
25: export function GuardianJourney({ map, learnerName, autoplay, hifz }: { map: JourneyMap; learnerName: string; autoplay: PlayTarget | null; hifz?: ReactNode }) {
65: {hifz}
```

### `apps/web/src/components/journey/kids.tsx`

Lines: 57, 64, 65, 396

```text
57: export function KidsJourney({ map, learnerName, autoplay, openIsland, hifz }: {
64: /** Today's hifz review, when the learner has a hifz map. */
65: hifz?: ReactNode;
396: {hifz}
```

### `apps/web/src/components/journey/middle.tsx`

Lines: 22, 86

```text
22: export function MiddleJourney({ map, learnerName, autoplay, hifz }: { map: JourneyMap; learnerName: string; autoplay: PlayTarget | null; hifz?: ReactNode }) {
86: {hifz}
```

### `apps/web/src/components/journey/screen.tsx`

Lines: 2, 28, 47, 49, 69, 71, 73, 75

```text
2: import { HifzCard } from '@/components/hifz/card';
28: * an island (back from the album). With pages on the learner's hifz map, a
47: const hifz = (
49: {map.hifz ? <HifzCard hifz={map.hifz} kids={look === 'kids'} /> : null}
69: <KidsJourney key={learner.id} map={map} learnerName={name} autoplay={autoplay} openIsland={island ?? null} hifz={hifz} />
71: <MiddleJourney key={learner.id} map={map} learnerName={name} autoplay={autoplay} hifz={hifz} />
73: <GuardianJourney key={learner.id} map={map} learnerName={name} autoplay={autoplay} hifz={hifz} />
75: <CalmJourney key={learner.id} map={map} title={t('mine')} autoplay={autoplay} look={fam.stage} hifz={hifz} />
```

### `apps/web/src/components/live-refresh.tsx`

Lines: 21, 174

```text
21: * shared mushaf's) leave the page alone.
174: * changes (the mistakes notebook: the words marked in the shared mushaf)
```

### `apps/web/src/components/room/room.tsx`

Lines: 36

```text
36: /** The side panel (the shared mushaf), with its name, when the lesson has one. */
```

### `apps/web/src/components/teach/classroom.tsx`

Lines: 9, 13, 29, 30, 37, 43, 49, 55, 56, 91, 102, 103, 106, 113, 125, 140

```text
9: import type { MushafPage } from '@/lib/mushaf/types';
13: import { Mushaf } from '@/components/mushaf/mushaf';
29: * room's "more", once everyone it records agreed. A Quran lesson of a course
30: * the hifz map belongs to has its shared mushaf: the room's side panel (in
37: mushaf: first = null,
43: mushaf?: MushafPage | null;
49: const m = useTranslations('mushaf');
55: // The mushaf as last drawn, so it starts from there when the room opens or closes around it.
56: const [mushaf, setMushaf] = useState(first);
91: panel={mushaf ? { name: m('title'), content: <Mushaf initial={mushaf} onChange={setMushaf} fill readOnMount /> } : null}
102: const withMushaf = (card: ReactNode) =>
103: mushaf ? (
… 4 more lines
```

### `apps/web/src/components/teach/report-editor.tsx`

Lines: 11, 16, 30, 66, 67, 68, 69, 188, 239, 417, 455, 456, 459, 460, 461, 462

```text
11: import { RecitationField } from '@/components/teach/recitation-field';
16: import { expectedPayload, recitable, suggestionsOf, type Expected, type Surah } from '@/lib/teach/recitation';
30: * voice may say what to recite, for a check of each recording. The API checks
66: // What to recite: asked while the helper is on, or the homework already says (its passage, else the lesson's).
67: const reciteOffered = surahs.length > 0 && (Boolean(form.assist?.recitation_check) || Boolean(hw?.expected));
68: const [reciteOn, setReciteOn] = useState(Boolean(hw?.expected));
69: const [recite, setRecite] = useState<Partial<Expected>>(hw?.expected ?? form.expected_suggestion ?? form.mistakes_suggestion ?? {});
188: ? { title: title.trim(), instructions: instructions.trim() || null, accepts, due_days: dueDays, ...expectedPayload(reciteOffered, reciteOn, accepts, recite) }
239: ? { title: title.trim(), instructions: instructions.trim() || null, accepts, due_days: dueDays, ...expectedPayload(reciteOffered, reciteOn, accepts, recite) }
417: {hw.expected?.title ? <p className="mt-1 text-sm text-muted">{t('reciteWhat', { title: hw.expected.title })}</p> : null}
455: {reciteOffered && recitable(accepts) ? (
456: <RecitationField
… 4 more lines
```

### `apps/web/src/lib/actions/shared.ts`

Lines: 6, 23, 306, 310, 311, 313

```text
6: import type { MushafPage, MushafResult } from '@/lib/mushaf/types';
23: * lesson's shared mushaf read again (its teacher's page, or another a learner
306: * A lesson's shared mushaf as it stands: the page asked for, else the one the
310: export async function readMushaf(session: string, page?: number): Promise<MushafResult> {
311: const done = await read<{ data: MushafPage }>('/v1/learning/lessons/{session}/mushaf', { params: { session }, query: { page } });
313: return { ok: true, mushaf: done.data.data };
```

### `apps/web/src/lib/api/server.ts`

Lines: 138

```text
138: * a part of a page only some records have (a lesson's mushaf), or a Server
```

### `apps/web/src/lib/family/family.test.ts`

Lines: 84, 86, 88, 90, 91, 210, 241, 242, 243

```text
84: it('has the Quran’s page only while the academy’s plan has it, after messages and never as a tab', () => {
86: expect(itemsOf(stage, seesMoney(stage)).all.some((i) => i.key === 'quran')).toBe(false);
88: const at = all.findIndex((i) => i.key === 'quran');
90: expect(tabs.some((i) => i.key === 'quran')).toBe(false);
91: expect(isAt(all[at]!, '/family/hifz/12')).toBe(true);
210: const ALL = ['messaging', 'support', 'curriculum', 'games', 'evaluation', 'quran'];
241: it('drops the Quran when its module is off even if asked for', () => {
242: expect(keys(itemsOf('classic', true, false, true, without('quran')).all)).not.toContain('quran');
243: expect(keys(itemsOf('classic', true, false, true, ALL).all)).toContain('quran');
```

### `apps/web/src/lib/family/nav-items.ts`

Lines: 24, 25, 32, 36, 48, 49, 71, 76, 80

```text
24: * the academy's plan has the Quran (`quran`), everyone has its page (the
25: * plan, the hifz map, exams, certificates) after messages, so the tabs stay.
32: * journey the curriculum's, the Quran the Quran's. An area that is off leaves
36: export function itemsOf(stage: Stage, money: boolean, guardian = false, quran = false, modules?: readonly string[] | null): { all: NavItem[]; tabs: NavItem[] } {
48: // The Quran (its page, and the hifz map under it): only while the academy's plan has it.
49: const quranItems: NavItem[] = quran && on('quran') ? [{ href: '/family/quran', key: 'quran', icon: 'book', also: ['/family/hifz'] }] : [];
71: all: [home, lessons, ...journeyItems, ...messageItems, ...quranItems, homework, ...pay, ...start, inbox, trials, ...recordings, ...privacy, ...help, tellUs, ...account, myData],
76: return { all: [home, lessons, homework, progress, ...messageItems, ...quranItems, inbox, trials, ...recordings, ...help, tellUs, ...account], tabs: [home, lessons, homework, progre…
80: all: [home, lessons, ...messageItems, ...quranItems, homework, progress, inbox, trials, ...recordings, ...help, tellUs, ...account],
```

### `apps/web/src/lib/journey/journey.test.ts`

Lines: 63, 86, 105

```text
63: subject: 'Quran',
86: title: 'Recite',
105: title: 'Quran',
```

### `apps/web/src/lib/journey/types.ts`

Lines: 4, 196, 197

```text
4: import type { JourneyHifz } from '../hifz/types';
196: /** Today's hifz review (pages left, done today, a day's pages); null until the learner has pages on their hifz map. */
197: hifz?: JourneyHifz | null;
```

### `apps/web/src/lib/live.test.ts`

Lines: 67, 68, 71, 72, 73, 75, 76, 83, 84, 85, 87, 88

```text
67: it('include the hifz map’s: a page reviewed, marked, or recited and then heard', () => {
68: expect(SIGNALS).toContain('hifz.changed');
71: it('include the shared mushaf’s, which its screen follows by itself instead of refreshing the page', () => {
72: expect(SIGNALS).toContain('mushaf.changed');
73: expect(refreshesPage('mushaf.changed')).toBe(false);
75: expect(refreshesPage('hifz.changed')).toBe(true);
76: expect(SIGNALS.filter(refreshesPage)).not.toContain('mushaf.changed');
83: expect(concerns('mushaf.changed', ['mushaf.changed'])).toBe(true);
84: expect(concerns('lessons.changed', ['mushaf.changed'])).toBe(false);
85: expect(concerns(RESYNC, ['mushaf.changed'])).toBe(true);
87: expect(concerns(undefined, ['mushaf.changed'])).toBe(false);
88: expect(concerns({ name: 'mushaf.changed' }, ['mushaf.changed'])).toBe(false);
```

### `apps/web/src/lib/live.ts`

Lines: 15, 16, 17, 19, 25, 28

```text
15: * creatures, a guardian's limits); the hifz map and its daily review follow
16: * hifz (a page reviewed, marked, or recited and then heard); a lesson's
17: * shared mushaf follows mushaf (its page turned, a word marked).
19: export const SIGNALS = ['lessons.changed', 'homework.changed', 'inbox.changed', 'payments.changed', 'consents.changed', 'tickets.changed', 'privacy.changed', 'concerns.changed', 'c…
25: * is not refreshed for them: the shared mushaf turns its pages many times a
28: export const OWN_SIGNALS: readonly Signal[] = ['mushaf.changed'];
```

### `apps/web/src/lib/modules.ts`

Lines: 18, 63, 73, 74

```text
18: | 'quran'
63: ['/teach/exams', 'quran'],
73: ['/family/quran', 'quran'],
74: ['/family/hifz', 'quran'],
```

### `apps/web/src/lib/report-answers.test.ts`

Lines: 9

```text
9: { key: 'f2', label: 'Tajweed', type: 'choice', required: false, family: true, options: [{ key: 'o1', label: 'Excellent' }], min: null, max: null, unit: null },
```

### `apps/web/src/lib/site/trial.test.ts`

Lines: 31, 52, 146, 152

```text
31: const family: TrialSettings = { booking: 'family', response_hours: 4, notice_hours: 3, help_choose_subject: true, help_choose_subject_id: 'quran' };
52: expect(bookingSubject(family, draft({ helpChoose: true }))).toBe('quran');
146: const event = { utc: '2026-11-01T16:30:00Z', minutes: 30, title: 'Free trial lesson: Quran, Hifz; Noor', details: 'With Mona' };
152: expect(ics).toContain('SUMMARY:Free trial lesson: Quran\\, Hifz\\; Noor\r\n');
```

### `apps/web/src/lib/teach/areas.test.ts`

Lines: 12, 13

```text
12: it('shows the Quran’s exams only when the plan includes the Quran', () => {
13: expect(inPlan('/teach/exams', ['quran'])).toBe(true);
```

### `apps/web/src/lib/teach/areas.ts`

Lines: 6

```text
6: * exams the Quran's, messages messaging's, help support's, performance
```

### `apps/web/src/lib/teach/types.ts`

Lines: 86, 102, 103, 123, 183, 184, 185, 187

```text
86: import type { Expected, RecitationCheck } from './recitation';
102: /** The recording's check against what the homework asks to recite (teacher answers only; null: none). */
103: check?: RecitationCheck | null;
123: /** What it asks to recite, checked word by word for the teacher (teacher answers only; null: nothing). */
183: /** Helpers the academy turned on for this report: a draft from a voice note (POST teacher/reports/{report}/draft), and the recitation check. */
184: assist?: { voice_draft: boolean; recitation_check?: boolean };
185: /** The passage of the report's lessons' text, to start what to recite from (null: none). */
187: /** The verses with the words marked in the lesson's shared mushaf (null: none marked). */
```

### `apps/web/src/proxy.ts`

Lines: 12

```text
12: * (the locale's root and /platform, whose own page decides, a Quran
```

## Repo, CI, infra, docs (11 files)

### `.github/workflows/academy-new.yml`

Lines: 68, 134

```text
68: description: Areas of the plan taken away, comma-separated (e.g. quran,ai); optional
134: [[ "$FEATURES_OFF" =~ ^[a-z_,\ ]*$ ]] || bad "Areas taken away: names separated by commas (quran,ai)."
```

### `.github/workflows/deploy.yml`

Lines: 159

```text
159: academy='{"slug":"rehearsal","name_ar":"أكاديمية التجربة","name_en":"Rehearsal","country":"QA","currency":"QAR","timezone":"Asia/Qatar","locale":"ar","owner_name":"Rehearsal Owner"…
```

### `.github/workflows/web.yml`

Lines: 111, 112

```text
111: # The Quran's text (Tanzil's files, checked), so the demo comes with its Quran program (quran.spec.ts).
112: php artisan quran:text --fetch
```

### `README.md`

Lines: 303

```text
303: في الديمو مواد على دروس يوسف وزياد ومريم: ورقة متابعة PDF، وتسجيل، ولينك للسورة على quran.com، ودليل للمدرسين بس. الملفات اتعملت في الـ seeder نفسه.
```

### `docs/architecture/03-technical-architecture.md`

Lines: 503, 504, 505, 506

```text
503: - **اللي جنب الغرفة** (المصحف المشترك في حصة القرآن، بتاع موديول القرآن؛ 02، القسم 26): Classroom بيسأل `SharedKernel\Quran\LessonQuran::classPanel` (الافتراضي `NoLessonQuran` مابي…
504: - صفحة الحصة بتعرضه في الجنب، وطلباته `GET`/`POST class/{session}/mushaf` عند Quran، بنفس الشخص (الدخول أو اللينك الموقّع، عن طريق `Classroom\Contracts\ClassPage::viewer`)، والقرآن…
505: - **LiveKit**: بعد ما التغيير يتحفظ، المدرّس بيبعت `{v:1}` على topic ‏`mushaf` (reliable)، والباقيين بيعيدوا القراية. الرسالة بتتقبل بس من مشارك الـ metadata بتاعته `role=teacher`،…
506: - **القناة** `private-lesson.{session}` (قناة الحصة بتاعة Classroom: `ClassPage::channel`؛ والقرآن بيبعت عليها `LessonMushafChanged`، `mushaf.changed`، من غير بيانات) لأصحاب المقاع…
```

### `docs/architecture/04-design-patterns.md`

Lines: 48, 69, 111

```text
48: | M15و | **Quran** | كل حاجة للقرآن: نسخة المنصة من نصه، وخريطة الحفظ وورد مراجعتها، والمصحف المشترك في الحصة وكشكول الأخطاء، وتصحيح التسميع، ومقاطع الدروس، والبرامج والخطط، والاخت…
69: Quran --> Learning & Enrollment & People & Catalog & Scheduling & Classroom & Identity & Communication & Platform
111: - **المنفّذ دلوقتي (القرآن)**: Quran فوق ومحدش بيعتمد عليه (الـ arch test بيمنع أي module تحته يلمسه، و`Quran\Domain` حساب صافي: الحفظ المتباعد، والبرامج ومقدار الحصة، والتقدير، من…
```

### `docs/testing/ACCEPTANCE.md`

Lines: 406, 3761, 4144, 4166, 4184, 4202, 4223, 4243, 4332, 4472, 4534, 4553, 4568, 6105, 6124, 6145, 6164, 6782, 7289

```text
406: <sub>المرجع: CLAUDE.md AI helpers (QuranText, QuranSource)</sub>
3761: <sub>المرجع: CLAUDE.md Hifz map</sub>
4144: <sub>المرجع: CLAUDE.md Shared mushaf and mistakes notebook</sub>
4166: <sub>المرجع: CLAUDE.md Shared mushaf (MarkMistake/UnmarkMistake)</sub>
4184: <sub>المرجع: CLAUDE.md Shared mushaf</sub>
4202: <sub>المرجع: CLAUDE.md Shared mushaf (open until report or a day after)</sub>
4223: <sub>المرجع: CLAUDE.md Shared mushaf; App</sub>
4243: <sub>المرجع: CLAUDE.md Shared mushaf (MistakesBook)</sub>
4332: <sub>المرجع: CLAUDE.md Shared mushaf (mistakes_suggestion); AI helpers (homework.expected)</sub>
4472: <sub>المرجع: CLAUDE.md AI helpers (RecitationPresenter teacher only)</sub>
4534: <sub>المرجع: CLAUDE.md Hifz map (MarkMemorized)</sub>
4553: <sub>المرجع: CLAUDE.md Hifz map (ClearHifzPages)</sub>
… 7 more lines
```

### `docs/testing/cases.json`

Lines: 463, 4148, 4567, 4591, 4611, 4631, 4654, 4676, 4771, 4923, 4991, 5012, 5031, 6752, 6773, 6796, 6817, 7487, 8064

```text
463: "rule": "CLAUDE.md AI helpers (QuranText, QuranSource)"
4148: "rule": "CLAUDE.md Hifz map"
4567: "rule": "CLAUDE.md Shared mushaf and mistakes notebook"
4591: "rule": "CLAUDE.md Shared mushaf (MarkMistake/UnmarkMistake)"
4611: "rule": "CLAUDE.md Shared mushaf"
4631: "rule": "CLAUDE.md Shared mushaf (open until report or a day after)"
4654: "rule": "CLAUDE.md Shared mushaf; App"
4676: "rule": "CLAUDE.md Shared mushaf (MistakesBook)"
4771: "rule": "CLAUDE.md Shared mushaf (mistakes_suggestion); AI helpers (homework.expected)"
4923: "rule": "CLAUDE.md AI helpers (RecitationPresenter teacher only)"
4991: "rule": "CLAUDE.md Hifz map (MarkMemorized)"
5012: "rule": "CLAUDE.md Hifz map (ClearHifzPages)"
… 7 more lines
```

### `infra/deploy/README.md`

Lines: 168, 169

```text
168: alert mail says when one needs someone (`RUNBOOKS.md`, "An outside service needs you"). The Quran's text is fetched from Tanzil by the deploy
169: (`QURAN_TEXT_URL`, `QURAN_DATA_URL`, not written: Tanzil's own addresses) or from the same page.
```

### `infra/deploy/RUNBOOKS.md`

Lines: 310, 341, 349, 350, 351, 420, 422, 423, 425, 428, 429, 434, 435, 439, 440, 576, 595

```text
310: The academies' helpers (practice items, report drafts from a teacher's voice note, recitation checks,
341: - **Before an academy turns on the recitation check**: measure it on real recordings whose mistakes a
349: docker compose cp ./recitations web:/tmp/recitations
350: docker compose exec web php artisan quran:try-recitation /tmp/recitations
351: docker compose exec web rm -r /tmp/recitations
420: ## The Quran's text
422: The Quran's words (lesson passages, practice suggestions) come only from Tanzil's Simple text and its
423: metadata, kept in the storage volume (`storage/app/platform/quran`, with `manifest.json`: their SHA-256 and
425: (`quran:text --fetch --if-missing`; `curriculum:quran` is its older name); a deploy that could not reach Tanzil says so and goes on.
428: docker compose exec web php artisan quran:text            # which copy, its version and checksums
429: docker compose exec web php artisan quran:text --fetch    # fetch again (or the console: Platform settings › "Fetch again")
434: Tanzil's addresses are `QURAN_TEXT_URL` and `QURAN_DATA_URL` in `.env` should they move. Until a copy is
… 5 more lines
```

### `infra/deploy/deploy.sh`

Lines: 273, 395, 397, 398, 399, 406

```text
273: # Speech to text for the helpers that listen (a teacher's voice note, a recitation):
395: # The Quran's text: fetched from Tanzil once and checked whole, then kept in the storage volume (and its backups).
397: say "The Quran's text (only if the server has no copy yet)"
398: compose run --rm --no-deps -T web php artisan quran:text --fetch --if-missing \
399: || say "The Quran's text was not fetched this time; fetch it from the console (Platform settings) or: php artisan quran:text --fetch"
406: # A demo already there takes what later versions of it add (its Quran lessons' surahs, marked words and hifz maps once
```
