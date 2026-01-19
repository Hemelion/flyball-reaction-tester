# Unleashed Flyball Team – Flyball Reaction Tester

<p align="center">
  <img src="https://scontent-waw2-2.xx.fbcdn.net/v/t39.30808-6/529307358_1197038148893518_7517647576720036195_n.jpg?_nc_cat=102&ccb=1-7&_nc_sid=6ee11a&_nc_ohc=4Nn3zZ6vxcMQ7kNvwE9UG1n&_nc_oc=AdmFPyQxfQDPtGE9zbUZlW2QRw6ddeEo-8-TqnYUffmH36fAQEu5DaRTzvNboIA0tor1fheKaD1iIzfogDezUbFK&_nc_zt=23&_nc_ht=scontent-waw2-2.xx&_nc_gid=RvD7VEsdGz09--2-mtRVfQ&oh=00_AfoRLC7AWMpg1r_Trxt1U75brvbGJmWgU90bHeIS9SVEZw&oe=697287A9" alt="Unleashed Flyball Team" width="96" style="border-radius:16px;">
</p>

<p align="center">
  <b>Web-based reaction time tester synchronized with a real video trigger.</b><br/>
</p>

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [How It Works](#how-it-works)
- [Scoring & Philosophy](#scoring--philosophy)
- [Usage](#usage)
  - [1. Load video](#1-load-video)
  - [2. Mark the event](#2-mark-the-event)
  - [3. Configure the test](#3-configure-the-test)
  - [4. Run the test](#4-run-the-test)
  - [5. Read your stats](#5-read-your-stats)
- [Controls & Shortcuts](#controls--shortcuts)
- [Browser Notes](#browser-notes)
- [Technical Notes](#technical-notes)
- [Changelog](#changelog)
- [Disclaimer](#disclaimer)

---

## Overview

This app was built for the **Unleashed Flyball Team** to train and objectively measure reaction times **against real video footage** – for example, the exact frame when a dog leaves the box or when a light turns on.

Unlike typical “click when the screen turns green” games, this tool:

- lets you **synchronize a single frame in your own video** as the trigger event,
- measures how consistently you react **after** that frame appears,
- strongly penalizes **anticipation** (pressing before the actual event),
- rewards **repeatability** more than raw speed.

Everything happens **locally in your browser** – no backend, no uploads to a server.

---

## How It Works

1. You load a video and scrub to the frame where the event happens.
2. You press **“Set event (E)”**, and the app records that video time as the event (`eventTime`).
3. For each trial:
   - The app picks a random offset between `randomFrom` and `randomTo` seconds,
   - Starts playback that many seconds **before** the event,
   - You watch the video and press **React** exactly when the event occurs.
4. Reaction time is computed as:

   \[
   \text{reactionMs} = (\text{pressVideoTime} - \text{eventTime}) \cdot 1000
   \]

   - If this is **negative** or below 140 ms → you **predicted**, not reacted.
   - Otherwise it’s counted as a valid reaction.

5. After enough trials, the app:
   - discards predicted trials from the main stats,
   - fits a Gaussian curve to your valid times,
   - computes standard deviation (SD),
   - calculates a final score 0–100 weighted towards **low SD & no prediction**.

---

## Scoring & Philosophy

The goal is **train the brain not to jump early**, but to fire **consistently** on the signal.

- **Prediction**
  - Any trial with reaction \< 0 ms or \< 140 ms is labeled `"Predicted"` and `valid = false`.
  - Predicted trials are:
    - shown in the table (red badge),
    - excluded from Gaussian stats,
    - heavily penalize your final score.

- **Repeatability**
  - Standard deviation (SD) of valid times is the key metric.
  - Rough interpretation:
    - \< 15 ms → “Elite repeatability”
    - 15–30 ms → “Very good”
    - 30–50 ms → “Average”
    - \> 50 ms → “Low repeatability”

- **Speed (important but secondary)**
  - Faster average reaction time is better, but its weight in the final score is **reduced**.
  - A slightly slower but extremely consistent and honest responder will outscore a fast but jumpy one.

### Final score (0–100)

Conceptually:

- Start from 100,
- Subtract a **small penalty** for being slow,
- Subtract a **strong penalty** for high SD,
- Subtract a **very strong penalty** for predicted trials.

So:  
**no prediction + tight cluster = high score**, even if absolute ms are not world‑class.

---

## Usage

### 1. Load video

- Click **“Choose file”** and select a local video (`mp4`, `webm`, …), or  
- Click **“Load URL”** and paste a direct link to a video file.

On Safari: local files work best; CORS-restricted remote URLs may not allow frame-accurate seeking.

### 2. Mark the event

1. Use the native video controls to scrub to the exact frame of interest.
2. Click **“Set event (E)”** or press **E**.
3. Optionally enter a short description for the event (e.g. `"Dog hits the box"`).

An overlay in the top-right shows the event time in seconds.

### 3. Configure the test

In the right part of the main card:

- **Repetitions** – how many trials to run (default: `5`).
- **Random from (s)** – minimum random offset before the event (default: `1.5`).
- **Random to (s)** – maximum random offset before the event (default: `2.5`).

For each trial, the app will start the video at:

\[
\text{startTime} = \text{eventTime} - \text{randomOffset}
\]

with `randomOffset` uniformly drawn from `[from, to]`.

### 4. Run the test

- Click **“Start (S)”** or press **S**.
- Watch the video; do not anticipate the moment.
- When the event occurs, either:
  - click **“React (Space)”**, or
  - press the **Space** bar.

The app will pause the video, record your reaction time, and after a short pause automatically move to the next trial until all repetitions are done.

You can stop at any time with **“Stop”**.

### 5. Read your stats

In the **Results** panel:

- The **table** shows each trial:
  - time stamp,
  - reaction in ms,
  - rating / badge.
- The **Statystyki / Stats** section shows:
  - final score 0–100 with a short label,
  - number of valid vs predicted trials,
  - mean, SD, min, max,
  - a short explanatory note.

In the **Gaussian curve** card:

- A normal distribution curve fitted to valid trials,
- Mean \(\mu\) and ±1σ lines,
- Individual trials plotted as dots.

---

## Controls & Shortcuts

**Global / Test**

- **E** – set event at current video time.
- **S** – start the reaction test.
- **Space** – react (only when test is running).
- **Stop** button – aborts the test and pauses video.

**Video / View**

- Mouse/touch **drag** (with zoom \> 1) – pan the video.
- **Pinch** (mobile) – zoom in/out.
- **Zoom slider** – adjust zoom level.
- Preset buttons: **Fit**, **Small**, **Medium**, **Large**.
- **Double-click** on video – reset transform (zoom/pan).
