# Gnosis

Gnosis is a student-focused university application assistant built for exploration, planning, writing support, and guided preparation. The app combines school matching, AI essay coaching, application tracking, document readiness, mentor booking, and dynamically generated IELTS practice into one mobile-first experience.

## Features

### Core student workflow
- **Onboarding flow** for collecting student profile details.
- **Home dashboard** for quick access to major actions.
- **School matching** to explore recommended schools based on profile data.
- **AI Essay Coach** for university application writing, strategy, and guidance.
- **Community page** for social or collaborative student interactions.
- **Timeline page** for tracking tasks, deadlines, and next steps.
- **Documents page** for monitoring required uploads and readiness.
- **More page** for profile snapshot, saved schools, applications, CV builder, mentor support, and reset actions.

### Added mentor and IELTS functions
- **Mentor Matching** under CV Builder.
- Students can click a button, choose a time, and submit a mentor request.
- After submission, the app shows an alert message confirming that a mentor is being matched.
- **Personalized Practice for IELTS** under Mentor Matching.
- Clicking the button opens a new IELTS practice page.
- The IELTS page dynamically generates **20 multiple-choice questions** focused on:
  - IELTS exam format
  - Understanding of the exam
  - Concepts that improve performance

### IELTS practice behavior
- Questions are generated dynamically when the page loads.
- If AI generation fails, the page falls back to a local built-in 20-question practice set.
- Students can:
  - Answer questions
  - Submit answers
  - View explanations
  - Reset answers
  - Generate a new question set

## Tech Stack

- **React**
- **React Router**
- **Vite**
- **Tailwind CSS** or utility-based styling already used in the project
- **Lucide React** icons
- **OpenRouter API** for AI generation
- Browser local storage utilities for demo persistence

## Main Pages

- `/` — Onboarding
- `/home` — Home page
- `/match` — School matching
- `/ai-agent` — AI Essay Coach
- `/community` — Community
- `/timeline` — Timeline
- `/documents` — Documents
- `/more` — More page
- `/ielts-practice` — IELTS personalized practice

## Project Structure

A typical structure for this project is:

```bash
src/
  components/
    AppShell.jsx
    EmptyState.jsx
    PageHeader.jsx
    ui.jsx
  lib/
    helpers.js
    openai.js
    storage.js
  pages/
    AIAgentPage.jsx
    CommunityPage.jsx
    DocumentsPage.jsx
    HomePage.jsx
    IELTSPracticePage.jsx
    MatchPage.jsx
    MorePage.jsx
    OnboardingPage.jsx
    TimelinePage.jsx
  App.jsx
  main.jsx
```

## Installation

### 1. Clone the project

```bash
git clone <your-repo-url>
cd <your-project-folder>
```

### 2. Install dependencies

```bash
npm install
```

### 3. Start development server

```bash
npm run dev
```

The local app usually runs at:

```bash
http://localhost:5173
```

## Environment Setup

If you want to use environment variables instead of hardcoding values, create a `.env` file in the project root:

```env
VITE_SITE_URL=http://localhost:5173
VITE_SITE_NAME=Gnosis
VITE_OPENROUTER_API_KEY=your_openrouter_api_key
VITE_OPENROUTER_MODEL=stepfun/step-3.5-flash:free
```

## OpenRouter Integration

The app uses an OpenRouter-compatible chat completions endpoint for:
- AI Essay Coach replies
- Streaming essay responses
- Dynamic IELTS quiz generation

Example constants in `src/lib/openai.js`:

```js
const OPENROUTER_API_URL = "https://openrouter.ai/api/v1/chat/completions";
const OPENROUTER_API_KEY = "YOUR_OPENROUTER_API_KEY_HERE";
const OPENROUTER_MODEL = "stepfun/step-3.5-flash:free";
const SITE_URL =
  import.meta.env.VITE_SITE_URL ||
  window.location.origin ||
  "http://localhost:5173";
const SITE_NAME = import.meta.env.VITE_SITE_NAME || "Gnosis";
```

> **Important:** For safety, do not publish real API keys in a public repository.

## Routing

The app uses protected routes after onboarding is complete.

Example route setup:

- `/` → onboarding
- protected routes:
  - `/home`
  - `/match`
  - `/ai-agent`
  - `/community`
  - `/timeline`
  - `/documents`
  - `/more`
  - `/ielts-practice`

## More Page Additions

The **More** page includes:

### Profile Snapshot
- Student profile summary
- Completion progress
- Basic student information

### Saved Schools
- Displays bookmarked schools
- Shows match category badges such as Safe, Match, or Reach

### Applications
- Displays applied schools
- Shows status, date, deadline, and tuition
- Supports canceling an application

### CV Builder
- Opens a modal form
- Lets students edit:
  - full name
  - email
  - phone
  - city
  - summary
  - education
  - experience
  - activities
  - awards
  - skills
- Saves CV data
- Marks `CV Resume` as complete in the documents list

### Mentor Support
Includes two new cards:

#### Mentor Matching
- Book sessions with vetted mentors
- Choose a preferred time
- Submit request
- Shows an alert such as:

```text
Your mentor session request for [time] has been submitted. We are finding a suitable mentor for you now. Please wait quietly for our reply.
```

#### Personalized Practice for IELTS
- Opens the IELTS practice page
- Provides dynamically generated MC questions

## IELTS Practice Page

The `IELTSPracticePage.jsx` supports:

- Automatic question generation on page load
- Loading state while generating
- AI fallback handling
- Local fallback questions if generation fails
- Score calculation
- Explanation display after submission
- Reset answers
- Generate a new set

### Question format
Each question follows this structure:

```js
{
  id: 1,
  question: "Question text",
  options: ["A", "B", "C", "D"],
  answer: 0,
  explanation: "Explanation text"
}
```

## Local Storage / Demo Persistence

The app stores demo data locally for convenience. This may include:
- onboarding completion
- profile data
- saved schools
- applications
- tasks
- documents
- CV data

A reset action is available in the More page to clear local demo data.

## AI Functions in `src/lib/openai.js`

Typical exported functions include:

### `canUseRealAI()`
Checks whether a usable API key exists.

### `getEssayCoachReply(messages, profile)`
Gets a non-streamed essay coach response.

### `streamEssayCoachReply(messages, profile, onDelta)`
Streams an essay coach response incrementally.

### `generateIeltsQuiz(profile)`
Generates a 20-question IELTS multiple-choice quiz in JSON format.

## Expected JSON Quiz Shape

The AI is prompted to return:

```json
{
  "questions": [
    {
      "id": 1,
      "question": "What is IELTS?",
      "options": ["A", "B", "C", "D"],
      "answer": 0,
      "explanation": "Explanation here"
    }
  ]
}
```

## Error Handling Notes

The project includes handling for:
- failed OpenRouter requests
- empty AI content
- invalid quiz JSON
- missing API key
- unavailable streaming response body
- fallback local IELTS question set

## Recommended Development Notes

- Keep API keys out of public repositories.
- Prefer environment variables for deployable builds.
- For demo or local testing, a placeholder fixed constant may still be used temporarily.
- If AI-generated quiz output format changes, update the normalization logic in `openai.js`.

## Scripts

Typical scripts in `package.json`:

```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  }
}
```

## Example Workflow

1. Complete onboarding.
2. Open Home page.
3. Explore school matching.
4. Use AI Essay Coach for application writing help.
5. Save schools and apply.
6. Track timeline and documents.
7. Open More page.
8. Build CV.
9. Book mentor session.
10. Start IELTS personalized practice.
11. Answer generated MC questions and review explanations.

## Notes

This project is designed as a student application support experience with a mobile-friendly interface and AI-assisted study workflow.

If you are testing locally and not publishing the project, you can use a temporary test configuration. However, once the project is shared, API credentials should be moved to environment variables immediately.

## License

For internal testing, demo, or educational prototyping only unless you define your own license.
