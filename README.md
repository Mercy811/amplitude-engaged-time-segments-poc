# Engaged Time Segments POC

An interactive static POC for a fourth engaged-time architecture:

- Send `[Amplitude] Page Viewed` immediately so it is queryable at `t=0`.
- Calculate engaged time in the Browser SDK with a five-second rolling activity window.
- Append idempotent `[Amplitude] Engaged Time Segment` delta events every 15 seconds and on lifecycle boundaries.
- Aggregate segment deltas by a stable Page View ID in metric middleware.

This avoids holding Page Viewed in a delayed service for up to two hours. The trade-off is additional internal event volume and aggregation complexity.

The backend, ingestion stream, and metric layer are simulated in the browser for this GitHub Pages demo.
