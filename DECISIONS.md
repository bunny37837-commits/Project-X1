# DECISIONS.md — Technical Decisions Log

## [DEC-001] Single-file web architecture
Date: 2026-03-03
Status: Decided

Decision: Implement SatTrack Pro as one production-grade `index.html` containing HTML/CSS/JS.
Reason: SPEC explicitly requires no build step and single-file delivery.
Rejected: Multi-file bundler architecture (Webpack/Vite) due to explicit constraint mismatch.
Impact: All UI, logic, and integration code lives in one portable artifact.

## [DEC-002] Rendering engine
Date: 2026-03-03
Status: Decided

Decision: Use CesiumJS from CDN for globe, entities, orbit lines, and lighting.
Reason: SPEC mandates real 3D Earth with CesiumJS and day/night rendering.
Rejected: Three.js + custom globe because it increases complexity and diverges from SPEC.
Impact: CDN dependency on Cesium assets and Cesium Ion token configuration.

## [DEC-003] Data providers and update cadence
Date: 2026-03-03
Status: Decided

Decision: Use Open Notify for ISS live position and N2YO for categorized multi-satellite data, refreshing every 10 seconds.
Reason: Matches feature requirements and API key availability in SPEC.
Rejected: Static/mock satellite data except as temporary UI fallback when providers fail.
Impact: Requires resilient async fetching, stale-state handling, and user-visible status indicators.

## [DEC-004] Network policy
Date: 2026-03-03
Status: Decided

Decision: Network ON for runtime API and asset calls.
Allowed Domains: `api.n2yo.com`, `cesium.com`, `opennotify.org` (plus optional runtime CORS proxy fallback when direct calls fail).
Reason: Live satellite tracking and Cesium terrain assets require external requests.
Rejected: Fully offline mode because it cannot satisfy live-data goals.
Impact: App includes timeout/error guards and avoids sensitive credential logging.

## [DEC-005] Security posture
Date: 2026-03-03
Status: Decided

Decision: Keep API tokens in client code as supplied by SPEC, avoid token logging, sanitize rendered text with `textContent`, and avoid dynamic HTML injection.
Reason: Browser-only app requires client-side tokens; safe DOM updates reduce XSS risk.
Rejected: Server-side key proxy (not allowed by single-file/no-backend scope).
Impact: Keys are visible in source by design; UI remains defensive against untrusted API payloads.
