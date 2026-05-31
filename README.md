# EchoFlow AI 🎙️📈

EchoFlow AI is an ultra-low-latency, voice-first English language learning platform designed to build speaking confidence and fluency. By replicating a real-time phone call environment, it prioritizes auditory-first interaction and utilizes a Bring Your Own Key (BYOK) financial framework for provider-direct scalability.

---

## 📁 Repository Structure

The workspace is organized as a monorepo containing the following applications:

```bash
echo-flow-ai/
├── mobile/            # React Native Expo frontend client
│   ├── src/           # Component, routing, state, and hook code
│   └── assets/        # Visual and design system assets
├── server/            # Node.js Express backend proxy server
│   └── src/           # Database, router, controller, and logging setups
├── .husky/            # Monorepo-wide pre-commit and commit-msg hooks
└── package.json       # Monorepo root configuration and runner scripts
```

---

## 🛠️ Prerequisites

Ensure you have the following installed on your local environment:
* **Node.js**: `v22.x` (LTS recommended)
* **npm**: `v10.x` or higher
* **MongoDB**: Running locally on `mongodb://localhost:27017` (required for backend proxy logging and rate limiting)
* **Expo Go** or an emulator (Android Studio / Xcode iOS Simulator) for running the client application

---

## 🚀 Getting Started

### 1. Install Dependencies
Run the command below at the monorepo root to install packages in the root, `mobile`, and `server` subdirectories:
```bash
npm run install:all
```

### 2. Run the Applications
You can run the mobile client and backend proxy simultaneously or independently from the workspace root:

* **Start the Mobile Client**:
  ```bash
  npm run start:mobile
  ```
  *(Press `a` for Android, `i` for iOS, or `w` for Web build)*

* **Start the Backend Server**:
  ```bash
  npm run start:server
  ```
  *(Launches the Express app under `nodemon` on http://localhost:3000)*

---

## 🔍 Validation & Linting

We enforce codebase checks and commit validation locally using Husky:
* **Staged linting**: File commits trigger `expo lint` on `mobile` changes and ESLint/Prettier code formatting on `server` changes.
* **Commit Messages**: Commits are validated with Commitlint and must follow the Conventional Commits format (e.g. `feat: Add sqlite storage`).
