
<p align="center">
  <img src="./assets/banner.svg" alt="SyachOS" width="100%">
</p>


<p align="center">
  <a href="https://www.youtube.com/watch?v=G0Obn38-Oo8">
    <img src="https://img.youtube.com/vi/G0Obn38-Oo8/maxresdefault.jpg" alt="Watch the SyachOS demo" width="640">
  </a>
</p>
-->

<div align="center">

# 🎮 SyachOS

**A custom Android 13 / LineageOS 20 firmware for the AISLPC RG52 Mini (Rockchip RK3562) handheld.**

A from-scratch port (no prior Android port existed for this device), tuned for gamepad-only handheld use with no touchscreen.

</div>

---

> [!CAUTION]
> **Disclaimer — read first.** This is an unofficial, hobbyist firmware provided **AS-IS, with NO WARRANTY of any kind.** Flashing can **brick your device**, void your warranty, or wipe your data. **Almost all of this firmware was agentic-AI-coded** (built iteratively with AI assistance), one variable at a time. Security is intentionally relaxed (SELinux permissive + KernelSU root + signature spoofing) — **do not use this device for banking, payments, or storing sensitive data.**
>
> **Hardware revisions:** this device shipped in quite a lot of revisions — some even with active fans (mine doesn't), and some with different WiFi modules. These different revisions might not work with this Android port and you may get a bootloop. Unfortunately, I can't fix something I don't physically have. You assume all risk.

## ✨ Features

### 🎮 Controllers & input

- **Built-in gamepad spoofed as an Xbox controller** — the internal pad presents to Android/games as an **"Xbox Wireless Controller"** (`045e:02fd`), so games that expect a standard Xbox pad just work.
- **Flydigi VADER3 2.4GHz dongle → Xbox 360 (XInput)** — plug in the 2.4GHz dongle and the Flydigi is spoofed as a **"Microsoft X-Box 360 pad"** (`045e:028e`, XInput) and automatically re-ordered to be **Player 1** in games.
- **Switchable button layout (Xbox ↔ Nintendo)** — a **"Button Layout" toggle in the power-button menu** swaps the face buttons between **Xbox** style (default — A on the bottom) and **Nintendo** style (**A↔B and X↔Y swapped**), for games and emulators that assume a Nintendo layout. Works on **both** the built-in gamepad **and** the Flydigi (XInput) controller, flips **instantly — even mid-game** (no restart), and **persists across reboots**.
- **Full in-game mapping** — both analog sticks, the D-pad (hat axis), L1/R1, analog **L2/R2 on the correct sides**, L3/R3 as real stick-click buttons, A/B/X/Y, START/SELECT/HOME, and BACK all work in games and in the UI.
- **L3 + R3 virtual mouse** — tap the **L3+R3** chord to toggle an on-screen cursor; the right stick moves the pointer, **R3 = left-click**, and **hold R3 = scroll**. The screen does a brief **inverted-color flash** each time you toggle the mouse on/off so you always know the state.

### ⌨️ Shortcut combos

- **Brightness:** hold **SELECT + tap Volume Up / Volume Down** to step screen brightness in even **5% increments**. The native LineageOS brightness bar appears and fades out ~2 seconds after the last press. (SELECT stays passive — it's never "consumed", so it won't interfere with games.)
- **Kill all apps:** **double-tap SELECT + START** to close everything (works on both the built-in pad and the Flydigi).
- **Kill foreground app:** **long-press HOME** to force-close the app you're in.
- **Mouse toggle:** **L3 + R3** (see above).

### 🖥️ UI & system

- **Auto-hide navigation bar** with a mouse-summon hook — the nav bar stays out of your way and can be summoned when you need it.
- **Custom SyachOS boot animation** ("Starting SyachOS / Please Wait…").
- **SyachOS branding** throughout, with a custom gamepad-navigable home launcher (**"SyachOS Home"**).
- **Snappy UI** — tuned animation scales for a faster feel.
- **Power-menu performance toggle** — press-and-hold the power button to find a **3-mode performance switch** right beside the USB-mode toggle. **Tap to cycle in place** — *Powersave → Balanced → Performance* — and the menu stays open with the label updating on each tap. It retunes the **CPU governor + clock caps** and the **GPU governor** together, and your choice **persists across reboots**. Rough guide: **Powersave** for light/2D games and longer battery, **Balanced** (the default) for everyday play, and **Performance** for demanding 3D titles. Note: Performance runs the chip harder and this is a fanless handheld, so long sessions on Performance may thermally throttle — that's expected.
  - **Powersave** — CPU on the *schedutil* governor with a **408 MHz** floor and a **1.416 GHz** ceiling, so it never boosts into the top clocks; GPU forced to its **powersave** governor (held low). Coolest and longest battery — ideal for 2D / retro titles, menus, and emulators that don't need the headroom.
  - **Balanced** *(the default)* — CPU on *schedutil* scaling freely from **1.416 GHz up to the full 2.016 GHz** as load demands; GPU on **simple_ondemand**, clocking itself between **300–900 MHz** on demand. Best all-round for everyday play.
  - **Performance** — CPU pinned to the *performance* governor holding **1.416 → 2.016 GHz** (no down-clocking); GPU pinned to its **performance** governor at the full **900 MHz**. Fastest and hottest — because the device is fanless, thermal throttling starts to pull the CPU back toward **~1.416 GHz at roughly 82 °C** on long sessions, so you won't always hold the top clock.
- **Debloated** — 14 stock apps removed.
- **LeanbackIME** — a fully D-pad-navigable on-screen keyboard (no touchscreen needed).
- Suppressed nuisance notifications (Trust warning + serial-console notice).

### 🛒 SyMart — built-in app store & updater

**SyMart** is a built-in, Play-Store-style **online emulator & app store/updater** that installs and keeps your emulators and apps current **on-device, with no Google Play Store**. It bundles and/or downloads popular emulators and tools such as **PPSSPP, RetroArch (aarch64), NetherSX2 (classic), DraStic, Flycast, Mupen64Plus FZ, and Droid-ify** — A = install, B = back.

> [!WARNING]
> **Heads-up on emulator builds:** several emulators (e.g. **RetroArch** and **Flycast**) are pulled from their **official nightly / bleeding-edge** pages, so those builds can be **unstable or crash-prone**. If you want a rock-solid version instead, grab the official **stable release** yourself.

### 🔐 Root & microG

- **Root:** KernelSU-Next + NeoZygisk + Vector (LSPosed), baked in and **flash-proof** (survives reflashing).
- **microG** — account-free Google Play services replacement, including Play licensing (so native Android games that check for Play services can run without a Google account). Signature spoofing is handled at the kernel level.

### 📡 Connectivity & storage

- **WiFi** working (Rockchip RK915 driver). Note: WPA3/PMF (802.11w) is not supported by the chip firmware — it falls back cleanly to WPA2/CCMP.
- **MTP file transfer** to PC (Linux & Windows work out of the box; macOS needs a helper like OpenMTP / Android File Transfer).
- **Power-menu USB-mode toggle** — switch ADB ↔ File transfer right from the press-and-hold power menu (persists across USB replug).
  - ⚠️ **Turn File transfer OFF when you're done moving files.** Leaving USB in **File transfer (MTP)** mode makes the speaker emit a periodic **popping** sound whenever a **2.4GHz dongle** (or any USB peripheral) is connected to the port. Switch back to **ADB only** (the default) and the popping stops. It's harmless, but annoying during play.
- **Secured ADB** — requires the on-screen RSA "Allow USB debugging?" authorization (fully D-pad/gamepad confirmable), plus rooted adb on boot.

## 💾 SD card requirements

- Use a **genuine, name-brand microSD card** (SanDisk, Samsung, Lexar, Kingston, etc.). Counterfeit and no-name cards are the #1 cause of corruption and boot failures.
- **Minimum 32 GB.**
- For a good idea of which cards perform well on this class of RK35xx handheld, use the **R36S microSD compatibility list** as a benchmark: [R36S Compatibility List](https://handhelds.wiki/R36S_Compatibility_Lists#TF2_Compatibility_⚠️)

## ⬇️ Installation

1. Get a genuine, name-brand microSD card (32 GB minimum) and a card reader.
2. Download the latest **SyachOS** image.
3. Flash the image to the **entire card** with a tool such as `dd`, Balena Etcher, or Rufus. (Example on Linux: `sudo dd if=SyachOS.img of=/dev/sdX bs=4M conv=fsync status=progress` — replace `/dev/sdX` with your card, and double-check it.)
4. Insert the card into the RG52 Mini and power on. First boot runs a one-time userdata resize and may reboot once — this is normal.
5. Enjoy. If something isn't accessible by D-pad / joystick, use the virtual mouse (L3 + R3).

## 🧩 Kernel source (GPL)

In keeping with the GPL, the kernel source (including the KernelSU-Next integration) is published here:

[github.com/syach1/kernel_rk3562_rg52mini](https://github.com/syach1/kernel_rk3562_rg52mini)

## ☕ Support this project

> [!NOTE]
> **Using AI costs real money.** Please be considerate when asking for bug fixes or features you'd like. To help keep this possible, please consider buying me a coffee at [ko-fi.com/syach1](https://ko-fi.com/syach1). Every bit helps. 🙏

## 🙏 Credits

- **LineageOS** — the base ROM.
- **microG** — account-free Google services replacement.
- **KernelSU-Next** — kernel-based root.
- **bmdhacks** — the RK3562 kernel base.
- **TheGammaSqueeze / GammaOS** — reference and inspiration for RK35xx handheld ports.
- **syach1** — SyachOS build, integration, and tuning.

---

> [!CAUTION]
> Again: **no warranty, use at your own risk, you can brick your device, and this firmware was largely AI-coded.** Don't use it for anything security-sensitive.
