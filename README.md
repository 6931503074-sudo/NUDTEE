# NUDTEE

A real-time board game meetup coordination app. Built for Intro to Software Engineering (15031001), Academic Year 2569.

## The problem

Board game players who want to find more people to play with especially people who enjoy the same genre currently rely on manual back-and-forth in LINE or Facebook groups. Existing groups don't show what genre each member enjoys, so organizers invite the wrong people, and there's no live number showing how many players a session still needs, so organizers must ask around one by one. This wastes time and often means a session never comes together even though enough interested players existed.

## Who it's for

- **Players** who already belong to a group but can't easily find others who like the same genre
- **Session organizers** who need the right number and the right kind of players without asking one by one in chat
- **Newcomers** with no existing friend group, who have no way to see what sessions are open

## Core features (MVP)

| FR | Feature |
|----|---------|
| FR-1 | Create a session (genre, location, date/time, player count) |
| FR-2 | Set favorite game genres on your profile |
| FR-3 | Join / leave a session, with live remaining-spot count |
| FR-4 | Filter sessions by genre |
| FR-5 | Real-time session list — updates within 2 seconds, no refresh |

Out of scope for this MVP: map/GPS view, waitlist, notifications, ratings/reviews, café booking integration, in-app chat.

## Tech stack

- **Frontend:** [HTML/CSS/JS]
- **Backend / database / auth / realtime:** [Supabase](https://supabase.com) (free tier)
- **Hosting:** Vercel / Netlify (free tier)
- **Login:** Google OAuth

## Project status

- [x] Problem statement, users, MVP scope (M1)
- [x] SRS: FR-1–FR-5, NFRs, use cases (M2)
- [x] Use case diagram
- [x] data model
- [x] Sequence diagram (join + realtime broadcast flow)
- [x] UI wireframes
- [ ] Clickable prototype covering every Must FR (M3)
- [ ] Final report + Golden Thread table (M3)
- [ ] Demo slides
- [x] AI-use statement

## Getting started

```bash
# clone the repo
git clone <repo-url>
cd NUDTEE

# No install needed — just open index.html in your browser 

``` 

## Data model

- **users** — id, display_name, favorite_genres
- **sessions** — id, organizer_id, genre, location, scheduled_at, min_players, max_players, status
- **session_participants** — session_id, user_id, joined_at (the join table FR-3/FR-5 compute the live count from)

See `/docs` for the full SRS, ERD, sequence diagram, and wireframes.

## Team

| Name | Student ID | Role |
|------|-----------|------|
| Suratsawadee Areerob | 6931503119 | FR-3 Join / leave session |
| Thanyarat Ainpasat | 6931503107 | FR-4 Filter by genre |
| Ninmanee Nualsee | 6931503050 | FR-5 Realtime sync + integration lead |
| Rawisara Palang | 6931503065 | FR-2 Genre profile tags |
| Sirawit Kansuwan | 6931503074 | FR-1 Create session |

## AI usage

This project used Claude to help draft the problem statement, SRS, FR/NFR list, ERD, sequence diagram, and wireframes. Every AI-drafted piece was reviewed and adjusted by the team.