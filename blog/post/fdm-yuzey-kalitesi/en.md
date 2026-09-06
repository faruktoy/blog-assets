---
type: article
slug: "ra-in-fdm"
title: "Improving Surface Quality in FDM Prints: PLA vs ABS vs PETG"
description: "Cross-comparing five academic sources on how layer height, speed, temperature and Z wobble affect Ra."
date: "2026-04-30"
category: "printing"
tags:
  - 3D Printing
  - FDM
  - Surface Roughness
  - Ra
  - Research
cover: ""
published: true
featured: true
legacySlugs: []
lang: en
---

# Improving Surface Quality in FDM Prints: PLA vs ABS vs PETG

> How good can a 3D print look? The technical answer is measured by surface roughness — the Ra value. In this post, I draw from my own printing experience, a paper I reviewed for my Research Methods course, and four international studies to cross-compare what really determines surface quality in FDM.

## What Is Ra and Why Does It Matter?

Surface roughness (Ra) is the arithmetic average of micro-irregularities on a surface. In FDM prints, this typically ranges from 1–15 µm. Lower Ra = smoother surface.

Why does it matter? I measure real aircraft parts and 3D print display models and commemorative plaques — scaled replicas of Pitot tubes, AOA sensors, and Ice Detectors. For these kinds of parts, surface quality directly determines visual success: you can't gift a rough model. For functional parts, Ra is critical for fit and aesthetics.

There's a notable gap in the literature: most studies optimize parameters for a single material, while cross-material comparisons under identical conditions are relatively rare. In this post, I bring together multiple sources to paint a more complete picture.

## Filament Comparison: PLA, ABS, PETG

The paper I reviewed for my Research Methods course (Kovan et al.) compares all three filaments using a Taguchi L27 experimental design under identical conditions. The results:

- PLA produced 7.23% better Ra than ABS and 54.19% better than PETG.
- In tensile strength, PLA led by 46% and 34% respectively.

These findings don't stand alone. Portoacă et al. (2023, Polymers) found that for ABS and PLA, increasing infill percentage and setting extrusion temperature to 220°C improved failure load. Interestingly, while Kovan's study shows a clear Ra advantage for PLA, Portoacă's results suggest ABS can be competitive in the surface-strength balance with the right temperature and infill settings.

On the PETG side, Mishra et al. (2023, Polymers) focused exclusively on PETG, using RSM and ANFIS models to determine optimal parameters: 50 mm/s speed, 0.1 mm layer height, 230°C temperature, and 0.6 mm raster width. While PETG showed the worst Ra in Kovan's cross-material comparison, Mishra's material-specific optimization achieved far better results — proving there's no such thing as a "bad material," only parameters that haven't been tuned for it.

In my own experience, I generally prefer ABS. Yes, PLA can give better Ra numbers, but ABS offers UV resistance, heat tolerance, and impact toughness that make it far more suitable for display models — PLA warps on a sunny shelf, ABS holds up. ABS does show slightly more visible layer lines, while PETG leaves a "wet" appearance.

The biggest downside of ABS is VOC (volatile organic compound) emission. Styrene gas is released during printing, so an enclosure and proper ventilation are essential. Printing ABS in a small, unventilated room is a health risk — I always print in a ventilated environment.

Bottom line: there's no "best filament" — it depends on the goal. Display and durability? ABS. Smoothest possible surface? PLA. Chemical resistance and flexibility? PETG.

## Layer Height: The Most Decisive Parameter

There's broad consensus in the literature on this. While Kovan et al. identified layer height as the dominant factor, Pérez et al. (2018, Materials) independently confirmed this. In Pérez's ANOVA analysis of PLA, only layer height and wall thickness had a statistically significant effect on surface roughness — print speed and temperature did not.

Even more striking, a 2025 study published in the International Journal of Advanced Manufacturing Technology reported that layer height can account for up to 66% of surface roughness variance. That's an extraordinary ratio — a single parameter determining two-thirds of the outcome.

Concrete numbers from Kovan et al.:

- 0.1 mm layer → Ra ~1.44 µm (best surface)
- 0.2 mm layer → Ra ~4–6 µm (standard)
- 0.3 mm layer → Ra ~8–12 µm (rough but fast)

The physical reason is the "staircase effect": thick layers create visible step-like artifacts on sloped and curved surfaces. Pérez's study explicitly highlights this, while Kovan's SEM images provide evidence of this effect on fracture surfaces.

Parts I print at 0.1 mm on my P3Steel look almost injection-molded. But print time triples. So I use 0.2 mm for prototypes and drop to 0.1 mm only for final parts.

## Speed and Temperature: What the Sources Say

The effect of print speed is where the sources interestingly diverge — and that divergence itself is valuable information.

Kovan et al. found the best Ra at 60 mm/s, not 40 mm/s, challenging the "slower = better" assumption. Mishra et al. found 50 mm/s optimal for PETG. Pérez et al., however, found that speed had no statistically significant effect on Ra.

This apparent contradiction actually tells us something important: speed's effect depends on the material, printer mechanics, and the levels of other parameters. In Kovan's Taguchi design, speed's effect emerges in interaction with infill ratio and raster angle; in Pérez's study, it becomes insignificant when isolated. My sweet spot: 50–65 mm/s.

On temperature, there's a clearer picture:

- PLA: 200–210°C for cleanest surface (Portoacă et al. recommend 220°C for mechanical strength, but slightly lower is better for surface)
- ABS: 230–240°C, but an enclosure is essential — confirmed by Portoacă's work
- PETG: 230°C (Mishra et al.'s optimum), too hot and stringing starts

Printing a temperature tower is the most reliable way to find your filament's ideal temp.

## Z Wobble: The Silent Surface Killer

You've optimized parameters, chosen the right filament, but there are irregular lines on your print? You're likely dealing with Z wobble. The literature typically focuses on software parameters, but mechanical faults can invalidate all optimization.

Z wobble is a periodic surface artifact caused by misalignment between the Z-axis leadscrew and stepper motor. Symptoms:

- Regularly spaced undulations on the surface
- Lines that span the print height, independent of layer height
- The same pattern visible on all sides when you rotate the part

This issue is distinct from the staircase effect discussed in the academic literature: staircase is linear with layer height, Z wobble is about mechanical alignment. One reason Pérez's study found speed and temperature insignificant for Ra might be that their test printer was well-calibrated mechanically — these variables only become meaningful once mechanical issues are resolved.

I struggled with this extensively when building my P3Steel. My solution:

1. Replaced the rigid coupler with a flexible jaw coupler — rigid connections transfer misalignment directly to the surface.
2. Aligned the Z motor coaxially with the leadscrew (you can check with a ruler).
3. Added an anti-backlash nut — reduced both wobble and Z banding.

After these three steps, the visible improvement in Ra was dramatic.

## Quality vs Strength: A Cross-Study Comparison

The key finding from Kovan et al.: optimal parameters for best surface quality and best tensile strength are different.

- Lowest Ra: PLA – 60% infill – 0.1 mm layer – 60 mm/s – 30° raster angle → Ra 1.44 µm
- Highest strength: PLA – 60% infill – 0.3 mm layer – 40 mm/s – 45° raster angle → 32.18 MPa

Layer height and speed go in opposite directions. Thin layers give smooth surfaces but reduce inter-layer adhesion. A study presented at the 2023 SFF Symposium demonstrated that doubling layer height from 0.1 to 0.2 mm resulted in a 6–11% drop in tensile strength.

Portoacă et al. approach this balance from a different angle: by increasing infill and optimizing temperature, both surface and strength can be improved simultaneously. Mishra et al. used multi-objective optimization (NSGA-II) for PETG to create a Pareto front — mathematically proving that multiple "correct answers" exist in the quality-strength tradeoff.

This is why "what will this part do?" should be asked before every print. For my aircraft display models, I print the outer shell at 0.1 mm while keeping infill at 60% — a compromise between surface quality and strength.

## Conclusion: Find Your Own Parameters

Comparing five different academic studies, the picture is clear: layer height is the dominant factor everywhere, but other parameters' effects vary by material and printer mechanics. There is no single recipe.

My recommendations:

1. Start with a temperature tower — see your filament's real behavior.
2. Choose layer height based on the part's purpose, not autopilot.
3. Check your Z axis — mechanical issues can't be fixed with software.
4. Change one parameter at a time; otherwise you won't know what affects what.
5. Do material-specific optimization — Kovan's cross-comparison is a roadmap, but as Mishra's PETG study shows, material-specific tuning yields far better results.

## References

[1]: https://dergipark.org.tr/en/download/article-file/3434449 "Kovan et al., Modeling and Optimization of Surface Roughness and Tensile Strength of ABS, PLA, and PETG Specimens Produced by FDM Method"
[2]: https://doi.org/10.3390/ma11081382 "Pérez, M. et al. (2018), Surface Quality Enhancement of FDM Printed Samples Based on the Selection of Critical Printing Parameters, Materials, 11(8), 1382"
[3]: https://doi.org/10.3390/polym15163419 "Portoacă, A.I. et al. (2023), Optimization of 3D Printing Parameters for Enhanced Surface Quality and Wear Resistance, Polymers, 15(16), 3419"
[4]: https://doi.org/10.3390/polym15030546 "Mishra, P. et al. (2023), Parametric Modeling and Optimization of Dimensional Error and Surface Roughness of FDM Printed PETG Parts, Polymers, 15(3), 546"
[5]: https://doi.org/10.1007/s00170-025-14820-2 "Evaluating the Influence of Machine Type on Surface Roughness in Material Extrusion (2025), Int J Adv Manuf Technol"
