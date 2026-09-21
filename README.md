# Community Health Experience Passport

An interactive digital passport for the Abu Dhabi Public Health Centre community
health showcase. Visitors register with their name, explore health departments,
collect a stamp at each activity by scanning that activity's QR code, and unlock
a gift after completing **3 of 5** activities.

> ### ⚠️ Prototype — demonstration and testing only
> This version stores all data in the visitor's own browser. It is **not ready
> for live event use**. See [Current limitations](#current-limitations) below.

---

## Live demo

Once GitHub Pages is enabled, the app is available at:

```
https://YOUR-USERNAME.github.io/adphc-passport/
```

Open it on a phone. HTTPS is required for the in-app camera scanner to work.

---

## How it works

1. A visitor scans the entrance QR code, or opens the link directly
2. They register with **their name only**
3. They choose a department and their passport page opens
4. Tapping an activity circle opens the camera scanner
5. Scanning that activity's QR code presses an ink stamp onto the page
6. After **3 of 5** stamps, a gift celebration appears
7. Staff verify the pass at the gift desk

Progress is saved automatically and survives a page refresh.

---

## Privacy

The application collects a **name only**, which is stored in the visitor's own
browser and never transmitted anywhere.

It does **not** ask for, store or send:

- Email addresses
- Telephone numbers
- Emirates ID or employee numbers
- Any medical or health information

No analytics, tracking or third-party data collection is present.

---

## Project structure

```
index.html          The entire application — UI, logic and data layer
adphc-logo.jpg      Official ADPHC logo
```

No build step, no package manager, no server-side code. It is a single static
page that runs entirely in the browser.

---

## Running it locally

Serve the folder over HTTP — opening `index.html` directly from disk
(`file://`) will block the camera.

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000/index.html>. `localhost` counts as a secure
context, so the camera scanner works there.

---

## Demo controls

The floating **Demo controls** button on the participant screens lets you
simulate an activity scan without printing anything. It runs the real stamping
logic, the real duplicate check and the real gift rule — nothing is bypassed.

This is the quickest way to test the 3-of-5 gift rule.

---

## QR codes

The application generates every QR code it needs. Sign in to
**Admin → QR Codes** and use *Print / save as PDF* to produce:

| QR code | Purpose |
|---|---|
| Entrance | Registration / reopening a passport |
| Five activity codes | One per activity, collects that stamp |
| Admin dashboard | Opens the admin sign-in screen |
| Staff gift desk | Opens the staff sign-in screen |

**No QR code contains a password or access code.** The admin and staff codes open
a sign-in screen and nothing more.

> **Important:** QR codes are generated from the address the page is currently
> served at. Print them only once the app is at its final address — codes made
> from a different address will not work.

---

## Access codes

Access codes for the admin dashboard and staff gift desk are **not published in
this repository**. They are held as SHA-256 digests in the source, so reading the
page does not reveal them.

Contact the project owner for the codes.

> This is obfuscation, not authentication. The check runs on the visitor's own
> device, so a short code could still be brute-forced offline. Proper staff
> authentication must be server-side before live-event use.

---

## Current limitations

The prototype uses browser storage (`localStorage`) on each visitor's device.

| | |
|---|---|
| ❌ Data is **not shared between devices** | Each phone holds only its own passport |
| ❌ The admin dashboard is **not an event dashboard** | It shows only the browser it is opened in |
| ❌ The staff desk **cannot verify other phones** | Only passports created in that same browser |
| ❌ Stamps are **not tamper-proof** | Editable through browser developer tools |
| ❌ Clearing browser data loses the passport | Recoverable within the same browser via Passport ID |

### What a live event would require

A central database (Power Pages + Dataverse, or equivalent) to provide:

1. Registrations combined across all visitor devices
2. A genuine event-wide admin dashboard
3. Cross-device gift verification at the staff desk
4. Server-side stamp validation and gift eligibility
5. Real staff and admin authentication

The application is built with a swappable data layer so a backend can be
connected without rebuilding the interface.

---

## Browser support

| | |
|---|---|
| iPhone | Safari, iOS 11+ |
| Android | Chrome |
| Desktop | Chrome, Edge, Firefox, Safari |

The camera scanner requires **HTTPS** (or `localhost`). If the camera cannot
start, printed QR codes still work with the phone's own camera app, which opens
the same link.

---

## Status

**Suitable for demonstration, rehearsal and device testing.**

Not approved for live event use while it relies on browser storage alone.

---

*Abu Dhabi Public Health Centre — Community Health Experience Showcase*
