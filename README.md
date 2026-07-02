# Frontend — Greenstep API Client

This repository contains the frontend client for the Greenstep API (Vite + Vue). The README below describes the folder layout and the purpose of major modules.

## Folder structure

frontend/
├─ index.html
├─ package.json
├─ vercel.json
├─ vite.config.js
├─ src/
│  ├─ App.vue
│  ├─ main.js
  │  ├─ style.css
  │  ├─ api/
  │  │  ├─ activity.js
  │  │  ├─ auth.js
  │  │  ├─ challenge.js
  │  │  ├─ client.js
  │  │  ├─ friend.js
  │  │  ├─ goal.js
  │  │  └─ photo.js
  │  ├─ components/
  │  │  ├─ Navbar.vue
  │  │  └─ Sidebar.vue
  │  ├─ layouts/
  │  │  └─ MainLayout.vue
  │  ├─ router/
  │  │  └─ index.js
  │  ├─ stores/
  │  │  └─ authStore.js
  │  └─ views/
  │     ├─ ActivityList.vue
  │     ├─ ChallengeCreate.vue
  │     ├─ ChallengeList.vue
  │     ├─ Dashboard.vue
  │     ├─ FriendList.vue
  │     ├─ FriendRequests.vue
  │     ├─ Goal.vue
  │     ├─ Leaderboard.vue
  │     ├─ LogActivity.vue
  │     ├─ Login.vue
  │     ├─ PhotoGallery.vue
  │     └─ Register.vue

## What each module does

| Path / Module | Responsibility |
|---|---|
| src/api/client.js | Centralized HTTP client (fetch or axios wrapper), base URL and request helpers used by other API modules. |
| src/api/auth.js | Authentication API calls (login, logout, register, token refresh). |
| src/api/activity.js | Endpoints for logging and fetching user activities. |
| src/api/challenge.js | Endpoints for creating, listing, and joining challenges. |
| src/api/friend.js | Friend-related endpoints: list friends, send/accept requests. |
| src/api/goal.js | CRUD operations for user goals. |
| src/api/photo.js | Photo upload / gallery endpoints and helpers. |
| src/components/Navbar.vue | Top navigation component — links, user menu, and primary actions. |
| src/components/Sidebar.vue | Sidebar navigation used in the main layout. |
| src/layouts/MainLayout.vue | Page shell combining Navbar and Sidebar, and slot for views. |
| src/router/index.js | Vue Router setup: routes mapping to views and navigation guards. |
| src/stores/authStore.js | Authentication state (current user, tokens), and helper actions/getters. |
| src/views/Dashboard.vue | Main dashboard showing user summary, stats, and quick actions. |
| src/views/ActivityList.vue | Displays a list/history of logged activities. |
| src/views/LogActivity.vue | UI for logging a new activity. |
| src/views/ChallengeList.vue | List available challenges and status. |
| src/views/ChallengeCreate.vue | Form to create a new challenge. |
| src/views/FriendList.vue | Shows user's friends and quick interactions. |
| src/views/FriendRequests.vue | Manage incoming and outgoing friend requests. |
| src/views/Goal.vue | View and manage an individual goal. |
| src/views/Leaderboard.vue | Leaderboard showing rankings across users or groups. |
| src/views/PhotoGallery.vue | Photo gallery view and photo management. |
| src/views/Login.vue | Login form and related flows. |
| src/views/Register.vue | Registration form and flows. |

## Quick start

1. Install dependencies:

cd frontend
npm install

2. Run the dev server:

npm run dev

3. Build for production:

npm run build

## Notes
- This README was generated from the current folder layout. If you refactor files or add new modules, update this document accordingly.