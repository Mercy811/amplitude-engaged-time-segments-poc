# Delayed Page View · Engaged Time POC

An interactive static POC for an engaged-time architecture using a delayed-event (heartbeat) service:

- Send the original `[Amplitude] Page Viewed` to the delayed-event service.
- Calculate engaged time in the Browser SDK with a five-second rolling activity window.
- Reuse the shared 60-second heartbeat cadence and checkpoint immediately on blur/hidden.
- Replace the pending snapshot using a stable `insert_id`, while preserving the original event timestamp and Page View ID.
- On navigation, lifecycle end, or expiry, attach `engaged_time_seconds` to that same Page Viewed event and forward it to Amplitude.

No separate engaged-time analytics event is created. The main trade-off is that Page Viewed is not queryable in Amplitude until the delayed service finalizes and forwards it.

This is a proposed architecture POC, not a production-ready implementation. It does not fully implement ordering/version races, BFCache, browser suspension, offline persistence, multi-tab behavior, shared Heartbeat isolation, or the Analytics first-class metric surface.

The browser SDK, delayed-event service, and Amplitude ingestion are simulated in-browser for this GitHub Pages demo.
