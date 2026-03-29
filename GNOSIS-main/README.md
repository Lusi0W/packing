# Gnosis Admission Assistant

A React-based university application assistant that helps students manage onboarding, university matching, application timelines, documents, community posts, and AI essay coaching.

<p align="center">
  <img alt="React" src="https://img.shields.io/badge/React-Frontend-61DAFB?logo=react&logoColor=white">
  <img alt="Router" src="https://img.shields.io/badge/React_Router-Navigation-CA4245?logo=reactrouter&logoColor=white">
  <img alt="Storage" src="https://img.shields.io/badge/Storage-localStorage-6B7280">
  <img alt="Status" src="https://img.shields.io/badge/Status-Portfolio%20Project-8B5CF6">
  <img alt="License" src="https://img.shields.io/badge/License-Educational-lightgrey">
</p>

## Overview

Gnosis Admission Assistant is a student-focused web application designed to support the university application journey from profile setup to task planning, document tracking, and essay preparation.

The app includes a guided onboarding flow, university matching, application timeline management, document readiness tracking, community interaction, and an AI essay coach interface. It is built as a front-end project with browser localStorage persistence, which makes it suitable for demos, portfolio presentation, and future backend expansion.

## Features

- Multi-step onboarding flow
- Personalized university matching
- Timeline and task management
- Document vault and readiness tracking
- Community posts and interactions
- AI essay coach chat experience
- localStorage-based persistence
- Mobile-friendly app-style interface

## Pages

### Onboarding
Users complete a multi-step onboarding flow with personal details, academic background, major preferences, target countries, and dream school information.

### Home
The dashboard displays readiness status, profile progress, upcoming tasks, notifications, and quick navigation actions.

### Match
Users can search and filter universities, review match results, and explore schools based on profile preferences.

### Timeline
Users can manage application tasks, deadlines, and AI-suggested next steps.

### Documents
Users can track document status, upload supporting files, and monitor submission readiness.

### Community
Users can browse milestones, resources, and advice posts, then interact through upvotes and save actions.

### AI Essay Coach
Users can interact with an AI-style chat assistant for essay brainstorming, draft improvement, and interview preparation.

### More
Users can review profile details, scores, workspace shortcuts, and reset selected local data.

## Tech Stack

### Frontend
- React
- React Router DOM
- Lucide React

### Styling
- Utility-style CSS classes
- Custom responsive app layout
- Card-based UI system

### State and Persistence
- React Hooks
- Browser localStorage

## Project Structure

```text
src/
├── App.jsx
├── main.jsx
├── index.css
├── components/
│   ├── AppShell.jsx
│   ├── BottomNav.jsx
│   ├── EmptyState.jsx
│   ├── NotificationPanel.jsx
│   ├── PageHeader.jsx
│   ├── ProgressRing.jsx
│   ├── StatCard.jsx
│   └── ui.jsx
├── data/
│   └── mockData.js
├── lib/
│   ├── helpers.js
│   ├── openai.js
│   └── storage.js
└── pages/
    ├── AIAgentPage.jsx
    ├── CommunityPage.jsx
    ├── DocumentsPage.jsx
    ├── HomePage.jsx
    ├── MatchPage.jsx
    ├── MorePage.jsx
    ├── OnboardingPage.jsx
    └── TimelinePage.jsx
```

## Installation

This section explains the complete local setup process.

### Prerequisites

Make sure the following tools are installed on your computer:

- Node.js 18 or above
- npm
- Git
- A code editor such as VS Code

Check whether they are installed:

```bash
node -v
npm -v
git --version
```

If Node.js is not installed, download the LTS version from:

```text
https://nodejs.org/
```

---

### Step 1: Clone the repository

Clone the repository from GitHub:

```bash
git clone https://github.com/Andrew-Ng701/gnosis-admission-assistant.git
```

Move into the project folder:

```bash
cd gnosis-admission-assistant
```

If you are not using Git, you can also:

1. Download the repository ZIP file from GitHub
2. Extract it to your computer
3. Open the extracted folder in your terminal or code editor

---

### Step 2: Install dependencies

Run the following command in the project root folder:

```bash
npm install
```

This will install all required packages from `package.json`.

After the installation finishes, a `node_modules` folder will be created automatically.

---

### Step 3: Create the environment file

If you want to run the app in local demo mode, create a `.env` file in the root directory.

Example:

```env
VITE_USE_REAL_AI=false
VITE_AI_PROXY_URL=/api/essay-coach
```

Explanation:

- `VITE_USE_REAL_AI=false`  
  Uses the fallback/mock AI response logic in the front-end app.

- `VITE_AI_PROXY_URL=/api/essay-coach`  
  Defines the backend proxy path for AI requests if you later connect a real service.

If you are only testing the UI locally, keeping `VITE_USE_REAL_AI=false` is enough.

---

### Step 4: Start the development server

Run:

```bash
npm run dev
```

The terminal should show a local development URL, usually:

```text
http://localhost:5173/
```

Open that URL in your browser.

---

### Step 5: Test the main flow

After the app starts:

1. Complete the onboarding flow
2. Fill in your profile and academic information
3. Open the Match page and browse schools
4. Open the Timeline page and review tasks
5. Open the Documents page and check upload flow
6. Try the AI Essay Coach
7. Explore the Community and More pages

---

### Step 6: Build for production

To create a production build:

```bash
npm run build
```

This generates an optimized output folder, usually named `dist`.

To preview the production build locally:

```bash
npm run preview
```

## Available Scripts

### `npm run dev`
Starts the local development server.

### `npm run build`
Builds the app for production.

### `npm run preview`
Previews the production build locally.

## Environment Variables

The app supports optional AI-related environment variables.

Create a `.env` file in the project root:

```env
VITE_USE_REAL_AI=false
VITE_AI_PROXY_URL=/api/essay-coach
```

### Notes

- Do not commit real API keys to GitHub
- Keep sensitive configuration in `.env`
- Use a backend proxy if you connect a real AI provider
- The current project can still work in fallback mode without a live backend

## Local Data and Reset Guide

The project uses browser localStorage to persist user data. Based on the source structure, app data includes profile, tasks, posts, documents, notifications, messages, and onboarding status. [file:2]

Common localStorage keys include:

- `gnosis_onboarding_complete`
- `gnosis_profile`
- `gnosis_tasks`
- `gnosis_posts`
- `gnosis_documents`
- `gnosis_notifications`
- `gnosis_messages`

These keys are initialized through the storage layer and seeded automatically when the app shell loads. [file:2]

### Why reset local data

If you changed the data model during development, older localStorage values may no longer match the latest code structure. That can cause missing fields, blank UI states, or incorrect behavior. [file:2]

### How to reset local data

In Chrome or Edge:

1. Open the app in the browser
2. Press `F12` to open Developer Tools
3. Go to `Application`
4. Open `Local Storage`
5. Select your app origin
6. Remove keys starting with `gnosis_`
7. Refresh the page

## Recommended Setup Notes

This app uses React Router for page navigation and protects app routes by checking whether onboarding is complete. The route structure includes `/home`, `/match`, `/ai-agent`, `/community`, `/more`, `/timeline`, and `/documents`. [file:2]

App data is seeded when `AppShell` loads, and persistence is handled through helper functions in `lib/storage.js`. [file:2]

The AI module reads `VITE_USE_REAL_AI` and `VITE_AI_PROXY_URL`, and falls back to mock responses if real AI mode is not enabled. [file:2]

## GitHub Setup

If you want to publish this project to GitHub for the first time, run the following commands in the project root:

```bash
git init
git add .
git commit -m "Initial commit: Gnosis admission assistant"
git branch -M main
git remote add origin https://github.com/Andrew-Ng701/gnosis-admission-assistant.git
git push -u origin main
```

For later updates:

```bash
git add .
git commit -m "Update app features"
git push
```

### Recommended repository name

```text
gnosis-admission-assistant
```

### Recommended GitHub description

```text
A React-based university application assistant that helps students manage onboarding, university matching, application timelines, documents, community posts, and AI essay coaching.
```

## Recommended `.gitignore`

Create a `.gitignore` file in the project root with the following content:

```gitignore
node_modules
dist
.env
.env.*
.DS_Store
.vscode
.idea
```

## Deployment Notes

This app can be deployed as a static front-end project to platforms such as:

- Vercel
- Netlify
- GitHub Pages
- Other static hosting services

Typical build settings:

### Build command

```bash
npm run build
```

### Output directory

```text
dist
```

### Important note

If you later connect a real AI backend, you should not call a secret API directly from the browser. Use a secure backend proxy instead. The current front-end already expects a proxy-style AI endpoint path. [file:2]

## Troubleshooting

### `npm install` fails

Possible reasons:

- Node.js version is too old
- internet connection issue
- dependency conflict
- corrupted lock file

Try:

```bash
rm -rf node_modules package-lock.json
npm install
```

### `npm run dev` does not start

Check the following:

- You are inside the correct project folder
- `package.json` exists
- Dependencies were installed successfully
- Node.js version is supported

### The browser shows a blank page

Possible reasons:

- Syntax error in source files
- Import/export mismatch
- Old localStorage data conflicts with the latest code

Try:

1. Check browser console logs
2. Check terminal logs
3. Clear localStorage
4. Restart the development server

### Routes are not working correctly

Check that:

- `react-router-dom` is installed
- Page components are exported correctly
- Routes are defined correctly in `App.jsx` [file:2]

### AI coach is not using a real model

That is expected if `VITE_USE_REAL_AI=false`. In that case, the app uses fallback mock responses defined in the AI module. [file:2]

## Roadmap

Possible future improvements:

- Backend API integration
- Real authentication
- Cloud database
- File storage service
- Real AI essay feedback backend
- Application analytics dashboard
- Saved school lists
- Counselor or admin mode
- Accessibility improvements
- Test coverage

## Contributing

Contributions are welcome for UI improvements, bug fixes, refactoring, documentation, and feature expansion.

Suggested contribution flow:

1. Fork the repository
2. Create a branch

```bash
git checkout -b feature/your-feature-name
```

3. Commit your changes

```bash
git commit -m "Add your feature"
```

4. Push the branch

```bash
git push origin feature/your-feature-name
```

5. Open a Pull Request

## License

This project is intended for educational, demonstration, and portfolio use unless otherwise specified.

If you plan to make it a fully open-source project, consider replacing this section with an MIT License or another open-source license.

## Author

**Andrew Ng**

Software developer focused on AI integration, educational tools, OCR-related workflows, and application-oriented web systems.
