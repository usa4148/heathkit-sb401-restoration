---
title: "Heathkit SB-401 Transmitter — Restoration Plan"
subtitle: "Rev. 1.3 — built from the Heath manual (595-947-10), service bulletins and field sources"
date: "November 2026"
geometry: margin=0.9in
fontsize: 10pt
colorlinks: true
linkcolor: black
urlcolor: black
citecolor: black
toccolor: black
toc: true
---

<!-- Build: pandoc sb401-restoration-plan.md -o sb401-restoration-plan.pdf --pdf-engine=xelatex -V mainfont="DejaVu Serif" -->

> **DANGER — LETHAL VOLTAGE.** The SB-401 runs a voltage-doubler plate supply that reads **about 800 V DC** on its own HV meter position (manual p. 90) and runs about 720 V under load. The manual: *"This Transmitter has operating voltages up to 800 volts; ... These voltages can be fatal."*
>
> - **Unplug** the line cord. The FUNCTION switch alone does not remove the supply.
> - **Discharge** the high-voltage capacitors the way the manual does (p. 94): touch the screwdriver blade to the chassis *first*, then to the lower lead of feedthrough capacitor **Q**. Repeat several times.
> - **Verify with a meter** on a high-voltage range before touching anything. Do not rely on the panel meter.
> - Keep **one hand in your pocket** when the unit is live. The 6146 plate caps are at plate voltage whenever the transmitter is on.
> - Use a **50 Ω non-reactive dummy load** for every transmit test. **Never a light bulb** (the manual says so twice).
> - **Do not key the transmitter for more than 30 seconds at a time** (manual p. 95, and service bulletin SB-401-8). The 6146s are the one part of this rig that cannot be replaced casually.

# 1. Source documents

| Document | Where | Use |
|---|---|---|
| **Heath SB-401 Assembly and Operation Manual**, 595-947-xx (©1966; schematic dated 8-2-68). Two copies were used: the **full 88-page image scan supplied by the owner** (`sb-401.pdf`, pp. 1–154 plus the fold-out schematic), and the archive.org OCR text of the "Condensed Manual" 595-947-10 | Owner's scan; Internet Archive item `assemblyoperatio00unse_0` (Ron Patterson W6FM / DLARC collection) | **Primary reference.** Parts lists #1–#5, initial test (pp. 87–90), alignment (pp. 90–97), tune-up charts (pp. 114–116), in-case-of-difficulty and troubleshooting chart (pp. 117–120), specifications (pp. 121–123), **circuit description with the power-supply and metering figures (pp. 125–138)**, X-ray views (pp. 139–140), **voltage and resistance charts (pp. 145–146)**, **LMO schematic (p. 147)**, replacement parts price list (pp. 148–154), and the **full schematic**. |
| **Heath SB-401 service bulletins** (SB-401-1D through SB-401-16; SB-400-1/2/3) | Heath mailing list: 1997 and June 1998 transcriptions (Joe Lutz W7LPF; the 1998 post is the one AF6C links, retitled "Complete 1966-89") and 2014 repost (Van Lincoln WD8AAM); nostalgickitscentral.com | Factory-documented fixes. Indexed in §5.2. |
| W2JDL, "The Heathkit SB401 Transmitter," *73 Magazine*, July 1967, pp. 98–100 | PDF supplied by owner | Contemporary build-and-review: circuit walk-through, SB-400 comparison, the 680 Ω finals resistor, RG-62 interconnect cables, and the CW/transceive switch setting. |
| Heathkit group (groups.io), "SB 401 is here and the...", May 2024 (AF6C, WB4GRA, W7EKB, KB2QIU) | Pasted by owner (page 2 of 3 only) | Crystal list for the SBA-401-1 pack and the seven "undo" steps for running the manual's Initial Test on a built unit (§4.1). |
| AF6C, *Heathkit of the Month #43: SB-401* (Oct. 2012) | w6ze.org/Heathkit/Heathkit_043_SB401.pdf | Circuit description, SB-400 vs SB-401 differences, tube line-up, serial/date notes, the RL-2 hang-up fix. |
| *Heathkit SB-401 Amateur Transmitter* restoration (Feb. 2021) | heathkit-interests.blogspot.com | Replacement electrolytics, resistor drift measurements, the P.E.C. network. |
| *SB-301/SB-401 Functional Repair Guidelines* thread (Oct. 2010: WB4LNM, WA2CKY, K9STH, W7EKB) | puck.nether.net/pipermail/heath | Practical recap order, grounds, cables, power cord. |
| *SB-401 Info/Experience needed* (Apr. 2008, N0JMY) | puck.nether.net/pipermail/heath | Which electrolytics a recap kit covers. |
| *Finals going bad in Heathkit SB-401 transmitter?* (Jul. 2011) | rec.radio.amateur.boatanchors (Google Groups) | 80 m neutralization and tune-up field thread. |
| G3OOU, *Heathkit SB Line — Where Next?* | qsl.net/g3oou | General SB-line ageing notes; 6146 and carbon-comp comments. |
| Kembel, *Heathkit HW-101 and SB-10x Restoration and Troubleshooting* (rev. Dec. 17, 2021, 190 pp.) | PDF supplied by owner | Not SB-401-specific, but it carries the **LMO part-number table**, **K9STH's tube-LMO repair** and KI4IUA's stuck-LMO repair, the Heath **filter table** (404-283 is the SB-401's SSB filter), and general SB-line servicing practice (p. 116–132, 101–105). |
| **Heathkit-Radios** (groups.io), "sb-401 lmo," Apr. 29 – May 2, 2026 (messages 22979–22994) | Pasted by owner | One SB-401 LMO fault and its fix (§3.5, §5.1). *The rest of the group was not searched (§11).* |
| EEVblog forum, antiqueradios.com thread t=422212 | eevblog.com, antiqueradios.com | *Not retrieved for this revision (§11).* |

**Manual page references use the manual's printed page numbers.** The owner's scan is image-only, so figures and chart values in this revision were read by eye from the page images (the archive.org copy has an OCR text layer only, and the charts and schematic do not survive in it). Values read from the voltage chart are marked as such and should be confirmed on the page before you condemn a part.

**Numbering scheme (schematic note 1):** 0–99 chassis parts; 100–199 carrier generator board; 200–299 mixer-bandpass board; 300–399 terminal board #1; 400–499 terminal board #2. Resistors are 1/2 W unless marked. The SB-400 uses *different* designators (for example R71 on the SB-400 is R402 on the SB-401), so do not mix SB-400 and SB-401 documents without a cross-reference.

# 2. Transmitter at a glance

## 2.1 Factory specifications (manual pp. 121–123)

| Item | Spec |
|---|---|
| Coverage | 3.5–4.0, 7.0–7.5, 14.0–14.5, 21.0–21.5, 28.0–28.5, 28.5–29.0, 29.0–29.5, 29.5–30.0 MHz (eight 500 kHz segments) |
| Mode | SSB (selectable USB/LSB), CW. **No AM** (the MODE switch has an AM position; the manual's circuit does not provide AM) |
| DC input | **180 W PEP SSB; 170 W CW** |
| RF output | **100 W** on 80–15 m; **80 W** on 10 m (50 Ω non-reactive) |
| Output impedance | 50–75 Ω, SWR below 2:1 |
| Stability | < 100 Hz/hr after 20 min warm-up; < 100 Hz for ±10% line change |
| Dial accuracy | Within 200 Hz; within 400 Hz after calibration at the nearest 100 kHz point |
| Carrier suppression | 55 dB below rated output |
| Unwanted sideband | 55 dB down at 1000 Hz and higher |
| Oscillator feedthrough / mixer products | 55 dB down (45 dB at the 3910 kHz crossover) |
| Harmonics | 35 dB below rated output |
| Third-order distortion | 30 dB down from rated PEP |
| Audio response | 350–2450 Hz ±3 dB |
| Audio input | High-impedance mic or phone patch (600 Ω RCA) |
| CW | Break-in by VOX from a keyed tone (grid-block keying); about 1000 Hz sidetone, switched to the speaker |
| Power | 105–125 / 210–250 VAC, 50/60 Hz; **80 W standby, 260 W CW key-down** |
| Fuse | **4 A slow-blow at 120 V; 2 A at 240 V** (the 2 A is not supplied) |
| Pilot lamps | **#47** |
| Size / weight | 14-7/8 × 6-5/8 × 13-3/8 in.; manual says 26-1/2 lb (shipping weight was about 34–36 lb) |
| Semiconductors | 5 crystal diodes (balanced modulator, relative power) and 12 silicon diodes |

Production and price: first shipments Sept. 1966; kit price **$285** (Radio Electronics ad, Dec. 1966); produced into 1975–76. The **SB-400** (1964) was the predecessor and cost $325. AF6C dates the change to the **dual-primary power transformer** (54-198, 120/240 V) to about **fall 1968**; earlier SB-401s have the single 120 V transformer (54-143).

## 2.2 Tube complement (manual p. 123; AF6C Table 4)

| V | Tube | Function | Failure notes |
|---|---|---|---|
| V1 | 6EA8 | Mic preamp / cathode follower | Heater-cathode leakage → hum |
| V2 | 6AV11 (triple triode) | LSB, USB/CW carrier oscillators and cathode follower | Compactron-style; hard to test |
| V3 | 6AU6 | Isolation amp / ALC-controlled stage | Gassy → ALC misbehaves |
| V4 | 6EW6 | LMO mixer | Moderate |
| V5 | 6EW6 | Heterodyne mixer | Moderate |
| V6 | **6BZ6** | LMO (inside LMO 110-40) | See note below |
| V7 | OA2 | 150 V regulator for LMO and heterodyne oscillator | Dim/unstable glow → drift |
| V8 | 6AW8 | Heterodyne oscillator and receiver het-osc amp | Moderate |
| V9 | **6CL6** | RF driver | Weak → low drive on all bands |
| V10, V11 | **6146** | Final amplifiers (parallel, class AB1) | **Wear item.** Gas, low emission, screen secondary emission |
| V12 | 6D10 (triple triode) | VOX amp, relay amp, sidetone amp | Hard to test; VOX and relay faults |
| V13 | 6J11 (dual pentode) | Anti-VOX amp and sidetone oscillator | Hum, VOX weirdness |

*LMO tube note:* the manual's tube list (p. 123) and AF6C both give **6BZ6** for the LMO in the SB-401 (the SB-400's LMO 110-13 used a 6AU6). The SB-301 plan found that its LMO used a **6CB6** per the manual, not the 6BZ6 the AF6C article implied. **Sources disagree on the LMO part number too:**

| Source | SB-401 LMO |
|---|---|
| Heath manual (parts lists #3/#5 and price list p. 151: **"100-40" Linear master oscillator, $63.30**, with the LMO schematic p. 147 labelled **6BZ6**; the archive.org OCR misreads the number as 110-40) | **100-40**, V6 = 6BZ6 |
| AF6C | 110-13 (SB-400); 110-32, then **110-40 from 1968**; both SB-401 versions 6BZ6 |
| Bulletin SB-401-1D | 110-32 is no longer available; use **100-40-LMO** |
| Kembel, Table 12 (p. 116) | SB-401 **110-32**, 6BZ6 (his table also lists the SB-101's 110-40 as 6CB6 and the SB-301's 110-40 as 6BZ6) |

Kembel's text distinguishes the two by construction: **110-32 has a large, thick gear on the tuning-capacitor shaft; 110-40 has a small, thin one** (p. 125). That matters for the grounding-braid repair in §4.6. **Open the LMO and read its label and look at the gear before buying a tube or a braid kit.** Fit the tube type the LMO is marked for, and ideally the same brand, because the LMO is calibrated with its tube.

*Typo check:* AF6C's prose calls V1 a "6EA6" in one place; his own table and the manual say **6EA8**.

## 2.3 How it works (AF6C; manual circuit sections)

- **Signal path (SSB):** mic → V1A preamp → V1B cathode follower → four-diode balanced modulator (carrier from V2) → V3 isolation amp (ALC acts here) → 3395 kHz crystal filter (404-283) → V4 mixes with the 5.0–5.5 MHz LMO (V6) → 8.395–8.895 MHz bandpass coupler → V5 mixes with the crystal heterodyne oscillator (V8) → band-switched driver V9 → 6146 pair → pi network.
- **Crystal filter:** Heath **404-283** (smaller case; replaced the SB-400's 404-200). Kembel's table gives 2.1 kHz at −6 dB and 5 kHz at −60 dB, shared with the SB-301, SB-310 and SB-101 (p. 101). A secondhand 404-283 with a 30 dB passband dip had a broken PCB track inside (p. 105), so a filter that is dull or lossy is repairable.
- **Carrier frequencies:** LSB 3393.6 kHz, USB 3396.4 kHz, CW **3395.4 kHz** (CW transmits 1 kHz above the dial frequency so the receiver beat note is 1 kHz). The USB and LSB crystals and the eight heterodyne crystals come from the receiver in transceive, or from the optional **SBA-401-1 crystal pack**. Only the CW crystal (Y10) ships with the kit.
- **SBA-401-1 pack, as AF6C lists it:** ten crystals, 3393.6 kHz (LSB carrier), 3396.4 kHz (USB/CW carrier), and heterodyne crystals 12.395 (80 m), 15.895 (40 m), 22.895 (20 m), 29.895 (15 m), 36.895, 37.395, 37.895 and 38.395 MHz (the four 10 m segments). Subtract 8.895 MHz from a heterodyne crystal to get the dial frequency at LMO zero. The kit's own CW crystal is **404-215 (3395.4 kHz)**. The SB-301 also carries a 23.895 MHz crystal (15 MHz WWV) and a 3392.110 kHz RTTY crystal, which the transmitter does not use. W7EKB says the SB-401's crystals are the same as the SB-series transceivers', and WB4GRA says a **crystal switch board 85-132-1** from an SB-10x, with its crystals, works as a source.
- **Heterodyne crystals (SBA-401-1):** Y1 38,395.0 · Y2 37,895.0 · Y3 37,395.0 · Y4 36,895.0 · Y5 29,895.0 · Y6 22,895.0 · Y7 15,895.0 · Y8 12,395.0 kHz; Y9 3396.4 USB; Y11 3393.6 LSB.
- **Final:** two 6146s in parallel, class AB1. **Idle plate current about 50 mA total** (the manual's BIAS ADJUST step; ~25 mA each) at a bias of about **−50 V**. Standby cuts the tubes off by removing **screen voltage** (the grids sit at −170 V DC in STBY, manual p. 90).
- **Tank:** 250 pF tuning cap; 245/245/354 pF three-gang loading cap; **100 pF and 200 pF** fixed loading caps added on 40 and 80 m; tapped silver-plated coil plus separate 10 m air coil. The 20/15/10 m settings use only the two 245 pF sections; 40/80 m use all three.
- **Neutralization:** a small coupling cap plus a trimmer (the "neutralizing capacitor") feeds plate RF back to the driver-plate B+ end, with an RF choke isolating it from the supply.
- **8.6 MHz trap:** a series LC trap in the V9 grid circuit (C303, adjusted on terminal board #1) removes an LMO/BFO mixing product near the top of 40 m.
- **Metering** (0–1 mA, 100 Ω): GRID (across a 4.7 kΩ resistor; about 0.1 mA SSB, 0.5 mA CW), PLATE (six 10 Ω resistors in parallel in the final cathodes; 0–500 mA), ALC (bridge), HV (500 kΩ multiplier; reads **one-half** of the supply, so the dial is "×100" and shows about 800 V), REL PWR (rectified RF sample).
- **T/R:** a six-pole relay (RL1), driven by the VOX/relay amp V12B. Contacts switch: the accessory-socket line voltage; **screen voltage plus the internal antenna relay (RL2)**; RCVR MUTE and LINEAR RELAY; ALC/ground at V3; cutoff bias at V9; and speaker between receiver audio and sidetone.

## 2.4 Power supply (AF6C §1; manual parts lists)

- **Transformer** 54-143 (early) or 54-198 (dual primary). Filaments are a 12.6 V centre-tapped winding: one half runs both 6146s and V9, the other half runs the rest of the tubes and the lamps.
Per the manual's Figure 6-15 (p. 136):

- **High voltage:** the red / red-yellow secondary (about 275 VAC) feeds **D5–D8** in a full-wave doubler charging **C78 and C79, 125 µF each (25-34)**. **R44 and R45, 100 kΩ 2 W**, sit across them as bleeder/equalizers. Output **720 VDC at 250 mA full load**.
- **Low voltage:** the brown / brown-yellow winding (**95 VAC**) feeds a half-wave doubler (**D3, D4, C81 100 µF**) into a pi filter: **C77A 40 µF, C77B 100 µF** (the 100-40 can, 25-59), **R41 100 kΩ 2 W** bleeder and the **4.5 H filter choke** (46-43). Output **250 VDC at 100 mA**. **V7 (OA2)** regulates the LMO and heterodyne oscillator at 150 V.
- **Bias:** the blue winding (about 125 VAC) feeds **D2**, **C403 and C404 (20 µF each)** and **R412 (1000 Ω, 1 W)**. **−170 VDC no load**; dividers make the **−45 to −70 V** bias range and the other negative rails.
- **Filaments:** a separate winding (yellow, green, yellow-green leads).
- **Line:** 4 A slow-blow fuse in the primary; **C75 and C76, 0.005 µF 1.4 kV** line bypass; TV-style quick-disconnect line cord. The 240 V wiring uses a 2 A fuse.
- **Rectifiers:** silicon 57-27 (750 mA, 500 PIV): D5–D8 high voltage, D3/D4 low voltage, D2 bias; others for VOX, ALC and DC blocking.

**Metering figures (pp. 137–138):** GRID reads across **R33 4.7 kΩ** (RFC102 0.5 mH, C104 .005); PLATE across the cathode network with **R6 750 Ω**; ALC is a bridge across V3's cathode and screen (R117 33 kΩ, R119 68 kΩ, R116 2.2 kΩ, **R120 10 kΩ ALC ADJUST**); HV is **R43 500 kΩ in series with the meter, R42 10 kΩ shunt**, fed from the doubler centre tap, and "indicates 1000 volts full scale"; REL PWR is **D9** rectifying a sample taken through **R34 10 kΩ / R35 1 kΩ**, with **R36 600 Ω** (REL PWR ADJ) and C80 .005.

## 2.5 Voltage chart readings (manual p. 145)

Conditions (p. 146): FUNCTION **STBY**, BAND 3.5, MODE CW, DRIVER full CCW, FINAL LOAD 50 Ω, FINAL 80, LEVEL full CW, METER REL PWR, LMO 0, key open. VTVM readings; tolerance ±20%. *These were read from the scanned fold-out by eye; confirm them on the page before relying on them.*

| Point | Reading |
|---|---|
| HV doubler output (strip H) | **about 831 V**; **about 450 V** at the mid-point |
| HV winding (H) / other AC | **275 VAC**; about 116 VAC at strip J (line); 6.2–6.3 VAC filaments |
| Low-voltage B+ | about **250–258 V** on strip AC and the V4/V9/V12 plate and screen circuits |
| Regulated (V7 OA2) | **150 V** at both marked pins |
| Bias rails | **−170 V** (strip AD lug 4); **−180 V** (strip L); **−181 V** at the V10/V11 grids (finals cut off in STBY) |
| V9 (6CL6 driver) | about **−17 V** blocking bias on its grid circuit; plate circuit about 214–256 V |
| V10/V11 screens and plates | **0 V in STBY** (screen voltage is removed) |
| V4/V5 | plates about 230–253 V; V4 and V5 cathode about 1.5 V |
| Terminal board #1 / #2 | −180, −17, 0, 254–255, 26 V at the marked lugs (see the chart for lug numbers) |

The text of the initial test (p. 90) quotes **−170 V** at V10/V11 pin 5 and **800 V** on the HV meter position; the chart shows −181 V and about 831 V, which is the same within tolerance.

# 3. What fails, ranked

Rankings combine the manual's circuit knowledge, the service bulletins and the field reports in §1. The blog restoration and the 2010 Heath-list thread agree on the order: **electrolytics first, carbon-composition resistors second, grounds and contacts third, then the 6146s.**

## 3.1 Capacitors

**Electrolytic inventory from the manual's parts lists** (the manual prints no voltage ratings; ratings below come from the circuit voltages and from restorers' choices, so check your own unit):

| Ref (part no.) | Value | Where | Replace with |
|---|---|---|---|
| 25-34 ×2 (**C78, C79**) | **125 µF** | HV doubler. The chart shows about **831 V** across the pair in standby, so each sees about **415–450 V** | **500 V**, 105 °C parts are the comfortable choice; 450 V parts have almost no margin at high line. Keep **R44/R45 100 kΩ 2 W** across them (§3.2). The 2021 blog used a 100 µF 450 V and a 47 µF 500 V |
| 25-59 (**C77A 40 µF, C77B 100 µF**) | 100-40 µF can, 350/300 V | Low-voltage B+ pi filter (about 250 V) | Discrete 47 µF + 100 µF at ≥ 350 V, or a restuffed can. Recap kits exist (see §9) |
| 25-57 (**C81**) | 100 µF | Low-voltage half-wave doubler | 100 µF 250 V (blog replaced a 200 V part with a 250 V part) |
| 25-16 ×2 (**C403, C404**) | 20 µF | Bias filter (−170 V rail, **polarity reversed**) | 20 µF ≥ 250 V; positive lead to ground |
| 25-135 | 20 µF PC-mount | Carrier generator board | 20 µF 350 V (matches the recap-kit listing) |
| 25-54 ×4 | 10 µF 15 V | Carrier generator board (small axial) | 10 µF 50 V |

**Other capacitors:**

| Part | Likelihood | Notes |
|---|---|---|
| 0.005 µF 1.4 kV and 1.6 kV discs (21-35 and its 1.4 kV sibling) | High | Line-to-chassis safety caps. The blog replaced Z5U discs at BC/BD/BE with **X1/Y2 safety caps**. Do this regardless of symptoms |
| 0.2 µF "resin" (27-34, 5–6 per kit; the price list reads ".2 µfd resin") | Medium | Film/resin; check leakage and ESR |
| Mica (many) | Low | Check only if a stage is dead |
| Neutralizing and trimmer caps (31-13 3–12 pF, 2–19 pF carrier null) | Low | Mechanical; clean and re-set |

**Capacitor testing:** check electrolytics with an ESR meter or leakage tester rather than a bare capacitance meter, and remember a cap can read normal while heating the can. Hot-running caps are an immediate stop sign (WA2CKY, Oct. 2010).

## 3.2 Resistors

The 2021 blog measured **more than half of the transmitter's roughly 100 resistors more than 10% high**, and it replaced most of them. W7EKB and WA2CKY say the same thing about the SB-301/401 pair: carbon-composition parts drift up, sometimes by hundreds of percent, and Heathkit tolerances are loose.

- **Do not shotgun-replace.** Measure each resistor in critical circuits (bias dividers, plate/screen feeds, ALC, VOX, metering multipliers) and replace the ones out of tolerance.
- **Critical values to verify in place or lifted:** **R44, R45 and R41 (100 kΩ, 2 W)**, the bleeders in the high- and low-voltage supplies (the blog's "110 kΩ 2 W carbon comp" is almost certainly one of these; 100 kΩ ±10% is fine, but a high-reading bleeder leaves the 125 µF caps charged); **R412 1 kΩ 1 W** (bias filter); bias dividers off the −170 V rail; the **6.8 kΩ 1 W driver plate/screen dropper R5** (SB-401-11 item 9); the **150 Ω driver cathode resistor** (SB-401-11); the 4.7 kΩ grid-meter resistor; the 750 Ω plate-meter resistor and 500 kΩ HV multiplier (both set the meter calibration); the **six 10 Ω final-cathode resistors**; the **4 kΩ 7 W wirewound** (the blog replaced a crumbling 7 W part with a 10 W part); and the 2 W carbon-comp parts (the blog found a 110 kΩ 2 W one still good).
- **The 680 Ω resistor from terminal strip P lug 3 to the wire joining the V10/V11 lug-3 pins** (installed on manual p. 94) was added in the SB-401 to cut distortion: the 1967 *73* review says it "reduces the already acceptable distortion products figure by 3 to 4 dB." KB2QIU calls it the finals' grid-voltage connection and the review calls it the screen supply; check the pin function on the schematic before you probe it. Replace it if it has drifted.
- **R402** was raised from 1/2 W to **1 W** in the SB-401; the same change is recommended for the SB-400's R71 (AF6C). It is the one on terminal board #2 in the X-ray view (p. 140), next to R401/R412 on the −170 V supply.
- Use 500 V carbon film or metal film in the high-voltage areas. Lift one end of replaced parts slightly off the board to ease later service.

## 3.3 Diodes

- **Silicon 57-27** rectifiers rarely fail; test them while the supply is open. The blog found the rectifier good.
- **Germanium/crystal diodes** (balanced modulator, relative power meter, ALC): leakage drifts with age. Heath bulletin SB-401-16 (Apr. 1980) was titled *Germanium Diode Change*; its text is "not yet available" in the transcription. Replace a bad balanced-modulator diode as a matched set, then redo the carrier null (§4.7).
- **D105** (VOX/relay rectifier): leakage causes **VOX delay drift** (SB-401-7). An open D105 prevents the relay closing (manual troubleshooting chart).

## 3.4 Tubes, by risk

- **6146 finals (V10, V11):** the single most likely tube replacement. A gassy tube holds RL-2 closed after you unkey (bulletin SB-401-2, §5.2) and can make neutralization impossible. A faint blue glow on the glass is ordinary; a glow *between plate and grid* is gas (K7NOM, 2011). G3OOU warns that **6146B** types are hard to neutralize and says not to use them. Treat that as one restorer's opinion; the kit shipped plain 6146s (part 411-75), so use 6146 or 6146A and test any other type for neutralization.
- **6CL6 driver (V9):** weak tube → low drive everywhere.
- **OA2 (V7):** if the glow is weak, flickers or does not strike, the LMO drifts and the heterodyne injection is unstable.
- **Compactrons and multi-section tubes (V2 6AV11, V8 6AW8, V12 6D10, V13 6J11):** hard to test on a typical tester; swap with a known good one before deeper diagnosis.
- **LMO tube (V6):** see §2.2 and §4.6.

## 3.5 Mechanical and connections

- **Chassis grounds.** K9STH: loosen and retighten *every* machine screw and nut that passes through the chassis; he credits this with fixing about 90% of intermittent faults. Heath says the same (manual p. 117: retighten all hardware; 90% of returned kits had bad connections).
- **Switch and relay contacts.** Band, mode, function and meter switches plus RL1/RL2: clean with DeOxit-type cleaner. Do not over-lubricate.
- **LMO and tuning cap.** Intermittent frequency jumps come from dirty moving contacts in the LMO tuning cap; run the dial end-to-end several times first (W7EKB). Bulletin **SB-401-13** says to clean the **phono connector on the rear of the LMO**.
  - K9STH (via Kembel, p. 124): many tube LMOs develop a **"warble" while tuning**, caused by dried lubricant on the tuning capacitor's pivot points. Cleaning helps, but it usually returns unless the **rotor shaft is bonded to the capacitor frame with a braid** (§4.6).
  - KI4IUA (p. 130): hardened grease can make the stop washers bind so the dial only turns about 2½ of the 5 turns.
  - **Heathkit-Radios, "sb-401 lmo" (CT7AWB, Apr.–May 2026):** a cheap SB-401 whose LMO gave no output, or a very noisy one when tapped. On the bench, the LMO produced signal everywhere except near the end of its range, where the output dropped to almost nothing. He found a 100 kΩ resistor reading 120 kΩ and replaced it, then re-soldered **the wire from the large variable capacitor to ground**; the LMO then worked. WB9UVJ asked about the output curve and the capacitor plate spacing. Together with K9STH's braid fix, this points to **a poor rotor-to-ground bond and drifted resistors** as the first things to check. The manual's 6BZ6 LMO schematic (p. 147) has a 330 kΩ grid leak, 47 Ω, 1 kΩ screen resistor and a 10 kΩ bias resistor feeding the shifter diode, but **no 100 kΩ**, so his unit may be a different LMO revision; measure against the schematic of the one in your hands.
- **Loading cap turns when the plate cap is turned** → SB-401-14.
- **Dial cord and drive.** The 2021 blog's unit had a missing dial string and a missing load-select string and spring. Replacement cord and the **dial pulley/spring** are the usual lost parts.
- **Paint flaking, silkscreen, cracked knobs.** Cosmetic; clean silkscreen gently (91% alcohol was used on the blog unit).
- **Power cord.** The original two-conductor "widowmaker" cord and 2-pin inlet are a safety issue. Fit an IEC inlet (WA2CKY, W7EKB) or a three-wire cord with the chassis grounded.

# 4. Restoration plan

## 4.1 Phase 0: Assess cold (unplugged, discharged)

1. Photograph everything before touching it, including the underside, the coil forms and the switch decks. Draw the **V5/V8/V9/V10/V11 lead dress** (bulletin SB-401-9 treats lead dress as an instability cause).
2. Check the **power-transformer label**: single 120 V (54-143) or dual (54-198). Check the fuse holder and confirm the fuse is **4 A slow-blow at 120 V**.
3. Inspect for heat damage around the power resistors and the 125 µF caps. Smell the transformer.
4. Check which tubes are fitted and whether any are the wrong type; verify the LMO label.
5. **If the unit is already built, put it back into the manual's "initial test" state first.** The manual's Initial Test (p. 87) was written for a kit that is not finished yet, so its readings only apply if you undo seven things (KB2QIU, Heathkit group, May 2024; the page numbers are where the manual reinstalls each):

   | # | Undo | Redone at |
   |---|---|---|
   | 1 | Remove both 6146 finals and pilot lamp TW | p. 88 step 1 (readings are quoted with and without them) |
   | 2 | Unsolder the large green transformer lead from lug 3, terminal strip J | p. 89 step 2 |
   | 3 | Remove the crystals | p. 89 step 3 (Y10); p. 96 (accessory pack, Y9/Y11) |
   | 4 | Remove all tubes | p. 89 step 4, except the 6CL6, which goes in on p. 95 step 3 |
   | 5 | Remove the fuse | p. 89 step 5 |
   | 6 | Unsolder the **680 Ω resistor from lug 3, terminal strip P** | p. 94 step 1 (column 2) |
   | 7 | Unsolder **coil TB lug 2 from feedthrough capacitor Q** | p. 94 (bottom of column 1) |

   Tag every lead you lift, and photograph first. Then **do the manual's resistance check** with the fuse and tubes out, ohmmeter common to the chassis (manual pp. 88–90; readings are VTVM values, within ±20%, and *VOM readings will differ considerably*). Selected points:

| Terminal strip / lug | Expected |
|---|---|
| J lugs 1 and 2 | Low (the as-built value is illegible in the scan); rises to **0.8 Ω** with V10/V11 out and **1 Ω** with pilot lamp TW also out (filament string) |
| J lug 3 | 0 Ω (ground) |
| J lugs 4 and 5 | infinity |
| H lugs 1, 2, 4, 5 | ≥ 10 kΩ (diode) |
| AC lugs 1 and 4 | ≥ 10 kΩ after 10 s (diode); lugs 2, 3 and 5 ground |
| AD lug 2 | ≥ 10 kΩ after 10 s; lug 4 about 3 Ω; lug 5 about 600 Ω or higher |
| AB lug 1 | ≥ 10 kΩ after 10 s; lug 4: 0 Ω in CW/TUNE, ≥ 15 kΩ in LSB/USB |

   Note: bulletin **SB-401-12** says AC lugs 2 and 4 read 0 Ω if the RL-2 ground wire (SB-401-2) has been added; that is expected, not a fault.
6. Check the line cord, chassis ground continuity, and **the isolation of the phone-patch jack from the transformer case** (the troubleshooting chart lists a shorted phone-patch jack as a relay fault).

## 4.2 Phase 1: Clean

- Vacuum, then brush; compressed air only outdoors. Clean the 6146 anode clips and parasitic chokes (they are 45-53 / 45-43 types; look for discoloured or cracked ones).
- DeOxit the band switch (five decks), mode and function switches and all tube sockets; reflow any suspect solder joint.
- Clean the tuning-capacitor wipers, **lightly** lubricate shaft bushings with thin machine oil (WA2CKY), and leave the LMO closed unless it has a problem (K9STH's LMO notes on the Heath list are the reference).
- Clean the dial glass, check the pilot-lamp sockets, and replace #47 lamps.
- *SB-10x advice from Kembel (p. 22) that applies here:* clean each tube socket pin with a dental brush and DeOxit; a loose tube can be tightened by inserting a fine needle between the phenolic and the contact; **clean the contact between each mixer and driver tube shield and its socket tab, and the driver shield clips under the chassis** (missing or poorly grounded shields are "almost guaranteed" to cause transmit instability, consistent with SB-401-9); clean relay contacts with an index card moistened with contact cleaner drawn between the contacts, holding the actuator in to reach the normally-open ones.

## 4.3 Phase 2: Power supply first

1. **Replace the electrolytics** (§3.1) *before* applying power. Observe the polarity of each can; the negative-bias filters are reversed relative to B+.
2. Replace the line-bypass discs with X1/Y2 (§3.1). Install the IEC inlet or three-wire cord.
3. Test the **filter choke**: **120–140 Ω is normal; below 100 Ω means shorted turns** (SB-401-10). If it has failed, the Heath replacement was PN 46-32 (4.5 H at 150 mA) per bulletin SB-401-2D (§5.2). Note the manual's parts list shows 46-43, so confirm the number on your own choke.
4. Check the **bleeder / equalizing resistors R44 and R45 (100 kΩ 2 W)** across the two 125 µF caps (and R41 across the low-voltage 40 µF section). With 720–831 V across 200 kΩ, R44/R45 carry only a few milliamps, so the bank drains slowly even when they are good; **discharge manually every time** and verify with a meter.
5. **First power-up on a variac with a lamp in series** (series bulb limiter) and a 4 A slow-blow in the holder: bring up to 60–70 V, watch for heat, smell and arcing, then to full line. The manual's first power test (p. 90): FUNCTION to STBY, expect **−170 VDC** between pin 5 of V10/V11 and chassis; then METER to HV expects **about 800 V** and PLATE expects 0 mA.
6. Confirm V7 (OA2) strikes and glows steadily, and the 6.3 V filament string reads right at the tube sockets.

## 4.4 Phase 3: Resistor survey

Measure in place, then lift one end of any value that reads high. Work from the highest-voltage circuits down: HV doubler resistors and meter multipliers, the 6146 screen and grid circuits, the V9 plate/screen string, bias dividers, then the audio and VOX circuits. See §3.2 for the critical values.

## 4.5 Phase 4: Signal-path caps, diodes and bypass

- Replace the electrolytic bypasses on the carrier generator board (the four 10 µF/15 V and the 20 µF 25-135). Some are hard to reach under the board at the back of the terminal strip (2021 blog); work gently; the foil on these single-sided boards lifts easily if overheated.
- **Add a 0.01 µF** disc in parallel with the **6146 screen bypass** and cathode bypasses if the rig is unstable on 80 m (I0JX, Jul. 2011: the screen bypass is the most critical). This is a field fix, not a factory change; try it only after the stock components are verified.
- Check **RFC4 and RFC6 are not interchanged** and that **C26 is isolated from its shaft** (SB-401-9).

## 4.6 Phase 5: LMO and dial

- Tube: use the type marked on the LMO label (see §2.2). The LMO is calibrated with its supplied tube; expect a small calibration shift when it is replaced.
- Check the **phono connector on the LMO** (SB-401-13) and the LMO MODE / FREQ CONTROL switch path.
- Check dial cord, springs and the zero-set pulley before the dial calibration (manual pp. 96–97).
- **Bench-test the LMO before anything else.** A tube LMO has three leads: **B+, filament and bias** (the bias lead goes to a 33 kΩ resistor), plus the RCA output. Power it from a bench supply and listen to it on a receiver near 5.25 MHz with the BFO on, or scope or count the output. Tap it. Rock-steady output is the goal; a warble, dropouts when tapped, or output that collapses near one end of the range all point to the capacitor ground bond, its lubricant, or drifted resistors (§3.5).
- **Removing the LMO without pulling the front panel** (Kembel, p. 122): unplug the line cord; turn the dial fully counterclockwise to the stop; remove the knob; loosen the shaft bushing nut and pull the shaft forward off the circular dial's metal ring; loosen the dial setscrew and ease the dial forward off the spiral follower; free the follower from the pointer; unsolder the three leads (note which goes where) and unplug the RCA output; remove the four chassis nuts (two are under cable bundles; a ¼ in. socket reaches them); lift off the slide-rule/pilot-light assembly. Refit in reverse, then **redo the dial calibration** (manual pp. 96–97, plus Kembel).
- **Cleaning and the grounding braid** (K9STH, Kembel pp. 124–126): remove the side panel on the **tube side** (10 hex-head ¼ in. sheet-metal screws; the bottom two hold the mounting lugs; two or three carry red lacquer seals from the factory warranty). Do not disturb the small variable capacitor inside. Remove dried lubricant from the main capacitor's pivots (WD-40 and a toothbrush); free the shaft stops so it turns the full five-plus turns; re-lubricate the pivots. Then bond the rotor shaft to the frame: take out the gear setscrew that is exposed with the capacitor about half open, fit a short 8-32 stud, and solder about 2 in. of braid (RG-58 braid works) from the stud to the capacitor frame. **On the 110-32 (large gear)** the stud must be a headless 8-32 rod about ½ in. long so it clears the worm gear; **on the 110-40 (small gear)** a ½ in. 8-32 screw clears, and you tin the head. Turn the shaft through all five turns and confirm the braid touches nothing.
- **Stuck stop washers** (KI4IUA, pp. 130–131): clean the washers and re-grease (he used white lithium grease). Reassemble with the collar lightly tight, watch a frequency counter on the LMO output, and set the counterclockwise stop near **5.5 MHz** and the clockwise stop near **5.0 MHz** (within about 10 kHz), then tighten.

## 4.7 Phase 6: First transmit and alignment (manual pp. 90–97)

Equipment: **50 Ω non-reactive dummy load** (Heath HN-31 Cantenna type), an **11 MΩ VTVM with RF probe** (Heath IM-11 / 309C), a CW key, a high-Z microphone, and either an **SB-301/SB-303 receiver** (transceive method) or the **SBA-401-1 crystal pack**.

**Alignment with an SB-301 or SB-303 as transceiver:**

1. **V9 out.** Connect the SB-301 per Figure 2-1A. Set the 8.6 MHz trap cap on terminal board #1 as in inset 1 of Figure 2-2.
2. **Carrier generator** (FUNCTION TRCV, receiver STBY, FREQ CONTROL LOCKED, MODE CW, LEVEL full clockwise): probe pin E on the carrier board; with receiver MODE USB, adjust the **balanced modulator transformer** slug for maximum (about 1–1.5 V; take the peak nearest the *top* of the slug). Then with LUG 2 of the MIC connector shorted to chassis (or PTT pressed), alternately adjust the **CARRIER NULL control and capacitor** for minimum.
3. **ALC meter:** METER to ALC; adjust **ALC ADJUST** for zero.
4. **Heterodyne oscillator coils:** probe pin 2 of the V9 socket (wrap a cut-off resistor lead around the probe tip). On each band, **adjust the driver grid coil, then the HET OSC coil**, for maximum; always keep both BAND switches on the same band. Readings of about 1.5 V or higher are normal.
5. **V9 in.** Probe the bare wire between pin 5 of V10 and V11: peak the **driver PLATE** coil, then the **GRID** coil, on each band (35 V or higher is normal). At 29.0 adjust the DRIVER control, then the 29.0 grid coil.
6. **8.6 MHz trap:** remove the HET OSC cable, set 7.0 band, LMO dial at 3, FUNCTION SPOT, MODE CW, LEVEL and DRIVER fully clockwise, UNLOCKED; adjust the trap cap for **minimum** indication; reconnect and repeak the driver coils.
7. **Carrier null (final):** LEVEL fully counterclockwise, MODE USB. Alternate the CARRIER NULL control and capacitor to a minimum; switch to LSB and use the capacitor to match the USB reading; repeat until both are equal. Redo the balanced-modulator slug if you cannot get near zero.
8. **Neutralization (manual p. 94):** BAND 28.5, VTVM probe in the **ANTENNA** connector, FUNCTION TRCV, LEVEL fully clockwise, key. Peak DRIVER, then FINAL with LOAD at the 50 Ω mark. Using an **insulated screwdriver**, adjust the **neutralizing capacitor for minimum**, re-peak FINAL, re-adjust neutralizing, and repeat. *Do not key for more than 30 s.*
9. **Discharge and wire up the final:** unplug, discharge via feedthrough capacitor Q, connect Q's lead to coil TB lug 2, install the 680 Ω resistor from terminal strip P lug 3 to the centre of the bare wire between V10/V11 pin 3, then close the final compartment.
10. **Final bias:** dummy load on, **V9 out**, METER PLATE, BAND 3.5, FUNCTION TRCV, MODE USB; allow a few minutes to warm up; key and set **BIAS ADJUST for 50 mA** on the PLATE scale.
11. **V9 in (with its shield).** FUNCTION TRCV, MODE CW, LMO dial at 0, DRIVER at the first mark from CCW. Key and repeak driver plate and grid coils for maximum **relative power** on each band.
12. **LMO calibration:** with the SB-301 on USB 3.5 and the SB-401 on SPOT, LMO dial at 3.5, talk into the mic and tune the LMO until you sound natural in the receiver; set the dial zero; switch both to LSB; use the **LMO FREQ SHIFT coil** to match. Repeat until the USB/LSB shift is gone.
13. **Final adjustments:** 3.5 band, METER to GRID, set LEVEL for **0.2 mA**; adjust the **receiver HET OSC coil** for peak, on each band except the receiver's 15.0 band.

**Alignment with the SBA-401-1 crystal pack:** the same sequence, with the eight heterodyne crystals plus Y9 (USB) and Y11 (LSB) installed in the transmitter. See manual p. 97 onward.

**Transceive re-alignment bulletin (SB-401-3, §5.2):** the receiver BFO coil should be adjusted while measuring at C127 on the carrier-generator board, to avoid disturbing the transmitter.

## 4.8 Phase 7: Tune-up and checks (manual pp. 114–116, SB-401-8)

CW tune-up with a dummy load (also the bulletin's "alternate tune-up"):

1. FUNCTION TRCV (or TRAN); MODE CW; METER REL PWR; LEVEL fully CCW; FINAL LOAD at the 50 Ω mark; DRIVER at the first mark from CCW; MAIN TUNING at the operating frequency.
2. Key briefly and advance LEVEL until GRID reads about **0.5 mA (midscale)** (reduce LEVEL if above half scale).
3. Peak **FINAL**, **DRIVER**, and **LOAD** for maximum relative power.
4. METER to PLATE: expect **about 200–240 mA** (manual: ~220 mA; Figure 5-2 shows 240 mA single-tone peak). Never hold the key down more than 30 s.
5. Adjust the Relative Power control for half-scale on 80 m when fully loaded.

SSB: tune as for CW, set MODE to LSB below 14 MHz and USB at 14 MHz and above, set METER to ALC, adjust **ALC ADJUST** for zero with no modulation and PTT pressed, then adjust **LEVEL** so the meter peaks at midscale (top of the ALC area). **SSB plate current should normally run 80–100 mA**, with relative power about 1/4 to 1/3 of the CW reading. **No grid current is expected in SSB.**

**Anti-VOX:** with a strong receiver signal, advance ANTI-VOX until receiver audio no longer trips the VOX, then set VOX GAIN and DELAY to taste.

## 4.9 Phase 8: Optional modifications (restore stock first)

All mods are optional and reversible, and the stock circuit comes first.

- **Ground the 6146 screens in receive** by jumpering the unused NC contact of the relay section, pin 7 of RL1 (lug 7), to ground. This is **Heath bulletin SB-401-2**, so it is a *factory* fix rather than a mod. AF6C used it to cure antenna-relay hang-up after the radio got hot.
- A **1N4007** diode in the 6146 screen connection is the Collins KWM-2 fix (K9STH, Aug. 2010). He expects it to work on the SB-40X series but cites no Heath bulletin. Try it only if the RL1 pin 7 fix is not enough.
- **Instability fixes (factory):** replace buss wire between lugs 1 of coils CM and CN with a **100 Ω 1/2 W** resistor (SB-401-9) and the **100 Ω 1/2 W resistor between the two 10 m coils** on the driver grid side (SB-401-3D).
- **Full break-in** and a cathode-follower T/R switch (G3OOU) are possible but outside the factory design.

# 5. Symptom quick-reference

## 5.1 Troubleshooting (manual pp. 118–121 plus bulletins)

| Symptom | Likely causes |
|---|---|
| Filaments do not light | Green transformer lead not connected to J lug 3; open filament string; fuse missing or blown; pinched wires under shields |
| No DC at HET OSC test socket (crystal-kit units) | V8 voltages and wiring; band switch; crystals in wrong sockets; ground at crystal sockets; V7 (OA2) bad; function switch |
| No final plate current | V10/V11 voltages and wiring; cathode metering circuit; meter; BIAS ADJUST control |
| Full-scale plate current, no signal | Grid voltage at V10/V11 should be −50 V; bias supply; BIAS ADJUST control; cathode metering |
| Relay doesn't close (CW, key down, FUNCTION TRCV/TRAN) | RL1 or RL2; no B+; V12/V13/V1 wiring and voltages; tone oscillator dead; ANTI-VOX too high; **D105 open** |
| No carrier generator output (CW/TUNE) | Crystals; mode switch wiring; V2/V3; RL1; bias still on V3; shorted coax to mode switch |
| Carrier won't null | Crystal diodes; balanced modulator transformer; CARRIER NULL pot open/short; LEVEL not CCW |
| No RF at V9 pin 2 | Shorted coax from V5; band switch; coils; bandpass filter; heterodyne oscillator; V4/V5; RL1; bias at V9 pin 1; V5 pin 2 foil |
| No RF at V10/V11 pin 5 | RFC4 open; RFC5/RFC6 open; V9/V10/V11; band switch; coils; RL1; **8.645 MHz trap (C303) misadjusted** |
| Neutralizing not possible | Insufficient drive; driver-coil bypass wiring; wiring in final compartment |
| No RF output | V10/V11; **R17 open**; feedthrough C67 not connected to RFC9 lug 2; loading circuits; band switch; antenna relay RL2 |
| Weak spotting signal | Antenna-relay-to-RCVR-ANT wire too far from the bare wire between V10/V11 pin 5 lugs (SB-401-4) |
| Low drive on 7 and 14 MHz | 8 MHz trap set improperly |
| Instability | Open shield grounds; poor lead dress; loose hardware; improper neutralization; see SB-401-9 |
| Hum | Filter choke shorted; filter cap leakage; heater-cathode leakage (V1, V13); loose grounds; shield-lead grounds. See SB-401-10 |
| Relay stays energized after unkeying | Gassy 6146s; fix = ground relay pin 7 (SB-401-2); replace tubes |
| VOX delay drifts | Leakage in D105 or change in C141 (SB-401-7) |
| LMO drift / intermittent shift | Dirty phono connector at LMO (SB-401-13); LMO cap contacts; V7 |
| LMO no output, noisy when tapped, or output collapses near one end | Rotor-to-frame ground bond; dried capacitor pivot lubricant; drifted LMO resistors (a 100 kΩ read 120 kΩ in the 2026 groups.io case); the three LMO leads. §3.5, §4.6 |
| "Warble" while tuning | Dried LMO pivot lubricant; add the grounding braid (K9STH) |
| Dial turns only part of five turns | Stuck stop washers (KI4IUA) |
| Drive uneven from one end of a 500 kHz segment to the other | Bandpass coupler (52-65, 8.395–8.895 MHz). The manual calls it factory-tuned; Kembel (p. 40) measures the equivalent filter on SB-10x rigs by peaking DRIVER at 50 kHz steps with the 6146 screens removed, and notes sweep alignment is possible. Adapt with care |

## 5.2 Service bulletin index

All 20 entries from the Heath-list transcription. Numbers are as printed (the 2014 post prints "SB-401-14" twice). Serial-number limits are not given in any of them.

| No. | Date | Subject | Action |
|---|---|---|---|
| SB-401-1D | — | LMO change | PN 110-32 no longer available; use **100-40-LMO**. Add decoupling caps per the SB-101 procedure (no values given) |
| SB-401-2D | May 15, 1968 | Filter choke | PN 46-36 (4.5 H/120 mA) → **PN 46-32 (4.5 H/150 mA)**, only if the original has failed |
| SB-401-3D | Apr. 10, 1967 | Improve 14 MHz grid drive | Add a **100 Ω 1/2 W** between the two 10 m coils on the driver grid side |
| SB-401-1 | Feb. 16, 1973 | Carrier null control failure (SB-102, SB-401, HW-101; PN 10-147) | Fiber washer for clearance; control case grounded by a separate wire |
| SB-401-2 | Jan. 29, 1974 | **RL-2 hang-up** | Gassy 6146s; ground **lug 7 of RL-1** to ground the screens in receive |
| SB-401-3 | May 23, 1974 | Aligning SB-301/SB-401 as transceiver | Sequence for crystals, het osc coils and BFO adjustment at **C127** |
| SB-401-4 | May 23, 1974 | Spotting with SB-301/SB-401 | Re-route the red RCVR-ANT wire away from the final sockets; replace with coax if still bad |
| SB-401-5 | May 23, 1974 | CW sidetone with headphones | Cable changes (diagram not legible in the transcription) |
| SB-401-6 | May 23, 1974 | **RF voltage service guide** | Reference RF readings on 80 m CW key-down at 260 mA: **1.5 V at V9 pin 2; 36 V at V9 pin 6; 36 V at V10 pin 5**, with 125 W on an HM-102, LEVEL about 10:30, grid current 0.5 mA |
| SB-401-7 | May 23, 1974 | CW VOX troubleshooting | AC/DC reference voltages at V12/V13 pins; VOX delay drift from D105 leakage or C141 change; mount both parts on the board bottom |
| SB-401-8 | May 23, 1974 | Alternate tune-up | Presets, 30-second key-down limit, plate current 200–240 mA |
| SB-401-9 | May 23, 1974 | **Instability checklist** | RFC4/RFC6 not swapped; C26 isolated from shaft; 100 Ω resistor between CM/CN coil lugs; lead dress; replace driver/final tubes and re-neutralize; align into a non-reactive 50 Ω load |
| SB-401-10 | May 23, 1974 | Hum guide | Filter choke 120–140 Ω normal; check for leakage **C78, C403, C79, C404, C81, C402, C77A, C106, C77B** (the 1998 repost pairs these with the SB-400's C180, C183, C181, C184, C179, C147, C182A, C185, C182B; the 1997 repost scrambled the two columns); retighten grounds; check heater-cathode leakage; **solder the C79 mounting lug to its metal wafer** |
| SB-401-11 | May 23, 1974 | **Driver stage guide** | **1.5–2.5 V RF at V9 grid** all bands; bias −15 VDC key-up / −0.5 VDC key-down at V9 pin 2; cathode **150 Ω**; check C4 A–D wiring to BS3R/BS4R; check R-4, R-5 (**6.8 kΩ 1 W**), RFC-4, C-8, C-7, C-58 if plate/screen voltage is ≥ 50 V low |
| SB-401-12 | July 24, 1974 | Resistance at terminal strip AC | Lugs 2 and 4 read 0 Ω once the RL-1 ground wire is added; expected |
| SB-401-13 | July 24, 1978 | LMO drift | Clean the **phono connector on the LMO rear** |
| SB-401-14 | Aug. 7, 1978 | Loading cap turns with plate cap | Free and lubricate shafts; rubber grommet 73-3 on the loading shaft if needed |
| SB-401-15 | Jan. 21, 1980 | Driver plate resistor overheats | Text not available |
| SB-401-16 | Mar. 7, 1980 | Incompatible with HDP-1220 BW clipper | Text not available |
| "SB-401-14" (second) | Apr. 10, 1980 | Germanium diode change | Text not available |

Related: **SB-400-1/-2/-3** (driver, hum and CW VOX guides, May 23, 1974) are the SB-400 versions of SB-401-11, -10 and -7. The full set is at nostalgickitscentral.com; the Heath-list repost links `nostalgickitscentral.com/heath/Service_Bulletins/sb-sb401.pdf`.

# 6. Operation notes

## 6.1 With the SB-301 or SB-303

- **Transceive** needs the receiver's LMO, heterodyne oscillator and BFO signals via the rear RCA jacks (RCVR LMO, HET OSC, RCVR BFO), the speaker, anti-VOX and mute jacks, and the RCVR ANT coax. Set the SB-401 **FREQ CONTROL to LOCKED**; use **UNLOCKED** for split or independent operation. After the SBA-401-1 kit, LOCKED is for use with the receiver independent of band (manual p. 116).
- **CW offset:** both rigs transmit **1 kHz above** the dial on CW so the receiver beat note is 1 kHz.
- **Sideband convention:** LSB on 80 and 40 m; USB on 20 m and up.
- **Interconnect cables:** the three signal cables that bring the **VFO (LMO), BFO and heterodyne-oscillator** signals into the transmitter are **RG-62**, cut to **exactly 2 ft** each (W2JDL, *73*, July 1967: "The cable is supplied with the kit"). W7EKB says the same: **RG-62, not RG-58**. If the pair has been recabled, check length and type.
- **CW with the receiver:** leave the transmitter's **FUNCTION switch in TRCV (transceive) for CW as well as SSB.** Putting it in TRAN for CW gives a constant beat note in the receiver; Heath issued a bulletin and revised the manual for this (W2JDL, 1967).

## 6.2 Rear panel (AF6C Table 3)

PATCH (RCA, 600 Ω), KEY (¼ in.), AC INPUT (2-pin), accessory socket (9-pin: pins 8/9 supply the external antenna relay at line voltage), RCVR AUDIO, SPKR, RCVR LMO, ANTI-VOX, HET OSC, RCVR BFO, RCVR MUTE, LINEAR RELAY, ALC INPUT, SO-239 ANTENNA, RCVR ANT.

## 6.3 Using an external amplifier

LINEAR RELAY grounds on transmit; ALC INPUT takes ALC voltage from the amplifier. The ALC meter should peak at or below midscale on SSB.

# 7. Tips and tricks

- Start with **grounds and electrolytics**, not a shotgun resistor swap.
- **Lift one end of replaced resistors** so the next person can measure them in circuit.
- Keep the **final compartment closed** whenever the transmitter is keyed.
- Before tuning, **let the unit warm up for a few minutes** (the manual's own bias step).
- Take **grid current as a drive indicator, not a goal**: the K3WQ thread concluded little or no grid current on 80 m is not itself a fault with 6146s, even though the manual's wording suggests otherwise.
- **Dummy load, not a light bulb.**
- If the 80 m dip and the power maximum do not coincide, suspect **neutralization** first, then the **fixed loading capacitors** (the 100/200 pF caps added on 40/80 m) and the band-switch contact; see the 2011 boatanchors thread.
- A **recap kit** (§9) saves hunting for the carrier-generator board electrolytics.

# 8. Maintenance schedule

| Interval | Task |
|---|---|
| Each session | Dummy-load check; keydown ≤ 30 s while testing |
| Yearly | DeOxit switches and sockets; retighten chassis grounds; check fuse; check output on the dummy load |
| Every 2–3 years (suggested) | Re-peak driver coils; re-null carrier; re-neutralize |
| As needed | Replace the 6146s if relay hang-up, low output or neutralization trouble appears |
| After a recap, every 5–10 years (suggested) | Check electrolytic leakage/ESR; the 125 µF caps are the first to go |

# 9. Parts sources

- **Hayseed Hamfest** (Tom N0JMY, hayseedhamfest.com): replacement electrolytics and recap kits for the SB-301 and SB-401 (Heath-list threads, 2008 and 2010). In 2008 he was adding the SB-401 to the line and listing five electrolytics (the carrier-generator board's small ones, a PC-mount 20 µF, and the two 125 µF cans). Confirm what the current kit contains.
- **Nichicon, Panasonic and similar 105 °C electrolytics** at Mouser/Digi-Key (the 2021 blog's choices).
- **X1/Y2 line-bypass caps**, 500 V carbon-film and metal-film resistors (Ohmite, Vishay/Yageo), **10 W wirewound** parts.
- **6146 / 6146A** tubes from reputable tube sellers; match the pair. Avoid the 6146B per G3OOU unless you can test neutralization.
- **Dial cord, knobs, lamps (#47), silicone grease** from the usual Heath parts dealers.
- **Original service bulletins:** nostalgickitscentral.com.
- **P.E.C. network (84-22):** no longer available per the 2021 blog; test it carefully and keep it if it measures right.

# 10. Sources

- Heath Co., *Assembly and Operation of the Heathkit SSB Transmitter Model SB-401*, 595-947-xx, ©1966: owner's 88-page scan (`sb-401.pdf`, not redistributed), and the "Condensed Manual" 595-947-10 on archive.org, item `assemblyoperatio00unse_0` (Ron Patterson W6FM collection).
- Eckweiler AF6C, "Heathkit of the Month #43: SB-401," w6ze.org (Oct. 2012).
- Heath mailing list archive (puck.nether.net/pipermail/heath): "Heathkit Service Bulletins — SB-401 (Complete)" (Aug. 1997); "Grid meter reading on SB-102 / Heathkit Service Bulletin Website" (Dec. 2014); "SB-301/SB-401 Functional Repair Guidelines" (Oct. 2010); "SB-401 Info/Experience needed" (Apr. 2008); "SB-401" (Aug. 2010); "SB401 Problem" (Dec. 2001); "Any SB-401 Hints available?" (Jul. 1997).
- rec.radio.amateur.boatanchors, "Finals going bad in Heathkit SB-401 transmitter?" (Jul. 2011).
- Heathkit-interests blog, *Heathkit SB-401 Amateur Transmitter* (Feb. 2021).
- Waters, M. (W2JDL), "The Heathkit SB401 Transmitter," *73 Magazine*, July 1967, pp. 98–100.
- Heath mailing list, "Heathkit Service Bulletins: SB-401 (Complete 1966-89)" (J. Lutz, June 13, 1998), the post AF6C cites for the bulletins.
- Heathkit group (groups.io), "SB 401 is here and the..." (May 2024), messages 7183–7186 (W7EKB, WB4GRA, AF6C) and KB2QIU's "undo" list.
- Kembel, R. W., *Heathkit HW-101 and SB-10x Restoration and Troubleshooting*, rev. Dec. 17, 2021 (LMO notes by K9STH and KI4IUA; filter table).
- Heathkit-Radios (groups.io), "sb-401 lmo" thread, messages 22979–22994 (CT7AWB, WB9UVJ), Apr.–May 2026.
- G3OOU, *Heathkit SB Line — Where Next?*, qsl.net/g3oou.
- RigPix, SB-401 entry (dates, final tubes).
- *Heathkit-Radios* (groups.io) — see §11.

# 11. What the manual confirmed and what it didn't

**Confirmed against the Heath manual (595-947-xx):** tube complement and the LMO tube type (LMO schematic p. 147: 6BZ6); fuse and lamp type; power draw; HV and bias values at first power-up; alignment sequence; final bias at 50 mA; tune-up currents; neutralizing procedure; the 30-second key limit; the discharge procedure; the troubleshooting chart.

**Not confirmed, because the scan does not preserve it:**

- The **resistance chart** and the full **schematic** have been seen in the owner's scan but not transcribed. Read stage-by-stage bench values from the page; only the headline voltages are tabulated in §2.5.
- **Electrolytic voltage ratings.** The manual prints none; replacement ratings are derived from the measured circuit voltages.
- **Text of bulletins** SB-401-15, -16 and the second "-14".
- Where the bulletin part numbers differ from the manual (46-36 / 46-32 versus the parts list's 46-43), confirm against your own unit.

**Sources not read for Rev. 1:**

- **groups.io** (partly: the Heathkit-Radios "sb-401 lmo" thread and one page of the Heathkit group's "SB 401 is here" thread). The group's pages sit behind a bot check, so only two threads supplied by the owner were read. The "sb-401 lmo" thread is used; the other thread was a "first Heathkit" reminiscence with no technical content (one poster, WA4FJC, mentions the SB-401 as his last big kit). The rest of the group's SB-401 history has not been searched.
- **antiqueradios.com t=422212** returned HTTP 403 and has not been supplied.
- **EEVblog:** search found no SB-401 thread, and nothing relevant has been added.

**Source conflicts found in Rev. 1.1:**

- **LMO part number** (110-32 vs 100-40/110-40) and the SB-301's 110-40 tube type disagree between Kembel's table, the Heath manual, AF6C and the SB-301 plan (§2.2). The SB-401's own manual lists **100-40** and shows a **6BZ6**, which agrees with AF6C and the bulletin. Treat the LMO label as the authority.
- Kembel's HW-101/SB-10x guide is for different rigs; its procedures are adapted here only where the circuit is shared (LMO, crystal filter, bandpass coupler, SB-line practice).

**Corrections to earlier assumptions:** *None yet.* Rev. 2 should list them, as the SB-301 plan did.
