---
title: OBS Settings Guide
lastModified: 2025-06-27T12:13:00.000Z
author: Ben
---

:::warning

This page needs some work! I'd like some more references to the video and screenshots - either from the video or your own OBS installation.

:::

# Video

:::embed

https://www.youtube.com/watch?v=ChPYNm_SqiY

:::

This page was written based on this video script! The video took quite the bit of effort to make, and provides a lot of visual aids that the following text may lack.

# OBS Studio Beginner’s Setup Guide (Gaming & Facecam)

By the end of this tutorial, you’ll have a fully functional OBS setup for screen recording and facecam, with independent audio tracks and optimal encoding settings-so your recordings are easy to edit and look great.

> **Who is this for?**  
This guide is beginner-friendly and especially suited for gamers. The only expectation is that you’ve already downloaded and installed OBS from [obsproject.com](https://obsproject.com/).

---

## Pre-requisites

**Windows Users:**  
Before opening OBS, right-click the shortcut, go to **Properties → Compatibility**, and enable **“Run this program as an administrator.”**  
*This isn’t always necessary, but it can prevent issues with capturing certain games.*

Open OBS. If you see the setup wizard, you can close it-we’ll configure everything manually.

---

## Initial Audio & Video Settings

By default, OBS adds your microphone and system audio as “global sources” (included in all scenes). I personally dislike this.

For more control:

1. Go to **Settings → Audio**.
2. Set all global audio devices to **Disabled** (especially system audio - we’ll add it a better way later).

**Video Settings:**

- Go to **Settings → Video**.
- Set **Base (Canvas) Resolution** to your monitor’s native resolution (e.g., 2560x1440 for 1440p).
- Set **Output (Scaled) Resolution** to match (unless you want to downscale).
- Set **FPS** to 60.
- Click **Apply** and **OK**.

---

## Scene Setup

Scenes are collections of sources (game, webcam, mic, etc.) for different recording needs.

### 1. Gaming/Main Scene

**Add Game Capture:**

- In the **Sources** box, click the **+** and select **Game Capture**.
- For most games, use **“Capture specific window”**. Some games may work better with **Window Capture**.
- In Game Capture settings, enable **“Capture audio (BETA)”** to capture audio from your game without any interference from other apps.

**Add Facecam:**

- Click **+ → Video Capture Device**.
- Select your webcam and set its resolution.
- Resize and move the webcam in the preview.  
  - **Crop:** Hold **ALT** and drag the edges.
  - **Reset:** Press **Ctrl+R**.
  - **Fit to screen:** Press **Ctrl+F**.
  - **Precise pixel-perfect crop:** Use **Filters → Crop** for exact values.

**Layering:**  
Sources at the top of the list appear in front of those below - like layers in an editing program.

**Add Microphone:**

- Click **+ → Audio Input Capture** and select your microphone.
- Speak normally and check your levels - aim for the yellow range. With the idea of recording and editing in mind, it's much better to edit your audio in post-production, as you will be able to tweak settings and make mistakes harmlessly.

**Separate Audio Tracks:**

- Right-click the volume mixer, select **Advanced Audio Properties**.
- Assign each source to its own track (e.g., gameplay on Track 1, mic on Track 2).
- Deselect all other tracks for each source.

**Add More Audio (e.g., Discord):**

- Add **Audio Application Capture** and repeat the above steps.

---

### 2. Facecam Scene

For talking directly to your audience or thumbnails:

- Add your camera and mic as before (OBS lets you reuse sources).
- Use **Ctrl+F** to fit the camera to the canvas.

**Advanced: Embedding scenes to apply filters independently:**

1. Create a Dedicated Scene for Your Source
  - In OBS, click the + button in the Scenes list and create a new scene (e.g., “Camera Scene”).
  - Add your camera (or other source) to this new scene.
  - Apply any filters you want (e.g., crop, color correction, LUTs) to the source in this scene.
2. Embed the Scene in Other Scenes
  - In your main scenes (e.g., “Gameplay”, “Facecam”), click the + in the Sources list.
  - Choose “Scene” as the source type.
  - Select your dedicated “Camera Scene” from the list.Now, your camera appears in this scene as a nested source, with all filters applied from the dedicated scene.
3. Create Multiple Dedicated Scenes for Different Filter Sets (Optional)
  - If you want different filter setups (e.g., one cropped, one with a LUT), create multiple dedicated scenes (e.g., “Camera Cropped”, “Camera Color Corrected”).
  - Embed the appropriate scene in each main scene as needed.

---

## Output & Recording Settings

Go to **Settings → Output** and set **Output Mode** to **Advanced**.

**Recording Tab:**

- **Recording Format:**  
  - **MKV** (recommended-safe from crashes, easy to recover).
  - **Hybrid MP4** (if you want direct compatibility with Premiere Pro).
- **Encoder:**  
  - **NVIDIA GPU:** NVENC (best for games, low impact).
  - **AMD GPU:** AMF.
  - **Intel:** QuickSync.
  - **No GPU:** x264 (CPU; not ideal for gaming).
- **Audio Tracks:**  
  - Select the tracks you assigned earlier (e.g., 1 for gameplay, 2 for mic, 3 for Discord, etc.).

I personally recommend that you use MKV, and then remux the footage later for Premiere.

---

### Encoder Settings

- **Bitrate Control:**  
  - **Default (CBR):** Not recommended for recording - wastes space, potentially poor quality in fast scenes.
  - **Use CQP (NVIDIA/AMD) or CRF (CPU):**  
    - Dynamically adjusts bitrate for consistent quality.
    - **CQP Value:** 18–22 (lower = better quality; higher = smaller files).
    - Don’t go too low - YouTube will compress your video anyway.
- **Preset:**  
  - If you get “encoder overload” errors, try a faster preset.
  - For more quality, try a slower preset (if your PC can handle it).

> For more details, see [NVIDIA’s NVENC documentation](https://docs.nvidia.com/video-technologies/video-codec-sdk/12.1/nvenc-application-note/index.html#nvenc-performance).

**Audio Tab:**

- Name your tracks for clarity (e.g., “Game”, “Mic”).
- Set bitrate to **320 kbps** for best quality.

---

## Monitoring & Testing

- Enable the **Stats Dock** (View → Docks → Stats) to monitor dropped frames, CPU/GPU usage, and disk space.
- Always start with plenty of free storage and aim for zero dropped frames.

---

## Editing & Remuxing

If you recorded in **MKV** and your editor (like Premiere Pro) won’t open the file:

- Go to **File → Remux Recordings** in OBS.
- Select your MKV files and convert them to MP4.  
  *(This is fast and lossless - no quality loss.)*

If you dislike remuxing, try **Hybrid MP4** as your recording format.

:::tip

Davinci Resolve can handle mkv files without issue, no remuxing required!

:::

