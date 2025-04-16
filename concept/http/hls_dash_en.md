### ✅ What is HLS and DASH?

Both **HLS (HTTP Live Streaming)** and **DASH (Dynamic Adaptive Streaming over HTTP)** are **adaptive video streaming protocols**. They allow users to **stream videos smoothly**, even on unstable networks.

#### 📺 What do they do?
They **split a video into small segments** (usually 2–10 seconds), and **generate multiple versions** of the video at different resolutions/bitrates (e.g., 240p, 720p, 1080p).

As the user watches the video, the player:
- Downloads and plays these small segments.
- Dynamically switches quality depending on **network speed or device power**.
- ✅ **Only one segment at one resolution is requested at a time**, and the next segment may be a different resolution depending on the user's current network speed. So it's **adaptive on the client side**.

---

#### 🔧 How it works (simplified):

1. Video is transcoded into **multiple resolutions**.
2. Each resolution is split into **segments**:
   - Example: `720p/segment0.ts`, `720p/segment1.ts`, ...
   - Same for 1080p, 480p, etc.
3. A **playlist file** is generated:
   - **HLS** uses `.m3u8` files
   - **DASH** uses `.mpd` (Media Presentation Description)

These playlist files tell the video player:
> “Here are the available qualities. Here’s where to find each 10-second clip.”

---

#### 🎯 Main difference:

| Feature | HLS | DASH |
|--------|-----|------|
| Developed by | Apple | MPEG group |
| Container Format | `.ts` (MPEG-2 Transport Stream) | `.mp4` (ISO BMFF or fragmented MP4) |
| Playlist | `.m3u8` | `.mpd` |
| Browser support | Best on Safari, iOS | Better on Android, Chrome |
| DRM support | Good | Very good |
| Latency | Higher | Lower (with tuning) |

➡️ **HLS is more widely used**, but **DASH is more modern and flexible**.

---

#### 💻 Who chooses the streaming protocol (HLS or DASH)?

✅ **You (the developer) choose the protocol** based on platform, player, and content delivery strategy. The browser or mobile OS **does not choose automatically**.

- On the web, you use libraries like `hls.js` (for HLS) or `dash.js` (for DASH).
- On mobile:
  - iOS/Safari natively supports **only HLS**.
  - Android supports both via players like **ExoPlayer**.
- So you decide which to use when building your app or video platform.


---

### Summary

- **HLS and DASH** = adaptive streaming protocols. Split videos into segments, support multiple qualities, and use playlists (`.m3u8`, `.mpd`) to deliver them efficiently.
- ✅ The client/player requests **one segment at a time** from one resolution, and dynamically switches quality based on conditions.
- ✅ The **protocol is chosen at the application level** — not automatically by browser or OS.