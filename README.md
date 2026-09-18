# 🆘 TouristSafetyApp — Offline SOS for Remote Travel

**Live demo:** https://YOUR-USERNAME.github.io/touristsafetyapp/
*(update this link once GitHub Pages is live — see Setup below)*

TouristSafetyApp is a concept safety app for tourists, trekkers, and travellers heading into areas with **no cellular signal** — forests, mountain trails, remote coastlines. It uses a **phone-to-phone offline mesh network** so an SOS or accident alert can still reach help, even when no single device in the chain has signal on its own.

---

## The problem

Tourists in remote areas often have no way to contact family, hotels, guides, or rescue teams in an emergency, because there's simply no cell tower nearby. A phone with zero bars is a phone with zero safety net.

## The solution

A wearable / mobile-linked system where every nearby traveller's device becomes a relay node. An emergency message hops from device to device — Tourist A → Tourist B → Tourist C → Guide/Rescue Gateway — until it reaches a device that *does* have signal (a ranger post, a village edge, a guide's satellite messenger), which forwards it on to real Police, an emergency contact, and — for accidents — the nearest hospital.

```
Tourist A --> Tourist B --> Tourist C --> Guide/Rescue Gateway --> Police / Contact / Hospital
   (no signal)     (relay)        (relay)         (has signal)
```

---

## What this repo contains

This repo holds a **working front-end prototype** (`index.html`) built to demonstrate the concept and user flow at a hackathon. It's a single self-contained HTML/CSS/JS file — no build step, no dependencies, works completely offline once loaded.

### Features demonstrated in the prototype
- **Hold-to-SOS button** — alerts Police, an emergency contact, and the group guide
- **Report Accident** — same alert chain, **plus the nearest hospital automatically** (accidents and danger situations route differently on purpose)
- **Silent alert** — sends the same SOS with no sound or screen flash, for situations where drawing attention is dangerous
- **Mesh network view** — animated visualization of how a message relays device-to-device to a gateway
- **Contacts management** — Police is fixed; friend, guide, and hospital contacts are editable
- **Offline alert log** — every alert is saved on-device (localStorage) with a timestamp and a generated trackable link, so there's a record even before a connection is ever regained

---

## How this would work in a real deployment

| Layer | Technology |
|---|---|
| Phone-to-phone relay | Bluetooth Low Energy mesh (similar approach to goTenna / Bridgefy) — roughly 30–100m per hop |
| Longer range across a trail | A low-cost LoRa module (e.g. ESP32 + SX1278, ~$8) worn or carried — kilometre-range hops between spread-out trekkers |
| The "gateway" | Any device in the mesh that regains signal (ranger post, village edge, guide's satellite messenger) auto-forwards the queued alert |
| Reaching real responders | Gateway forwards via SMS gateway API (e.g. Twilio) or a direct feed to local police control rooms and the nearest hospital, using the alert's GPS coordinates |
| Fall / accident detection | Phone accelerometer + gyroscope pattern (sudden freefall + impact + no movement after) triggers the accident flow automatically, no button press needed |

---

## Setup — hosting this yourself

1. Clone or fork this repo.
2. In **Settings → Pages**, set Source to "Deploy from a branch", branch `main`, folder `/ (root)`.
3. GitHub will publish `index.html` at `https://YOUR-USERNAME.github.io/touristsafetyapp/`.
4. Update the live demo link at the top of this README once it's live.

No build tools, package managers, or servers required — it's a static site.

---

## Tech stack (prototype)

- Vanilla HTML, CSS, JavaScript (no framework, no dependencies)
- LocalStorage for on-device offline alert history
- Inline SVG for the mesh network visualization

## Roadmap / what's next

- [ ] Real BLE mesh implementation (React Native or Flutter + native mesh libraries)
- [ ] LoRa hardware companion device integration
- [ ] Real accelerometer-based fall detection
- [ ] Backend gateway service (SMS/API forwarding to police & hospital systems)
- [ ] Offline cached maps and marked danger zones
- [ ] Voice-triggered ("codeword") SOS

## License

MIT — see [LICENSE](LICENSE).
