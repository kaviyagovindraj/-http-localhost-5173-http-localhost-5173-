# 🌸 StressPlay — Play Your Stress Away

> **Tagline:** *"Play your stress away."*

StressPlay is a gamified wellness and self-awareness full-stack web application built with React, TypeScript, Vite, Tailwind CSS, Firebase Authentication, and Cloud Firestore. It helps users take short, playful 2–5 minute resets tailored to their current mood and non-medical self-awareness estimates.

---

## 🛡️ Safety & Non-Medical Product Disclaimer

- **Not a Medical Product:** StressPlay is strictly for self-awareness and short mindful resets. It does NOT diagnose anxiety, depression, burnout, PTSD, or any medical condition.
- **Self-Awareness Estimates:** Every score is labeled as a *"wellness check-in estimate"* or *"self-awareness estimate"*, never a diagnosis.
- **Support Notice:** *"StressPlay supports self-awareness and short resets. It is not a replacement for professional care."*
- **Crisis Support:** Emphasizes contacting trusted individuals, local emergency services (911 / 112), or free crisis lines (988 Lifeline).
- **Private & Non-Judgemental:** Zero social competition, public leaderboards, or comparison mechanics.

---

## 🚀 Key Features & App Structure

StressPlay includes 14 routes and pages:
1. **Landing Page (`/`):** Hero, product preview, 3 benefit cards, "How it works" sequence, safety note.
2. **Authentication Page (`/auth`):** Email/password sign-up & log in, Google sign-in, and instant zero-setup Local Demo Mode.
3. **Onboarding Page (`/onboarding`):** 3-step skippable setup (Primary Goal, Session Length, Garden Companion).
4. **Home Dashboard (`/dashboard`):** Personalized time-based greeting, Quick Check CTA, stats grid, mini-game reset cards, garden growth stage, Zen Garden sand-raking widget.
5. **Quick Stress Check (`/quick-check`):** 30–60 second interactive game with floating bubble tapping, mood choice prompt, energy slider, and transparent reset recommendation.
6. **Mood Selection (`/mood`):** Mood selector mapped to personalized mini-games.
7. **Breathe & Bloom (`/game/breathe-and-bloom`):** Guided breathing orb (Inhale, Hold, Exhale, Rest) with procedural Web Audio tones and reduced motion progress bar.
8. **Throw Your Worry Away (`/game/throw-worry`):** Private note crumple and dissolve animation with strict opt-in reflection saving.
9. **Pattern Pause (`/game/pattern-pause`):** Simon-says style calming shape sequence recall with friendly no-failure shaming.
10. **Session Summary (`/session-summary`):** Post-game feeling check-in, before vs after rating, garden growth reward, and distress help card if needed.
11. **Your Journey (`/journey`):** Stress journey analytics page with 7d/30d/all-time SVG trend chart, session history, and non-medical disclaimers.
12. **My Garden (`/garden`):** Virtual garden with 5 stages (Seed → Sprout → Flower → Tree → Glowing Oasis), decorations, unlocked badges, and calm fullscreen mode.
13. **Settings & Profile (`/settings`):** Profile management, companion selection, theme switch, sound/motion/colorblind toggles, JSON data export, and complete account deletion.
14. **Safety & Privacy (`/privacy`):** Safety guidelines, reflection privacy explanation, and crisis support hotlines.

---

## 💻 Tech Stack

- **Frontend:** React 19, TypeScript, Vite 8, Tailwind CSS 4 (`@tailwindcss/vite`).
- **Icons & Motion:** Lucide React, Framer Motion, Canvas Confetti.
- **Audio:** Web Audio API procedural synthesizer (zero external MP3 dependencies).
- **Backend & Auth:** Firebase Authentication (Email/Password & Google) + Cloud Firestore.
- **Local Fallback:** Automatic mock/demo fallback when Firebase keys are omitted.

---

## 🛠️ Local Development Setup

### Prerequisites
- Node.js (v18+ recommended)
- npm

### Installation Commands

```bash
# 1. Clone or navigate to project directory
cd "chill pannu"

# 2. Install dependencies
npm install

# 3. Start local development server
npm run dev
```

Visit `http://localhost:5173` in your browser.

---

## 🔑 Firebase Configuration & Environment Variables

Create a `.env` file in the project root based on `.env.example`:

```env
VITE_FIREBASE_API_KEY=your_api_key_here
VITE_FIREBASE_AUTH_DOMAIN=your_project_id.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_project_id.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=1234567890
VITE_FIREBASE_APP_ID=1:1234567890:web:abcdef123456
```

> **Note:** If `.env` is omitted, StressPlay automatically runs in **Demo Mode**, loading realistic 7-day initial mock data so all features work seamlessly offline!

---

## 🗄️ Firestore Data Model

- `users/{userId}`: Profile name, companion avatar, onboarding status, preferences, streak metrics, garden stage level, growth points.
- `users/{userId}/checkins/{checkinId}`: Check-in timestamp, mood, energy level, bubble tapping metrics, recommended game.
- `users/{userId}/sessions/{sessionId}`: Completed mini-game type, duration, before mood, after feeling rating, garden growth reward.
- `users/{userId}/reflections/{reflectionId}`: Opt-in saved private reflection text (created ONLY if user explicitly consents).
- `users/{userId}/garden/{gardenId}`: Garden decorations, unlocked badges, growth points.

---

## 🔒 Security Rules (`firestore.rules`)

```json
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
      match /{allSubcollections=**} {
        allow read, write: if request.auth != null && request.auth.uid == userId;
      }
    }
  }
}
```

---

## 🚀 Production Build & Deployment

To build the production bundle:

```bash
npm run build
```

To preview the build locally:

```bash
npm run preview
```

### Deploying to Firebase Hosting

```bash
npx firebase-tools login
npx firebase-tools init
npx firebase-tools deploy
```

---

## 📋 Quality Verification Checklist

- [x] TypeScript compilation passes cleanly (`npm run build`)
- [x] Responsive layout tested for desktop (1440px) and mobile (320px+)
- [x] Firebase authentication and demo mode fallback operational
- [x] All 3 mini-games functional with persistent data updates
- [x] Non-medical safety disclaimers visible on dashboard & check-ins
- [x] Accessibility features present (44px touch targets, contrast, reduced motion, colorblind mode)
