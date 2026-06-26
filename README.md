⌨️ BM Typing Test V2
A web-based typing speed trainer built for Back Market BPO teams. Tracks WPM, accuracy, and progress across agents, teams, and languages — with a live race mode and a full admin panel.
🔗 Live app: https://aitormaa.github.io/BPOtypingV2/
⚙️ Admin panel: https://aitormaa.github.io/BPOtypingV2/?admin=backmarket2026
✨ Features
For Learners

    🌱 / 📘 Level filter — toggle between Beginner and Intermediate tests
    🌐 Language filter — filter tests by language (English, Spanish, French, etc.)
    🏆 Personal best badge on each test card — see your best WPM, grade, and accuracy at a glance
    ⏱️ Configurable test durations (30s → 3 min)
    🎯 Real-time WPM, accuracy, and error tracking while typing
    🏅 Badge & streak system — earn achievements as you improve
    📈 WPM progress chart (last 15 attempts) on your profile
    🏎️ Live race mode — compete in real time against teammates

For Admins
Tab	What you can do
Tests	Add / edit / toggle / feature tests. Set level, language, category, duration, and text
Results	Filter by team, test, and date range (All / 30d / 7d). View language column. Export CSV
Learners	Filter by team. Click any learner name to see their full history + stats. Export per-learner CSV
Leaderboard	Sort by WPM or Score. Filter by team. Team Summary table with avg WPM, avg accuracy, and A-grade rate
Races	Create race rooms with a shareable 6-character code. Start / end races live
Teams	Add teams with custom colours. Teams appear as a self-select dropdown at sign-in
🔗 Access Links
Who	Link
Learners	https://aitormaa.github.io/BPOtypingV2/
Admins	https://aitormaa.github.io/BPOtypingV2/?admin=backmarket2026

    ⚠️ Keep the admin URL private — share only with team leads and trainers.

🧑‍💻 How it works
Learner flow

    Go to the learner link
    Enter your name and Back Market email
    Select your team from the dropdown
    Pick a test (filter by level and/or language)
    Type the passage — WPM and accuracy update in real time
    See your grade, score, and any new badges earned
    Results are saved automatically to Firestore

Admin flow

    Go to the admin link
    Navigate tabs: Tests → Results → Learners → Leaderboard → Races → Teams
    All data exports via the ⬇ CSV button on each relevant tab

Race flow (Admin)

    Admin → Races → select a test → + Create Race → copy the 6-character code
    Share code with agents; they enter it on the learner page (🏎️ Race button)
    Once all players have joined → 🚀 Start — everyone types simultaneously
    Podium appears automatically when all players finish

🏆 Grading Scale
Score = WPM × Accuracy
Grade	Beginner	Intermediate
A	≥ 50	≥ 58
B	≥ 42	≥ 49
C	≥ 35	≥ 42
D	≥ 28	≥ 36
F	< 28	< 36
🏅 Badges
Badge	Condition
🎯 First Steps	Complete your first test
💨 Speed Demon	Score 50+
🚀 Rocket	Score 70+
⚡ Lightning	Score 80+
💎 Perfect	100% accuracy
🔟 Dedicated	10 attempts
🏋️ Grinder	25 attempts
🔥 On Fire	3-day streak
🌟 Week Warrior	7-day streak
🏆 Elite	Achieve grade A
👑 Champion	#1 on leaderboard
🏎️ Speed Racer	Finish a race
🛠️ Tech Stack
Layer	Technology
Frontend	Vanilla HTML / CSS / JavaScript (no framework)
Database	Firebase Firestore
Hosting	GitHub Pages
Auth	Email-based (no password — Firestore lookup)
🚀 Deployment
This is a single-file app (index.html). No build step required.
First-time setup

    Fork or clone this repo
    Enable GitHub Pages: Settings → Pages → Deploy from branch → main → / (root)
    The app will be live at https://<your-username>.github.io/<repo-name>/

Updating the app

# Edit index.html locally, then:
git add index.html
git commit -m "your change description"
git push

GitHub Pages auto-deploys within ~1 minute.
Firebase
The app uses a shared Firebase Firestore project. If you need your own isolated instance:

    Create a project at https://console.firebase.google.com
    Enable Firestore in Native mode
    Replace the firebase.initializeApp({...}) config object at the bottom of index.html with your own project credentials

📁 Data Structure (Firestore)

/tests/{testId}
  title, text, level, language, category, duration, active, createdAt

/learners/{learnerId}
  name, email, teamId, createdAt, lastSeen

/results/{resultId}
  learnerId, learnerName, testId, testTitle, wpm, acc, score, grade,
  level, language, time, errors, status (completed|abandoned), createdAt

/teams/{teamId}
  name, color, createdAt

/races/{raceId}
  code, testId, testTitle, text, level, time, status, createdAt
  /players/{learnerId}
    name, progress, wpm, done, rank, finishedAt

/settings/app
  featuredTestId

📊 CSV Exports
All exports include a date suffix (e.g. results_all-teams_2026-06-26.csv).
Export	Available from	Columns
Results	Results tab	Learner, Team, Test, Language, Level, WPM, Accuracy(%), Score, Grade, Status, Time(s), Errors, Date
Leaderboard	Leaderboard tab	Rank, Learner, Team, Test, Language, Level, WPM, Accuracy(%), Score, Grade
Learner history	Click learner name in Learners tab	Test, Language, WPM, Accuracy(%), Score, Grade, Status, Time(s), Errors, Date
🔒 Admin Access
The admin panel is protected by a URL parameter:

?admin=backmarket2026

Do not share this URL publicly. To change the password, search for backmarket2026 in index.html and replace with a new value.
Built for Back Market BPO training by Aitor.
