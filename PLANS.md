# PLANS.md — SatTrack 3D Roadmap

## Status
- [ ] Not Started
- [ ] In Progress
- [x] Complete

## V1 — Core working feature
### Goal
Ship a runnable single-file `index.html` that renders a real 3D Earth with Cesium and displays live ISS tracking.

### Acceptance Criteria
- 3D Cesium globe loads with the provided Cesium Ion token.
- ISS marker appears and updates on a 10-second loop.
- Side panel shows ISS telemetry (lat/lon/alt/speed).

### Tasks
- Wire CesiumJS via CDN in `index.html`.
- Add Open Notify ISS fetch and entity updates.
- Add baseline UI panel and status/error handling.

## V2 — Complete feature set
### Goal
Implement multi-satellite tracking and all user-facing interactions from SPEC.

### Acceptance Criteria
- Multiple categories (ISS, Starlink, GPS, Weather) can be filtered.
- Satellite click reveals details (name, altitude, speed, lat/lon).
- Search by name filters visible satellite list.
- Orbit path visualization is visible for tracked satellites.

### Tasks
- Integrate N2YO endpoints for live positions.
- Build category + search controls.
- Add entity click handling and details drawer.
- Render per-satellite orbit polylines.

## V3 — Production ready
### Goal
Polish for a complete production experience with robust fallbacks and full spec compliance.

### Acceptance Criteria
- Live update loop runs every 10 seconds with resilient API error handling.
- Day/night globe lighting enabled.
- User location marker shown when permission granted.
- ISS next pass prediction displayed.
- Satellite count and data refresh timestamps shown.

### Tasks
- Add hardened fetch utility with timeout and fallback behavior.
- Add loading, empty, and degraded-data states in UI.
- Final documentation updates (`DECISIONS.md`, `STATUS.md`).
- Final verification sweep for runnable single-file output.

## Risks & mitigations
| Risk | Impact | Mitigation |
|---|---|---|
| N2YO browser CORS restrictions | High | Use direct fetch first, then CORS proxy fallback path with clear UI warning. |
| Open Notify intermittently unavailable | Medium | Keep latest-known ISS point and show stale-data indicator. |
| Geolocation denied by user | Low | Gracefully continue without user marker. |

## Done Means
User opens `index.html` in a browser, sees a 3D Earth with live-moving satellites, can filter/search, click satellites for details, and view ISS next-pass prediction.
