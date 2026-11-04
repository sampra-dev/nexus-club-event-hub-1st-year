# Nexus — Club & Event Hub

A responsive community hub for discovering clubs and events, signing in with a mock Google profile, and keeping track of registrations and bookmarks.

## Quick start

**Requirements:** Node.js 18+ and npm.

```bash
npm install
npm run dev
```

Open the local URL printed by Vite (usually `http://localhost:5173`).

```bash
npm test       # run registration and bookmark unit tests
npm run build  # production build in dist/
npm run preview
```

## Features

- Responsive landing page with mobile navigation, event category filters, event cards, and club directory.
- Six sample events and six sample clubs in `src/data.js`.
- Mock Google sign-in with a demo profile; session persists in `localStorage`.
- Protected `/dashboard` route with profile, registrations, and bookmarks.
- Registration confirmation, unique ticket ID, and an SVG QR ticket generated with `qrcode.react`.
- Duplicate registration prevention and persistent bookmark toggles.
- Keyboard-operable buttons, semantic landmarks, accessible dialog labels, and reduced-motion support.

## Mock Google auth → real Google OAuth

The UI calls the provider contract in `src/lib/auth.js` (`signIn()` and `signOut()`). Replace `mockGoogleAuth` with a Google Identity Services integration or your preferred OAuth client, then return a normalized profile with `id`, `name`, `email`, and `avatar`. For production, validate the identity token on a backend and use secure, server-managed sessions rather than trusting client-side localStorage. The current implementation is intentionally a frontend-only demo and does not contact Google.

## Project structure

```text
src/
  App.jsx                 # Routes, page components, dialogs, app state
  data.js                 # Sample clubs and events
  styles.css              # Responsive visual system
  lib/
    auth.js               # Replaceable mock auth provider
    storage.js            # localStorage helpers and domain logic
    storage.test.js       # Unit tests
  test/
    setup.js
  main.jsx
```

## Demo notes

- Sign in with any click of **Sign in** / **Sign in with Google**; the app uses the sample Alex Morgan profile.
- Registering creates a local ticket and QR code. This is a demo ticket, not a venue-validated pass.
- Club Join buttons are interactive demo toggles and are not persisted; event registrations and bookmarks are persisted.
- Data is local to the browser. Clearing site storage resets the demo account and saved activity.
