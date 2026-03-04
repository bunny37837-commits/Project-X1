# STATUS.md — Project Progress Tracker

Current Milestone: V3
Completed: Upgraded `index.html` from minimal phase-0 to a professional monitoring UI with multi-source satellite feeds (CelesTrak groups), live air traffic overlay, source/orbit/search filters, click-to-select details, orbit trails, optional 3D buildings, my-location pinning, place resolution, and clear-place marker controls.
Verification: Local static serving passed (HTTP 200), browser automation screenshot captured, and repository clean after commit.
Next Step: Add compare dashboards (selected satellite vs selected flight), alert thresholds, and optional persistence for operator presets.

## Active Assumptions
ASSUMPTION: OpenSky and Nominatim availability can vary by region/CORS policy.
Reason: Both services are public endpoints and may rate-limit or block requests.
Impact: Air overlay/place resolution may degrade while core satellite tracking remains active.
Reversible: yes

ASSUMPTION: OSM buildings may be unavailable in some Cesium runtime contexts.
Reason: Buildings rely on runtime support and remote tiles access.
Impact: Buildings toggle can fail safely without affecting core tracking.
Reversible: yes

## Active Blockers
None.
