# HANDOFF — kmz-to-epanet

**Disposition:** FROZEN — awaiting Nikabou's return (his project; not reassigned).
**Handoff date:** 2026-07-06

## Purpose
Browser-based tool that converts Google Earth **KMZ/KML → EPANET `.inp`** format for water-network modeling. Public repo.

## Structure & how to run
Pure static HTML — **no build, no server, no deploy pipeline.** Open the file directly in a browser:
- `kmz_to_epanet_v5.html`, `kmz_to_epanet_v6.html` — converter versions
- `HydroForge-v8.html` — latest, adds satellite preview + EPANET backdrop
- **Not** published to GitHub Pages; run locally.

## In-flight work (frozen)
Branch **`add-hydroforge-v8`** (pushed 2026-07-06):
- **HydroForge v8** — satellite preview + EPANET backdrop generation, elevation-API fixes, optional ZIP bundle. Built & tested.
- **RESUME POINT:** verify backdrop rendering **after the Maps Static API is enabled** on the `water4-org` GCP project.
- Also contains a second commit: an **untested WIP edit to `kmz_to_epanet_v5.html`** (194 lines), committed only to preserve it at handoff — review before building on it.

## ⚠️ API key (public repo — do not leak)
`HydroForge-v8.html` (~line 1100) needs a Google API key with **Elevation** + **Maps JavaScript/Static** APIs. The committed value is a placeholder: `PASTE_YOUR_GOOGLE_API_KEY_HERE`.
- The real key lives in the **water4-org GCP console → APIs & Services → Credentials** (created under water4-org, so it survives Nikabou's leave).
- **Never commit the real key** — this repo is public. Paste it locally only.

- ## Maps API key restriction (added 2026-07-21)

The Google Maps key is now referrer-restricted to `http://localhost:*/*` (and API-restricted to elevation/maps/static-maps). This applies to kmz_to_epanet_v6.html on master and HydroForge-v8.html on the add-hydroforge-v8 branch: opening either directly as a file (`file://`) sends no referrer, so Maps/Elevation calls will fail with a key error. Serve locally instead:

    python3 -m http.server
    
then open http://localhost:8000/kmz_to_epanet_v6.html (or the HydroForge file on its branch). Key value lives in the GCP console (public repo, never commit it). A $25/mo Maps budget alert is set; any alert email means investigate.
