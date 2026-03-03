# DECISIONS.md — Technical Decisions Log

## [DEC-001] Single-file web architecture
Date: 2026-03-03
Status: Decided

Decision: Implement SatTrack as one production `index.html` containing HTML/CSS/JS.
Reason: SPEC requires no build step and single-file delivery.
Rejected: Multi-file bundler architecture (Webpack/Vite) due to explicit constraint mismatch.
Impact: All UI, logic, and integration code lives in one portable artifact.

## [DEC-002] Rendering engine
Date: 2026-03-03
Status: Decided

Decision: Use CesiumJS from CDN for globe rendering and entity updates.
Reason: SPEC mandates real 3D Earth with CesiumJS.
Rejected: Three.js + custom globe because it diverges from SPEC.
Impact: Runtime depends on Cesium CDN assets.

## [DEC-003] Live data source migration (Phase-0)
Date: 2026-03-03
Status: Decided

Decision: Replace key-based N2YO/Open Notify aggregation with CelesTrak bulk TLE ingestion plus local propagation using `satellite.js` in a Web Worker.
Reason: Inline feedback required removal of exposed keys and a deterministic, keyless live propagation path.
Rejected: Continuing with browser-exposed API key calls.
Impact: No API keys stored in source; positions are propagated client-side at ~1Hz message cadence.

## [DEC-004] Network policy
Date: 2026-03-03
Status: Decided

Decision: Network ON for runtime feed/assets with explicit domains.
Allowed Domains: `celestrak.org`, `cesium.com`, `cdnjs.cloudflare.com`.
Reason: TLE feed + Cesium + satellite.js are required for live experience.
Rejected: Offline mode because it cannot satisfy live-data requirements.
Impact: App surfaces runtime fetch failures in UI status panel.

## [DEC-005] Security posture
Date: 2026-03-03
Status: Decided

Decision: Do not embed API keys or tokens; sanitize user-visible updates using `textContent`; avoid dynamic HTML injection.
Reason: Browser-only apps are source-visible; removing credentials reduces exposure.
Rejected: Client-side credential storage.
Impact: Security risk reduced; all external content treated as untrusted input.
