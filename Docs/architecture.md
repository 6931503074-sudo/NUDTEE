# NUDTEE System Architecture

## 1. Architecture Overview

NUDTEE uses a combination of layered, client-server, MVC, and monolithic architectural styles. These styles are used together because each addresses a different aspect of the system.

- **Client-Server:** defines how the client communicates with the server.
- **Layered Architecture:** organizes the internal responsibilities of the server.
- **MVC:** organizes the structure of the client-side user interface.
- **Monolithic Architecture:** defines how the server application is deployed.

These architectural styles complement each other rather than conflict with one another.

---

## 2. Layered Architecture

The server side of NUDTEE (Supabase Backend & Core Services) is organized into three main layers:

- **Presentation Layer (API Routes & Validation):** receives requests from the client and handles request/response processing, input validation (e.g., non-empty fields, date/time checks, player capacity validation), and communication with the business logic layer.
- **Application Logic Layer (System Rules & Processing):** handles the main system rules and processing, including atomic join/leave concurrency logic, automatic session closing deadline checks (cron/triggers), real-time WebSocket channel dispatching, and Google OAuth authorization validation.
- **Data Layer (Data Access & Entities):** manages access to persistent information such as User profiles, Session details (titles, pinned map coordinates, schedules, player limits), Participation records, and In-room Chat messages.

The layers follow a clear flow:  
`Presentation` → `Application Logic` → `Data`

This separation keeps each layer focused on its own responsibility and reduces unnecessary coupling between request handling, system rules, and data management.

---

## 3. MVC Architecture

The client side of NUDTEE follows the Model-View-Controller (MVC) pattern to separate the user interface from interaction handling and client-side state.

- **View:** displays the screens that users interact with, including interactive map views with location pins (Leaflet / OpenStreetMap), session creation/edit forms, live participant lists, real-time in-room chat interfaces, and Google Calendar export confirmation buttons.
- **Controller:** handles user actions and screen flow, such as creating or editing session forms, pinning map coordinates, tapping join/leave actions (within 2 taps or fewer), sending chat messages, navigating between screens, and triggering Google Calendar event export.
- **Model:** maintains the client-side state needed by the interface, such as selected session data, live remaining-spot counts, real-time participant lists, active chat messages, user authentication/OAuth tokens, and connection status indicators (e.g., reconnecting states).

MVC helps keep the user interface organized by separating what the user sees, how user actions are handled, and what information the client currently holds.

---

## 4. Client-Server Architecture

NUDTEE follows a client-server structure.

The client provides the user-facing interface (web/mobile browser UI) and uses MVC to organize its screens, interaction handling, and local state.

The server receives requests from the client, applies the required business rules (such as atomic spot locking and deadline checks), accesses the necessary data, and returns the appropriate response.

The client and server communicate through request/response HTTP/JSON interfaces and real-time WebSocket channels (Supabase Realtime). The system also interacts with external services required for functions such as map tile rendering (Leaflet / OpenStreetMap), identity authentication (Google OAuth), and schedule export (Google Calendar API).

This structure separates user interaction from server-side processing and data responsibilities.

---

## 5. Monolithic Structure

The NUDTEE server application is designed as a monolithic architecture rather than a collection of microservices.

The system contains a focused set of closely related core features (FR-1 to FR-7) and is developed by a 5-person student team (Team Dek70) within a single semester build window. There is currently no requirement for individual parts of the server to be deployed or scaled independently.

Although the server is deployed as a single application, it still contains separate layers and modules with clearly defined responsibilities.
