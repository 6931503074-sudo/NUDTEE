# NUDTEE

A real-time activity meetup coordination web app. Built by **Team Dek70** for Intro to Software Engineering (15031001), Academic Year 2569.

**SDLC:** Agile (Scrum, feature-based sprints), split by functional requirement FR-1 to FR-7.

## The problem

General activity scheduling often suffers from unclear timing and participant requirements. Critical details such as the location and schedule get buried in LINE or Facebook group chats, leading to confusion and forgotten appointments. Organizers also have no live count of how many spots are still open, so they must ask around and recount RSVPs by hand. This wastes time and often means a session falls apart even though enough interested people exist.

## Who it's for

- **Organizers** who need to fill a session with the right number of people without recounting RSVPs in chat
- **Participants** who want clear dates, times, and locations, a live view of open spots, and a way to add the session to their own Google Calendar

## Core features (MVP)

| FR | Feature | Priority |
|----|---------|----------|
| FR-1 | Create a session (title, location or online meeting link, date/time, min/max players, registration deadline, category) | Must |
| FR-2 | Join / leave a session, with live remaining-spot count | Must |
| FR-3 | Real-time session status, updates within 2 seconds with no refresh | Must |
| FR-4 | Display a session's location on an interactive map | Must |
| FR-5 | In-room chat (session participants only) | Must |
| FR-6 | Auto-close: joining is blocked once registration closes (end of the deadline day, or the session start time, whichever comes first) | Must |
| FR-7 | Add a joined session to Google Calendar (pre-filled event link) | Must |

Lightweight extras (Could, no dedicated FR or acceptance test this term): category filter, user profile page, session cover image, online sessions with meeting link, time-overlap check, organizer tools (remove participant, close room), "use my current location", share-link button, Thai/English language menu.

### Out of scope this term

- Waitlist management
- Push notifications and native reminders (reminders are handled by Google Calendar)
- User ratings and reviews
- Venue booking and payment integration
- Social features and direct messaging (friend lists, following, 1-on-1 chat outside session rooms)
- Editing a session after creation (the organizer closes the room and creates a new one)
- Map overview showing all sessions on one map (a location is viewed per session)
- Google Calendar API integration (no OAuth tokens or Calendar API calls; the export uses a pre-filled event link)

## Success metrics

| ID | Metric | Target |
|----|--------|--------|
| SM-1 | Time for an organizer to create a session | 60 seconds or less |
| SM-2 | Taps for a player to join an open session from the list | 2 taps or fewer |
| SM-3 | Time for another device to show a join/leave change | 2 seconds or less |
| SM-4 | Taps to add a joined session to Google Calendar (excluding Google sign-in) | 2 taps or fewer |
| SM-5 | Rejection rate for join attempts (through the application) after registration has closed | 100% |
| SM-6 | Delivery time for in-room chat messages across devices | 2 seconds or less |

## Tech stack

- **Frontend:** static web page (HTML/CSS/JS)
- **Auth:** Google sign-in via Firebase Authentication
- **Database / realtime:** Cloud Firestore with real-time listeners (Firebase free Spark plan)
- **Map:** embedded Google Maps view (no API key)
- **Place search:** OpenStreetMap-based Nominatim and Photon services (light, rate-limited use)
- **Calendar:** Google Calendar event-template link (no API or OAuth)
- **Hosting:** Vercel or Netlify (free tier)

All services stay within free usage limits.

## Project status

- [x] Team Charter
- [x] SRS
- [x] Sequence diagrams
- [x] Use case diagram
- [ ] Architecture and data model (update)
- [x] UI wireframes / design
- [ ] Clickable prototype covering every Must FR
- [ ] Final report + Golden Thread table
- [ ] Demo slides
- [ ] AI-use statement (new version)

## Getting started

```bash
# clone the repo
git clone https://github.com/6931503074-sudo/NUDTEE1.git
cd NUDTEE1 https://nudtee-e329d.web.app/

# No install needed: just open index.html in your browser
```

## Data model

Stored in Cloud Firestore:

- **users**: Google account ID, display name, plus optional profile fields (username, short bio, small profile-picture thumbnail). The user's full profile is kept in the browser's local storage.
- **sessions**: organizer, title, short and room descriptions, category, online/offline type, location name, address and coordinates (or meeting link), date, start/end time, min/max players, registration deadline, cover image
- **participants** (stored with each session): which user has joined which session, with display name and thumbnail; used to compute remaining spots (`max_players - current_joined`) and reject joins when full. Join and leave run as Firestore transactions.
- **messages** (per session): sender ID, sender name, text, timestamp (in-room chat)

Session status (Open, Almost Full, Full, Joined, Closed) is computed when the list or details are displayed, not stored.

See /Docs for the SRS, diagrams, and design documents.

## Team

| Name | Student ID | Role |
|------|-----------|------|
| Sirawit Kansuwan | 6931503074 | Product/project lead, Documentation |
| Suratsawadee Areerob | 6931503119 | Documentation / AI log |
| Thanyarat Ainpasat | 6931503107 | Documentation / AI log|
| Ninmanee Nualsee | 6931503050 | Design / Front / UI, Backend / data |
| Rawisara Palang | 6931503065 | Design / Front / UI, QA / AI log |
