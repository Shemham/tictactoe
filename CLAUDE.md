# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Structure

This repo contains a Tic Tac Toe game in two forms:

- `tictactoe.html` — standalone single-file web app (open directly in a browser)
- `tictactoe-app/` — Capacitor project that wraps the web app for Android
  - `tictactoe-app/www/index.html` — the web source Capacitor uses (keep in sync with `tictactoe.html`)
  - `tictactoe-app/android/` — generated Android project (do not manually edit Gradle files)
- `TicTacToe.apk` — latest debug APK build output (committed for easy distribution)

## Environment

- **Java 21**: `C:/Program Files/Microsoft/jdk-21.0.10.7-hotspot`
- **Android SDK**: `C:/android-sdk` (API 34, build-tools 34.0.0)
- **GitHub account**: Shemham — always create a repo and push on new projects

## Build Commands

All Gradle commands must be run from `tictactoe-app/android/` with these env vars set:

```bash
export JAVA_HOME="/c/Program Files/Microsoft/jdk-21.0.10.7-hotspot"
export ANDROID_SDK_ROOT="/c/android-sdk"
export ANDROID_HOME="/c/android-sdk"
```

**Build debug APK:**
```bash
cd tictactoe-app/android && ./gradlew assembleDebug
```
Output: `tictactoe-app/android/app/build/outputs/apk/debug/app-debug.apk`

**Sync web changes into Android project (after editing www/):**
```bash
cd tictactoe-app && npx cap sync android
```

**Copy updated APK to repo root for distribution:**
```bash
cp tictactoe-app/android/app/build/outputs/apk/debug/app-debug.apk TicTacToe.apk
```

## Workflow: Making Changes

1. Edit `tictactoe.html` (the source of truth for game logic/UI)
2. Copy changes to `tictactoe-app/www/index.html` (keep both in sync)
3. Run `npx cap sync android` from `tictactoe-app/`
4. Build APK with `./gradlew assembleDebug`
5. Copy APK to repo root
6. Commit and push to GitHub

## Git & GitHub

- **Commit and push frequently** — after every meaningful unit of work (feature added, bug fixed, file created, build succeeded). Never let significant progress sit uncommitted.
- Commit messages must be clean and descriptive — summarise *what* changed and *why*, not just "update files".
- Push to `https://github.com/Shemham/tictactoe` after every commit so the remote is always up to date.
- This applies to all projects — always init a git repo and create a GitHub repo for new projects, then keep committing and pushing throughout the work.
