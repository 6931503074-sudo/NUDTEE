# NUDTEE Golden Thread Traceability

Problem → Requirement → Design → Feature (screen) → Test

| Problem | Requirement | Design | Feature (screen) | Test |
|---------|-------------|--------|------------------|------|
| No structured place to announce activities; details and locations get buried in chat threads. | FR-1 | Session form with place search and current-location picker, online option, player limits and registration deadline validation; session stored in Cloud Firestore. | Create Session form with location selection, category and registration deadline controls. Status:Pass | TC-1, TC-2, TC-3. Result:Pass |
| No reliable running headcount; organizers ask and count manually in chat. | FR-2 | Cloud Firestore transaction for join/leave with capacity checking. | Join/Leave button with live attendee count (current/max). Status:Pass | TC-4, TC-5, TC-6, TC-7. Result:Pass |
| Headcounts go stale between chat messages as people change their minds. | FR-3 | Cloud Firestore real-time listeners on session records. | Live-updating session list with status indicators (Open, Almost Full, Full, Joined, Closed). Status:Pass | TC-8, TC-9. Result:Pass |
| Unclear activity locations cause participants to get lost or arrive late. | FR-4 | Embedded Google Maps view centred on the saved coordinates, with an "Open in Google Maps" link. | View Location screen and map preview on the session details. Status:Pass | TC-10. Result:Pass |
| Disorganised logistical coordination across general group chats. | FR-5 | Per-session message collection in Cloud Firestore, opened only for participants. | Room Chat for joined attendees. Status:Pass | TC-11, TC-12, TC-15. Result:Pass |
| Uncontrolled last-minute joins after event preparations are finalised. | FR-6 | Time check (end of deadline day and session start) in the join flow before the join transaction. | Session shown as Closed and late join attempts rejected; ended sessions marked completed. Status:Pass | TC-13. Result:Pass |
| Participants forget scheduled activities for lack of reminders. | FR-7 | Google Calendar event-template link pre-filled with the session details. | "Add to Calendar" button on the session details. Status: | TC-14. Result:Pass |
