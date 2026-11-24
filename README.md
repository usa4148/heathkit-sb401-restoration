# Heathkit SB-401 Restoration Plan

A restoration plan for the Heathkit SB-401 HF SSB/CW transmitter (1966–1976, two 6146 finals, 100 W output on 80–15 m). It covers which parts fail with age, a phased restoration and alignment procedure checked against the Heath manual (595-947-10), the full list of Heath service bulletins, a symptom table, optional field fixes and maintenance. It is written to pair with the [SB-301 receiver plan](https://github.com/usa4148/heathkit-sb301-restoration).

**Status:** Rev. 1, built from the Heath manual, the SB-401 service bulletins and field sources. The manual's voltage/resistance fold-outs and schematic were not readable in the scan used, and groups.io was not reachable. See §11 of the plan.

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
- Heath SB-401 service bulletins (Heath mailing list transcriptions; nostalgickitscentral.com)
- AF6C, *Heathkit of the Month #43: SB-401* (w6ze.org)
- Heath mailing list; rec.radio.amateur.boatanchors; the heathkit-interests restoration blog; G3OOU

See also: [heathkit-sb301-restoration](https://github.com/usa4148/heathkit-sb301-restoration) · [heathkit-sb200-restoration](https://github.com/usa4148/heathkit-sb200-restoration) · [heathkit-sb102-restoration](https://github.com/usa4148/heathkit-sb102-restoration) · [heathkit-restoration](https://github.com/usa4148/heathkit-restoration) (index)
