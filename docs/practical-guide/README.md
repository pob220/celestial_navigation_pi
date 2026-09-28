# Celestial Navigation Practical Guide

[Open or download Practical_Guide.pdf](Practical_Guide.pdf)

Combined review edition prepared on 28 September 2026 from Robert Bossert's
two 27 September 2026 attachments to
[issue #319](https://github.com/rgleason/celestial_navigation_pi/issues/319).
This is documentation for review, not a plugin release or a change to the
documentation installed by the plugin.

## Contents

- Part I: altitude sights, fixes, running fixes, sight analysis, planning,
  horizon events and horizontal/vertical coastal sextant navigation (31 pages).
- Part II: lunar-distance observing, entry, results, sensitivity, planning,
  practice and Direct Triangle reference working (35 pages).

The combined PDF has 66 pages and 28 navigation bookmarks. Original printed
page numbers are retained separately within each part. The Lunar part begins
on combined PDF page 32.

## Changes to the source documents

The only textual correction is on altitude page 7: the stated new-lunar-sight
default was changed from `10800 sec` to `86,400 sec` to match the actual
current default and the explanation on lunar page 12.

Altitude page 20 is deliberately unchanged pending Bob's confirmation of the
Hawaii example's latitude and year. It currently states 18 degrees 15.6 minutes N
and 2026, whereas the earlier worked example uses 18 degrees 51.6 minutes N
and 2025. This remaining inconsistency should be resolved before incorporation
into the plugin.

The merge adds navigation bookmarks and document metadata. Existing screenshots
were not resampled or lossily recompressed.

## Verification

- PDF structure checked successfully with qpdf.
- All 65 pages other than corrected altitude page 7 render identically to their
  source pages at the comparison resolution.
- All source screenshot image digests, dimensions and placements are unchanged.
- On corrected page 7, pixel changes are confined to the corrected text line;
  surrounding text, screenshot and footer are unchanged.
- Corrected page 7 and representative pages/part transitions visually checked.
- Size: 5,595,204 bytes (approximately 5.34 MiB).
- SHA-256: `e12fdffb5c4f059da44523f18626fd0a423132db95c6e1ce1a605ca15cf97423`.

## Source PDFs

- [Altitude and coastal sight training, 27 September 2026](https://github.com/user-attachments/files/32711164/Celestial.Navigation.Plugin.Altitude.and.coastal.sight.Training.27.sept.2026.PDF.pdf)
  - SHA-256: `a5950b22c6cdfcb7bba983768a96c5d130f59b85d19508d36a8ae924541ea781`.
- [Lunar-distance training, 27 September 2026](https://github.com/user-attachments/files/32711172/Lunar.Distance.Use.Case.1.Sun-Moon.Sodus.Bay.version.27.Sept.2026.v2.8x.release.PDF.pdf)
  - SHA-256: `7ec6dbe5cea1c3f6a8cec72b3b122f944577065c907851b6f88848a1cea793af`.
