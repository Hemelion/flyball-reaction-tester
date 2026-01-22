# Unleashed Flyball Team – Flyball Reaction Tester

<p align="center">
  <img src="https://scontent-waw2-2.xx.fbcdn.net/v/t39.30808-6/529307358_1197038148893518_7517647576720036195_n.jpg?_nc_cat=102&ccb=1-7&_nc_sid=6ee11a&_nc_ohc=4Nn3zZ6vxcMQ7kNvwE9UG1n&_nc_oc=AdmFPyQxfQDPtGE9zbUZlW2QRw6ddeEo-8-TqnYUffmH36fAQEu5DaRTzvNboIA0tor1fheKaD1iIzfogDezUbFK&_nc_zt=23&_nc_ht=scontent-waw2-2.xx&_nc_gid=RvD7VEsdGz09--2-mtRVfQ&oh=00_AfoRLC7AWMpg1r_Trxt1U75brvbGJmWgU90bHeIS9SVEZw&oe=697287A9" alt="Unleashed Flyball Team" width="200" style="border-radius:16px;">
</p>

<p align="center">
  <b>Web-based reaction time tester synchronized with real video triggers.</b><br/>
  <i>Version 3.8</i>
</p>

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [How It Works](#how-it-works)
- [Scoring & Philosophy](#scoring--philosophy)
- [Usage Guide](#usage-guide)
- [Fullscreen Test Mode](#fullscreen-test-mode)
- [Controls & Shortcuts](#controls--shortcuts)
- [Rating System](#rating-system)

---

## Overview

This app was built for the **Unleashed Flyball Team** to train and objectively measure reaction times **against real video footage** – for example, the exact frame when a dog leaves the box or when a light turns on.

Unlike typical "click when the screen turns green" games, this tool:

- Lets you **load multiple videos** and set trigger events on each
- **Randomly selects videos** during testing to prevent memorization
- Measures how consistently you react **after** that frame appears
- Strongly penalizes **anticipation** (pressing before the actual event)
- Rewards **repeatability** more than raw speed
- Provides an **immersive fullscreen test mode** optimized for mobile devices

Everything happens **locally in your browser** – no backend, no uploads to a server.

---

## Key Features

### 🎬 Multi-Video Support
- Load multiple video files at once (use file picker or drag & drop)
- Set different event markers on each video
- Videos are randomly selected during test runs to prevent pattern memorization
- Dropdown selector to switch between loaded videos
- Load videos from URL for remote files

### 📱 Fullscreen Test Mode
- **Immersive fullscreen experience** during testing
- **Video controls completely hidden** to prevent distraction (especially important on mobile)
- Large, touch-friendly **"Reaguj (Space)"** button always visible at the bottom
- **Real-time result bubbles** showing your reaction time and rating after each trial
- **Test summary screen** at the end with final score, mean, SD, and quick actions
- Animated feedback with color-coded results
- Optimized for both desktop and mobile devices
- **Auto-fit video on load** - videos are automatically scaled to fit properly
- Automatic exit from fullscreen when test completes

### 📊 Comprehensive Statistics
- **Gaussian distribution curve** of your reaction times
- Mean (μ), standard deviation (SD), min/max values
- **Final score (0-100)** based on consistency and honesty
- Visual representation of repeatability
- Detailed breakdown of valid vs. predicted trials

### 🎯 Anti-Cheating Design
- Random video selection (when multiple videos loaded)
- Random start offset before event (configurable range)
- **Prediction detection** (reactions < 120ms marked as anticipated)
- Heavy scoring penalties for anticipation
- Unpredictable timing makes it impossible to "game" the system

### 🔍 Video Controls
- Zoom slider (0.5x to 2.5x)
- Pinch-to-zoom on mobile devices
- Pan/drag when zoomed in
- Preset zoom levels: **Fit**, **Small**, **Medium**, **Large**
- Double-click/tap to reset zoom

### 💾 Data Export
- Export all results to CSV format
- Includes trial number, timestamp, reaction time, rating, and video name

### 📲 Progressive Web App (PWA)
- **Install on device** - add to home screen on iOS/Android
- **Offline support** - core app works without internet connection
- **Native app feel** - runs in standalone mode without browser UI
- **Auto-updates** - service worker ensures you always have the latest version

---

## How It Works

1. **Load videos**: Select one or more video files, or load from URL
2. **Mark events**: Scrub to the exact frame and press **"Ustaw zdarzenie (E)"** for each video
3. **Start the test**: Click **"Start (S)"** to enter fullscreen test mode
4. **React**: Watch the video and press the React button exactly when the event occurs
5. **See results**: A bubble shows your time and rating after each trial
6. **Review stats**: After all trials, view comprehensive statistics and Gaussian curve

### Reaction Time Calculation

```
reactionMs = (pressVideoTime - eventTime) × 1000
```

- **Negative or < 120 ms** → Marked as "Przewidziałeś" (Predicted) – not a valid reaction
- **120-170 ms** → "Rewelacja" (Excellent)
- **171-240 ms** → "Bardzo dobrze" (Very Good)
- **241-270 ms** → "Dobrze" (Good)
- **> 270 ms** → "Do poprawy" (Needs Improvement)

---

## Scoring & Philosophy

The goal is to **train the brain not to jump early**, but to fire **consistently** on the signal.

### Prediction Detection
- Any trial with reaction < 0 ms or < 120 ms is labeled **"Przewidziałeś"** (Predicted)
- Predicted trials are:
  - Shown in the table with a red badge
  - Excluded from Gaussian statistics
  - **Heavily penalize** your final score

### Repeatability (Most Important)
Standard deviation (SD) of valid times is the key metric:

| SD Range | Rating |
|----------|--------|
| < 15 ms | 🏆 ELITARNA POWTARZALNOŚĆ (Elite) |
| 15-30 ms | ✅ BARDZO DOBRA POWTARZALNOŚĆ (Very Good) |
| 30-50 ms | ⚠️ PRZECIĘTNA POWTARZALNOŚĆ (Average) |
| > 50 ms | ❌ NISKA POWTARZALNOŚĆ (Low) |

### Final Score (0-100)
The score is calculated based on:
- **Speed** (small weight) – faster average is better
- **Consistency** (medium weight) – lower SD is better
- **Honesty** (large weight) – no predictions is best

**Formula concept:**
```
Score = 100 - speedPenalty - consistencyPenalty - predictionPenalty
```

A slightly slower but extremely consistent and honest responder will **outscore** a fast but jumpy one.

---

## Usage Guide

### 1. Load Videos

- Click the **file input** and select one or more video files (`mp4`, `webm`, etc.)
- Or click **"Wczytaj URL"** to load a video from a direct URL
- Use the **dropdown** to switch between loaded videos

### 2. Mark Events

For each video:
1. Use the video controls to scrub to the exact frame of interest
2. Click **"Ustaw zdarzenie (E)"** or press **E**
3. Optionally enter a description (e.g., "Dog hits the box")

The event marker shows in the top-right corner of the video.

### 3. Configure Test Settings

| Setting | Description | Default |
|---------|-------------|---------|
| Powtórzeń | Number of trials to run | 5 |
| Losowo od (s) | Minimum random offset before event | 1.5 |
| do (s) | Maximum random offset before event | 2.5 |

### 4. Run the Test

1. Click **"Start (S)"** or press **S**
2. The app enters **fullscreen test mode**
3. Watch the video – don't anticipate!
4. Press the **"Reaguj (Space)"** button or **Space** key when the event occurs
5. See your result in the bubble overlay
6. Repeat until all trials complete
7. View the **test summary** with your final score and options to retry or exit

### 5. Review Results

After the test:
- **Results table**: Each trial with timestamp, time in ms, and rating
- **Statistics panel**: Final score, mean, SD, min, max
- **Gaussian curve**: Visual distribution of your reaction times
- **Export CSV**: Download all results for further analysis

---

## Fullscreen Test Mode

When the test starts, the app enters an immersive fullscreen mode designed for focus:

### What You See
- **Full-screen video** without any native controls
- **Trial info** at the top showing current progress (e.g., "Próba 3 / 5 — Reaguj!")
- **Large React button** at the bottom, always accessible

### After Each Reaction
A **result bubble** appears in the center showing:
- Your reaction time in milliseconds (large text)
- Your rating with color-coded badge:
  - 🟡 Gold: "Rewelacja" (Excellent)
  - 🟢 Green: "Bardzo dobrze" (Very Good)  
  - 🟠 Orange: "Dobrze" (Good)
  - 🔴 Red: "Przewidziałeś" (Predicted/Too Early)
  - ⚪ Gray: "Do poprawy" (Needs Improvement)

### Test Summary Screen
After all trials complete, a **summary bubble** appears showing:
- **Final Score** (0-100) with color-coded indicator
- **Performance label** (e.g., "MISTRZ REAKCJI!", "Bardzo dobry wynik")
- **Average reaction time** (mean in ms)
- **Consistency** (standard deviation ±ms)
- **Valid trials count** (e.g., "4 / 5")
- **Quick actions**: "Jeszcze raz" (Try Again) or "Zakończ" (Exit)

### Exiting Fullscreen
- **After summary**: Click "Zakończ" to exit
- **Try again**: Click "Jeszcze raz" to restart with same settings
- **Manual abort**: The test runs until completion (no Stop button in fullscreen)

---

## Controls & Shortcuts

### Keyboard Shortcuts

| Key | Action |
|-----|--------|
| **E** | Set event at current video time |
| **S** | Start the reaction test |
| **Space** | React (only during active test) |

### Video Controls

| Control | Action |
|---------|--------|
| Zoom slider | Adjust zoom 0.5x – 2.5x |
| Pinch (mobile) | Zoom in/out |
| Drag (when zoomed) | Pan the video |
| Double-click | Reset zoom and position |
| Fit / Small / Medium / Large | Preset zoom levels |

### Test Controls

| Button | Action |
|--------|--------|
| Start (S) | Begin the test in fullscreen mode |
| Reaguj (Space) | Record reaction (in fullscreen) |
| Jeszcze raz | Restart test (in summary screen) |
| Zakończ | Exit fullscreen (in summary screen) |
| Eksport CSV | Download results as CSV file |

---

## Rating System

| Reaction Time | Rating (Polish) | Rating (English) | Valid |
|---------------|-----------------|------------------|-------|
| < 0 ms | Przewidziałeś | Predicted | ❌ No |
| 0-119 ms | Przewidziałeś | Predicted | ❌ No |
| 120-170 ms | Rewelacja | Excellent | ✅ Yes |
| 171-240 ms | Bardzo dobrze | Very Good | ✅ Yes |
| 241-270 ms | Dobrze | Good | ✅ Yes |
| > 270 ms | Do poprawy | Needs Improvement | ✅ Yes |

---

## Technical Notes

- **Browser compatibility**: Works best in Chrome, Firefox, Safari, and Edge
- **Mobile support**: Fully responsive, optimized for touch with layout fixes for iOS Safari and Chrome
- **PWA support**: Installable as app on mobile and desktop
- **Offline capable**: Core functionality works without internet
- **Local processing**: All data stays in your browser
- **No installation required**: Just open the HTML file, or install as PWA
- **Auto-fit on load**: Videos automatically fit to container when loaded
- **Safari note**: Local files work best; CORS-restricted remote URLs may not allow frame-accurate seeking

### Installing as PWA

**On iOS (Safari):**
1. Open the app in Safari
2. Tap the Share button
3. Select "Add to Home Screen"

**On Android (Chrome):**
1. Open the app in Chrome
2. Tap the menu (⋮)
3. Select "Add to Home Screen" or "Install App"

**On Desktop (Chrome/Edge):**
1. Look for the install icon in the address bar
2. Click "Install"

---

<p align="center">
  Made with ❤️ for the <b>Unleashed Flyball Team</b>
</p>
