# Trace

**Trace detects interruptions and physically guides users back to what they were doing.**

Trace is built for people with early cognitive impairment who lose independence when interruptions leave them stuck.

A simple phone call, a doorbell, or a question can break continuity.  
Trace restores it.

---

## The Problem

For people with early cognitive impairment, interruptions do not just pause tasks.

They end them.

After an interruption, users often:
- Walk into a room and forget why
- Stop mid-task with no sense of how to continue
- Lose confidence to resume on their own

This is not memory loss.  
This is loss of continuity.

And loss of continuity leads directly to loss of independence.

---

## The Trace Solution

Trace does not remind users what to do.

Trace brings them back to **where** they lost their flow.

When a user feels stuck, they tap:

> **“I’m stuck.”**

Trace then:
1. Analyzes recent motion patterns from the phone
2. Detects the most likely interruption moment
3. Physically guides the user back to that location using a directional arrow and haptic feedback

No maps.  
No reminders.  
No task lists.

Only physical guidance back to the moment that matters.

---

## How Trace Works

Trace uses well-established motion processing methods, not experimental surveillance.

### Motion Understanding
- Kalman filtering for trajectory smoothing
- Madgwick orientation fusion for device attitude
- Step and turn reconstruction from inertial data
- Behavioral change detection from motion variance

### Interruption Detection
Trace identifies sudden behavior shifts such as:
- Abrupt stops
- Direction reversals
- Search-like pacing
- Long hesitation

These patterns correlate strongly with interruption moments.

### Guidance

Once the interruption point is identified, Trace:
- Displays a directional arrow
- Uses a breathing guidance ring
- Adds haptic proximity feedback

The user does not think.

They simply follow.

---

## The Experience

The interface is intentionally minimal:

- One primary action: **“I’m stuck”**
- One output: **Guidance**

No menus.  
No clutter.  
No cognitive load.

Trace is designed to disappear while working.

---

## Trust & Privacy

Trace is built on strict privacy principles.

- No camera
- No microphone recording
- No raw sensor upload
- No location tracking maps
- No identity data

Motion data is processed locally.

Trace understands behavior, not people.

---

## Azure Usage

Trace uses Azure only where it adds reliability, not dependency.

- **Azure Voice Service**  
  Delivers calm, natural, human guidance voice

- **Azure Application Insights**  
  Ensures system stability, crash detection, and performance reliability

Trace does not rely on cloud processing to function.

Azure strengthens the experience.  
It does not replace it.

---

## Who Trace Is For

Trace is built for people who lose independence after interruptions, including:

- Early cognitive impairment
- Mild cognitive decline
- Post-stroke attention loss
- Executive function challenges

Trace is not a productivity tool.

It is an independence tool.

---

## Why Trace Is Different

Other apps track:
- Tasks
- Calendars
- Reminders
- Notes

Trace tracks where confusion begins.

And brings people back from it.

---

## Design Philosophy

- Human before technical
- Simplicity before features
- Guidance before instruction
- Trust before intelligence
- Continuity before productivity

---

## Current Status

Trace MVP includes:

- Motion processing pipeline
- Interruption detection logic
- Physical guidance interface
- Arrow + haptic navigation
- Minimal UI flow
- Azure Voice integration
- Azure App Insights monitoring

The system demonstrates real interruption recovery in everyday environments.

---

## Our Belief

Independence is not about memory.

It is about continuity.

Trace exists to protect continuity.

---

## Team

Trace is developed as part of the Microsoft Imagine Cup.

---

## Contact

For questions, feedback, or collaboration, please open an issue in this repository.

Trace is built to help people continue their day instead of restarting it.