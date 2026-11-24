# Heathkit SB-401 Restoration Plan

A restoration plan for the Heathkit SB-401 HF SSB/CW transmitter (1966–1976, two 6146 finals, 100 W output on 80–15 m). It covers which parts fail with age, a phased restoration and alignment procedure checked against the Heath manual (595-947-10), the full list of Heath service bulletins, a symptom table, a stage-by-stage "no output in TUNE mode" chapter, optional field fixes and maintenance. It is written to pair with the [SB-301 receiver plan](https://github.com/usa4148/heathkit-sb301-restoration).

**Status:** Rev. 1.4, built from the Heath manual (full scan, including the power-supply figures, voltage chart and schematic), the SB-401 service bulletins and field sources, with LMO repair notes from Kembel's HW-101/SB-10x guide and a Heathkit-Radios LMO thread. The resistance chart is not transcribed, and most of groups.io has not been searched. See §11 of the plan.

## Files

- [`sb401-restoration-plan.md`](sb401-restoration-plan.md) — source (pandoc markdown)
- [`sb401-restoration-plan.pdf`](sb401-restoration-plan.pdf) — rendered PDF

## Build

```sh
pandoc sb401-restoration-plan.md -o sb401-restoration-plan.pdf \
  --pdf-engine=xelatex -V mainfont="DejaVu Serif"
```

## Safety

**The plate supply reads about 800 V DC, which is lethal.** Unplug the transmitter and discharge the high-voltage capacitors through the lower lead of feedthrough capacitor Q with an insulated screwdriver, as the manual directs, then confirm with a meter before touching anything. Use a 50 Ω dummy load (never a light bulb) and do not key the transmitter for more than 30 seconds at a time.

## Sources

- Heath SB-401 Assembly and Operation Manual 595-947-10 (archive.org, `assemblyoperatio00unse_0`)
- Heath SB-401 service bulletins (Heath mailing list transcriptions, 1997/1998/2014; nostalgickitscentral.com)
- W2JDL, "The Heathkit SB401 Transmitter," 73 Magazine, July 1967
- AF6C, *Heathkit of the Month #43: SB-401* (w6ze.org)
- Heath mailing list; Heathkit-Radios (groups.io); rec.radio.amateur.boatanchors; the heathkit-interests restoration blog; G3OOU
- Kembel, *Heathkit HW-101 and SB-10x Restoration and Troubleshooting* (LMO repair, filters)

See also: [heathkit-sb301-restoration](https://github.com/usa4148/heathkit-sb301-restoration) · [heathkit-sb200-restoration](https://github.com/usa4148/heathkit-sb200-restoration) · [heathkit-sb102-restoration](https://github.com/usa4148/heathkit-sb102-restoration) · [heathkit-restoration](https://github.com/usa4148/heathkit-restoration) (index)
