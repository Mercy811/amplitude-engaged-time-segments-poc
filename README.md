# Delayed Page View · Engaged Time POC

An interactive static POC for an engaged-time architecture using a delayed-event (heartbeat) service:

- Send the original `[Amplitude] Page Viewed` to the delayed-event service.
- Calculate engaged time in the Browser SDK with a five-second rolling activity window.
- Use heartbeats to update the pending Page Viewed record.
- On navigation, lifecycle end, or expiry, attach `engaged_time_seconds` to that same Page Viewed event and forward it to Amplitude.

No separate engaged-time analytics event is created. The main trade-off is that Page Viewed is not queryable in Amplitude until the delayed service finalizes and forwards it.

The browser SDK, delayed-event service, and Amplitude ingestion are simulated in-browser for this GitHub Pages demo.
