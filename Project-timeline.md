# PhoneRemote — Project Plan & Timeline

**Project:** Desktop Remote Control App (Windows server + Android client)
**Developer:** Solo (experienced programmer, new to C#)
**Availability:** 1–2 hours/day (~10 hrs/week)
**Start Date:** February 2026
**Stack:** C# .NET (server) · Kotlin/Jetpack Compose (Android client)
**Transport:** Wi-Fi UDP (mouse) · Bluetooth Classic (keyboard/media/fallback)

---

## Project Summary

A lightweight, low-latency app that turns an Android phone into a mouse, keyboard, and media remote for a Windows PC. Uses a hybrid Bluetooth + Wi-Fi UDP architecture to combine reliability with speed.

---

## Assumptions & Constraints

- Developer has strong programming background (React, JS, web dev, technical writing)
- New to C# but will learn contextually while building (no dedicated syntax phase)
- 1–2 hours/day (~10 hrs/week, ~40 hrs/month)
- Personal use first, potential publish later
- No branding or marketing needed initially
- Android only (iOS deferred)
- No screen mirroring or file transfer in scope
- Claude available as pair-programming partner throughout

---

## Phase 0 — Setup & Proof of Concept

**Duration:** Days 1–4 (~6 hours)
**Goal:** Dev environment ready, first cross-device communication working

| Day | Task | Hours | Deliverable |
|-----|------|-------|-------------|
| 1 | Install Visual Studio, .NET 8 SDK, Android Studio | 1.5 | Dev environment ready |
| 2 | C# UDP server — listen for packets, log to console | 1.5 | Server receives UDP messages |
| 3 | Android app — simple touchpad UI, send UDP packet on touch | 1.5 | Android sends touch data over network |
| 4 | Wire `SendInput` — receive UDP → move Windows mouse | 1.5 | Phone touch moves PC mouse (raw) |

**Milestone 0:** ✅ Phone moves PC mouse — ugly but functional proof of concept

---

## Phase 1 — Mouse Control (MVP)

**Duration:** Week 1–2 (~16 hours)
**Goal:** Smooth, low-latency mouse control with full functionality

| Day | Task | Hours | Deliverable |
|-----|------|-------|-------------|
| 5–6 | Design binary UDP protocol (position deltas, click flags, scroll) | 3 | Protocol spec finalized |
| 7–8 | Implement protocol on both sides | 3 | Structured packets flowing |
| 9 | Left click, right click, double-click, long-press for right-click | 1.5 | Click actions working |
| 10 | Two-finger scroll (vertical + horizontal) | 1.5 | Scroll working |
| 11 | Sensitivity settings, acceleration curve, dead zone filtering | 1.5 | Mouse feels natural |
| 12 | Client-side predictive movement + visual feedback on phone | 1.5 | Feels instant |
| 13 | Latency profiling and optimization pass | 1.5 | Measured and optimized |
| 14 | Bug fixes, edge case testing | 1.5 | Stable mouse control |

**Milestone 1:** ✅ Polished mouse/touchpad control over Wi-Fi UDP

---

## Phase 2 — Keyboard Input

**Duration:** Week 3–4 (~14 hours)
**Goal:** Full keyboard input from phone to PC over Bluetooth

| Day | Task | Hours | Deliverable |
|-----|------|-------|-------------|
| 15–16 | C# Bluetooth Classic SPP listener (32feet.NET) | 3 | Server accepts Bluetooth connections |
| 17–18 | Android Bluetooth Classic client + pairing flow | 3 | Phone pairs and connects to PC |
| 19 | Key mapping — Android key events → Windows virtual key codes | 1.5 | Mapping table complete |
| 20–21 | On-screen keyboard UI (QWERTY, numbers, symbols) | 3 | Custom keyboard rendered |
| 22 | Special keys — Ctrl, Alt, Shift, combos, arrow keys, F1–F12 | 1.5 | Full modifier support |
| 23 | End-to-end testing, keystroke reliability validation | 1.5 | No dropped keystrokes |
| 24 | Bug fixes | 1.5 | Stable keyboard input |

**Milestone 2:** ✅ Full keyboard input over Bluetooth — phone is a wireless keyboard

---

## Phase 3 — Media Controls & Hybrid Transport

**Duration:** Week 5–6 (~12 hours)
**Goal:** Media remote + seamless Wi-Fi/Bluetooth auto-switching

| Day | Task | Hours | Deliverable |
|-----|------|-------|-------------|
| 25 | Media key injection — play, pause, volume, next, prev | 1.5 | Media keys work from server |
| 26 | Android media remote UI — clean button layout | 1.5 | Dedicated media screen |
| 27–28 | Transport auto-negotiation — detect shared Wi-Fi network | 3 | App detects best transport |
| 29–30 | Fallback logic — Wi-Fi down → Bluetooth handles everything | 3 | Seamless failover |
| 31 | Connection status indicator on Android | 1.5 | User sees active transport |
| 32 | Integration testing across transport switches | 1.5 | Reliable switching |

**Milestone 3:** ✅ Media controls + intelligent hybrid transport

---

## Phase 4 — Polish & Daily-Driver Quality

**Duration:** Week 7–8 (~14 hours)
**Goal:** App feels professional and reliable for daily use

| Day | Task | Hours | Deliverable |
|-----|------|-------|-------------|
| 33–34 | Auto-discovery — mDNS/broadcast so phone finds PC automatically | 3 | Zero-config setup |
| 35 | Auto-reconnection on disconnect (Wi-Fi drop, Bluetooth range) | 1.5 | Survives interruptions |
| 36–37 | Android UI polish — navigation between mouse/keyboard/media, dark mode | 3 | Clean, professional UI |
| 38 | Windows system tray app — minimize to tray, auto-start on boot | 1.5 | Server runs silently |
| 39 | Settings screen — sensitivity, preferred transport, layout options | 1.5 | Configurable |
| 40 | Multi-device testing, final bug fixes | 1.5 | Works on different phones/PCs |
| 41–42 | Stress testing — 1+ hour sessions, rapid input, transport switching | 3 | Release candidate |

**Milestone 4:** ✅ Polished, reliable app ready for daily personal use

---

## Timeline Summary

| Phase | Duration | Cumulative | Milestone |
|-------|----------|------------|-----------|
| Phase 0 — Proof of Concept | Days 1–4 | ~4 days | Phone moves PC mouse |
| Phase 1 — Mouse MVP | Week 1–2 | ~2 weeks | Full mouse control |
| Phase 2 — Keyboard | Week 3–4 | ~4 weeks | Keyboard over Bluetooth |
| Phase 3 — Hybrid Transport | Week 5–6 | ~6 weeks | Media + auto-switching |
| Phase 4 — Polish | Week 7–8 | ~8 weeks | Daily-driver quality |

**Total estimated time: ~8 weeks (~62 hours)**

---

## Risk Register

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| Bluetooth Classic API complexity on Android | High | Delays Phase 2 | Prototype BT connection in Phase 0 day 4 if ahead of schedule |
| Windows Bluetooth stack unreliable | Medium | Delays Phase 2 | Use 32feet.NET library; TCP WebSocket as backup transport |
| Wi-Fi firewall blocks UDP | Medium | Breaks Phase 1 | Add TCP fallback, provide user-facing troubleshooting guide |
| C# learning curve slows progress | Low | Minor delays | Claude as pair-programming partner; strong existing dev background |
| Android Bluetooth permissions (Android 12+) | Medium | UX friction | Handle runtime permissions properly from day 1 |

---

## Tech Stack Summary

| Component | Technology |
|-----------|-----------|
| Windows Server | C# / .NET 8, Win32 `SendInput` via P/Invoke |
| UDP Networking | `System.Net.Sockets.UdpClient` |
| Bluetooth Server | 32feet.NET library (Bluetooth Classic SPP) |
| Android Client | Kotlin, Jetpack Compose |
| Android Bluetooth | Android Bluetooth Classic API |
| Android Networking | Raw UDP sockets (`java.net.DatagramSocket`) |
| Protocol | Custom binary (mouse: UDP, keyboard/media: Bluetooth SPP) |

---

## Definition of Done (v1.0 — Personal Use)

- [ ] Phone controls PC mouse smoothly with <35ms perceived latency
- [ ] Keyboard input works reliably with no dropped keystrokes
- [ ] Media controls (play/pause, volume, skip) functional
- [ ] App auto-discovers PC on the network
- [ ] Falls back to Bluetooth when Wi-Fi unavailable
- [ ] Server runs in system tray without interfering with other apps
- [ ] Works reliably for 1+ hour sessions without disconnection

---

## Future Scope (Post v1.0, if publishing)

- iOS client (Swift/Flutter)
- Custom macro/shortcut buttons
- Gesture support (pinch-to-zoom, three-finger gestures)
- Screen mirroring (low priority)
- Presentation mode (slides control)
- Google Play listing, branding, landing page
- Encryption for Bluetooth/UDP channels
