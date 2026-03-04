# PLANS.md — SatTrack 3D Roadmap

## Status
- [ ] Not Started
- [ ] In Progress
- [x] Complete

## V1 — Core working feature
### Goal
Ship a runnable single-file `index.html` that renders a real 3D Earth and displays live satellites.

### Acceptance Criteria
- Cesium globe loads from CDN.
- Satellite positions update continuously from parsed TLE sources.
- Side panel shows live status and object counts.

## V2 — Complete feature set
### Goal
Add monitoring controls and selection-focused interactions.

### Acceptance Criteria
- Source switching between multiple satellite groups.
- Search and orbit-class filters control list + visibility.
- Click satellite to inspect details (name, lat/lon, altitude).
- Orbit trails can be toggled.

## V3 — Production ready
### Goal
Deliver professional-grade situational monitoring UX.

### Acceptance Criteria
- Live satellite monitoring remains keyless and stable.
- Optional live air traffic overlay works with graceful fallback.
- My-location pinning and clear-place controls are available.
- Optional buildings layer and place-name resolution are integrated.
- Status panel communicates degraded/error states clearly.

## Done Means
User opens `index.html` and gets a professional monitoring surface with live-moving satellites, filter/search controls, clickable details, and optional air/location/building context.
