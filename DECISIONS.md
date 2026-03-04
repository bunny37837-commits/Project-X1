# DECISIONS.md — Technical Decisions Log

## [DEC-001] Single-file web architecture
Date: 2026-03-03
Status: Decided

Decision: Keep the full monitoring platform in one production `index.html` file.
Reason: SPEC requires a no-build, browser-openable artifact.
Rejected: Bundled multi-file architecture.
Impact: UI, worker logic, and integration all remain in one deployable file.

## [DEC-002] Rendering engine and visual layer
Date: 2026-03-03
Status: Decided

Decision: Use CesiumJS globe with lighting enabled, optional OSM buildings, and entity overlays for satellites/aircraft/places.
Reason: Required 3D Earth and professional monitoring visuals.
Rejected: Replacing Cesium with custom 3D stack.
Impact: High-fidelity rendering with optional degradation if buildings are unavailable.

## [DEC-003] Live sources strategy
Date: 2026-03-03
Status: Decided

Decision: Primary satellite source is CelesTrak TLE with local worker propagation; optional air traffic overlay uses OpenSky feed; reverse geocoding uses Nominatim for selected objects.
Reason: Delivers multi-source live monitoring without embedded secrets.
Rejected: Returning to client-exposed key-based APIs.
Impact: Keyless runtime, broader situational context (orbital + atmospheric traffic + location context).

## [DEC-004] Network policy
Date: 2026-03-03
Status: Decided

Decision: Network ON for runtime feeds and assets.
Allowed Domains: `celestrak.org`, `cesium.com`, `cdnjs.cloudflare.com`, `opensky-network.org`, `api.allorigins.win`, `nominatim.openstreetmap.org`.
Reason: Required for live telemetry, CDN assets, optional CORS fallback, and place resolution.
Rejected: Offline-only mode.
Impact: Some optional panels degrade gracefully when external feeds are blocked.

## [DEC-005] Security posture
Date: 2026-03-03
Status: Decided

Decision: No API keys/tokens embedded; all remote payloads treated as untrusted and rendered via `textContent` or controlled labels.
Reason: Browser source is visible by design and must avoid credential exposure.
Rejected: Storing credentials in frontend code.
Impact: Safer client distribution and reduced leak risk.

## [DEC-006] Monitoring UX architecture
Date: 2026-03-03
Status: Decided

Decision: Provide operator-focused controls: source switching, orbit filters, search, selection details, trail toggles, air-overlay toggles, my-location pinning, and clear-place actions.
Reason: User requested professional-grade monitoring with richer controls and location context.
Rejected: Minimal phase-0 panel with only loaded/visible counters.
Impact: Improved operational usability and discoverability of tracked assets.
