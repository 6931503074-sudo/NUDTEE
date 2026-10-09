# NUDTEE — Architecture

## Three-tier architecture

### Presentation layer
- *Session list screen* — shows all open sessions with genre, location, time, and a live remaining-spot count; supports genre filtering (FR-4)
- *Create session screen* — form to create a new session (FR-1)
- *Profile screen* — lets a player pick the genres they enjoy (FR-2)

### Application logic layer
- *Create session* — validates and stores a new session (FR-1)
- *Set favorite genres* — validates and stores a player's genre tags (FR-2)
- *Join session* — checks remaining capacity, rejects if full, adds the participant (FR-3)
- *Leave session* — removes the participant, recalculates remaining spots (FR-3)
- *Filter sessions* — returns sessions matching the selected genre(s) (FR-4)
- *Broadcast session update* — notifies every connected viewer when a session's participant count changes (FR-5)

### Data layer
- *Player* — identifier, display name, list of favorite genres
- *Session* — identifier, organizer reference, genre, location, scheduled time, minimum players, maximum players, status
- *Participation* — session reference, player reference, joined-at time (the link between Player and Session that the join/leave operation reads and writes)

## Data model — entities, fields, relationships, operations

| Entity | Fields | Relationships | Operations that touch it |
|---|---|---|---|
| *Player* | id, display name, favorite genres (list) | organizes many Sessions; has many Participations | Set favorite genres (FR-2) |
| *Session* | id, organizer (Player), genre, location, scheduled time, min players, max players, status | belongs to one organizing Player; has many Participations | Create session (FR-1), Filter sessions (FR-4), Broadcast update (FR-5) |
| *Participation* | session (Session), player (Player), joined-at | belongs to one Session and one Player | Join session (FR-3), Leave session (FR-3) |
