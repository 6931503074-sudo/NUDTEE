# NUDTEE System Architecture

## 1. Architecture Overview

NUDTEE uses a combination of layered, client-server, MVC, and monolithic architectural styles. These styles are used together because each addresses a different aspect of the system.

- Client-Server: defines how the web client communicates with the Firebase back end.
- Layered Architecture: organizes the internal responsibilities of the application.
- MVC: organizes the structure of the client-side user interface.
- Monolithic Architecture: defines how the application is deployed.

These architectural styles complement each other rather than conflict with one another.

### Layered Architecture

The application is organized into three main layers:

- Presentation Layer: displays the screens, receives user input, and passes it to the application logic layer.

- Application Logic Layer: handles the main system rules and processing, including form validation, the join/leave flow (registration deadline check, time-overlap check, and capacity check), session status evaluation (Open, Almost Full, Full, Joined, Closed), chat access checks, and building the Google Calendar link.

- Data Layer: Cloud Firestore and Firebase Authentication, which manage users, sessions, participation records, and chat messages, and enforce the database security rules.

The layers follow a clear flow:

Presentation → Application Logic → Data

This separation keeps each layer focused on its own responsibility and reduces unnecessary coupling between screens, system rules, and data management.

### MVC Architecture

The client side of NUDTEE follows the Model-View-Controller (MVC) pattern to separate the user interface from interaction handling and client-side state.

- View: displays the screens that users interact with, including the session list, create-session form, session details with map preview, room chat, and user profile page.

- Controller: handles user actions and screen flow, such as tapping Join or Leave, submitting the create-session form, choosing a place from the search results, opening the chat room, tapping Add to Calendar, and filtering by category.

- Model: maintains the client-side state needed by the interface, such as the signed-in user, the latest session list received from the real-time listeners, the selected category filter, the create-session form state, and the messages of the open chat room.

MVC helps keep the user interface organized by separating what the user sees, how user actions are handled, and what information the client currently holds.

### Client-Server Architecture

NUDTEE follows a client-server structure.

The client is a static web page running in the user's browser. It provides the user-facing interface and uses MVC to organize its screens, interaction handling, and local state.

The server side is Firebase, used as a managed back end: Firebase Authentication handles Google sign-in, and Cloud Firestore stores the data and enforces the database security rules. There is no custom server code to deploy or maintain.

The client and Firebase communicate through the Firebase SDK using request/response calls (reads, writes, and transactions) and real-time listeners that push changes to every connected client. The system also interacts with external services required for functions such as map display (embedded Google Maps), place search (Nominatim and Photon), and calendar export (Google Calendar event link).

This structure separates user interaction from data storage and access control.

### Monolithic Structure

NUDTEE is deployed as a single static web application rather than a collection of services.

The system contains a small set of closely related core functions (FR-1 to FR-7) and is developed by one five-person student team within one semester. There is currently no requirement for individual parts of the application to be deployed or scaled independently, and all hosting must stay on free tiers (Firebase Spark, Vercel or Netlify).

Although the application is deployed as one unit, it can still contain separate layers and modules with clearly defined responsibilities.
