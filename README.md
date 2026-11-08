# NUDTEE

A real-time activity meetup coordination web app. Built for Intro to Software Engineering (15031001), Academic Year 2569.

## The problem

General activity scheduling often suffers from unclear timing and participant requirements. Critical details such as the location and schedule get buried in LINE or Facebook group chats, leading to confusion and forgotten appointments, and organizers have no live count of how many spots are still open, so they must ask around and recount by hand. This wastes time and often means a session falls apart even though enough interested people exist.

## Who it's for

- **Organizers** who need to fill a session with the right number of people without recounting RSVPs in chat
- **Participants** who want clear dates, times, and locations, a live view of open spots, and a reminder in their own calendar

## Core features (MVP)

| FR | Feature | Priority |
|----|---------|----------|
| FR-1 | Create / edit a session (title, pinned map location, date/time, min/max players, closing time) | Must |
| FR-2 | Join / leave a session, with live remaining-spot count | Must |
| FR-3 | Real-time session status — updates within 2 seconds, no refresh | Must |
| FR-4 | Display a session's location on an interactive map | Must |
| FR-5 | In-room chat (session participants only) | Should |
| FR-6 | Auto-close — joining is blocked once the closing time passes | Must |
| FR-7 | Add a joined session to Google Calendar | Should |

Out of scope for this MVP: waitlist, push notifications and reminders, ratings and reviews, venue booking and payments, friend lists and 1-on-1 messaging, genre tagging and filtering.

## Tech stack

- **Frontend:** HTML/CSS/JS
- **Map:** Leaflet + OpenStreetMap tiles
- **Backend / database / realtime:** [Supabase](https://supabase.com) (free tier)
- **Login and calendar:** Google OAuth, Google Calendar API
- **Hosting:** [confirm: Firebase Hosting / Vercel / Netlify] (free tier)

## Project status

- [x] Team Charter (revised for the general meetup scope)
- [x] SRS: FR-1–FR-7, NFRs, use cases (revised)
- [x] Sequence diagrams (draft)
- [x] Use case diagram (update for UC-1–UC-6)
- [ ] Architecture and data model (update)
- [x] UI wireframes / design
- [ ] Clickable prototype covering every Must FR
- [ ] Final report + Golden Thread table
- [ ] Demo slides
- [ ] AI-use statement (new version)

## Getting started

bash
# clone the repo
git clone https://github.com/6931503074-sudo/NUDTEE.git
cd NUDTEE

# No install needed — just open index.html in your browser

## Data model

- **users** — id, display_name, google_account_id
- **sessions** — id, organizer_id, title, latitude, longitude, scheduled_at, closing_time, min_players, max_players, status (open / full / closed)
- **session_participants** — session_id, user_id, joined_at (the join table FR-2/FR-3 compute the live count from)
- **messages** — id, session_id, sender_id, body, sent_at (in-room chat)

See /Docs for the SRS, diagrams, and design documents.

## Team

| Name | Student ID | Role |
|------|-----------|------|
| Suratsawadee Areerob | 6931503119 | TBD |
| Thanyarat Ainpasat | 6931503107 | TBD |
| Ninmanee Nualsee | 6931503050 | TBD |
| Rawisara Palang | 6931503065 | TBD |
| Sirawit Kansuwan | 6931503074 | TBD |

## AI usage

This project used Claude to help draft the problem statement, SRS, FR/NFR list, and diagrams, and to review them. Every AI-drafted piece was reviewed and adjusted by the team. See the AI-use statement in `/Docs`.
