# YASA Data Quality — Methodology Summary

This document summarises the data quality challenges identified in the JAMB IBASS dataset and the correction approaches applied. The full methodology is documented in a peer-reviewed research paper currently under review.

---

## Source dataset characteristics

The JAMB Internet-Based Admissions and Services System (IBASS) is the authoritative record of all JAMB-eligible tertiary institutions in Nigeria. As of January 2025, it contained 1,558 unique institutions and 28,267 accredited programmes. The source data has no coordinate fields and is navigable only institution by institution through the IBASS web portal.

---

## Two systematic data quality problems identified

### 1. Affiliation suffix contamination — 14.2% of institutions

IBASS institution names commonly embed affiliation references following the pattern:

```
[Institution Name], [City] (AFFL TO [Parent University])
```

Example: `FEDERAL COLLEGE OF AGRICULTURE, MOOR PLANTATION, IBADAN (AFFL TO FUNAAB)`

When this name is submitted to geocoding services without preprocessing, the affiliation reference (`FUNAAB` — Federal University of Agriculture Abeokuta) dominates the location signal. The geocoder returns the parent university's location in Abeokuta, not the college's actual location in Ibadan.

**Scale:** 221 of 1,558 institution names (14.2%) contained affiliation references requiring removal before geocoding.

**Implication for researchers:** Any geocoding of IBASS institution names that does not address this preprocessing step will produce systematically wrong coordinates for approximately one in seven Nigerian tertiary institutions.

---

### 2. State field misclassification — 7.7% of institutions

120 institutions (7.7% of the total dataset) are assigned to the wrong Nigerian state in the IBASS database. These are not random transcription errors — they concentrate in institutions whose formal names contain an explicit geographic reference that was not used to set the state field.

Example: `MEKARIA INSTITUTE OF TECHNOLOGY AND ADMINISTRATION, OBOSI, ANAMBRA STATE` appears in IBASS with state field set to Sokoto.

**Correction approach:** State names were extracted from institution name strings using a lookup against all 36 Nigerian state names and the FCT. When a name-derived state differed from the IBASS state field, the name-derived state was applied. Geopolitical zone classifications were re-derived deterministically from the corrected state.

**Implication for researchers:** Any study using IBASS state field data as a reliable geographic variable without validation may be working with wrong state classifications for approximately one in thirteen institutions. This affects research on regional educational distribution, equity analysis by geopolitical zone, and any geographic aggregation of institutional data.

---

## Geocoding approach

A priority-ordered dual-provider approach was used:

1. **Primary:** Google Maps Geocoding API — applied after affiliation suffix removal and state correction
2. **Fallback:** Nominatim (OpenStreetMap) — invoked when the primary provider returned no result within the Nigeria bounding box (4.0°N–14.0°N, 2.5°E–15.0°E)

All results were validated against the Nigeria bounding box. Institutions receiving identical coordinates — indicating city centroid assignment — were identified through coordinate clustering and flagged for crowdsourced correction via [YASA Verify](https://yasa.com.ng/verify).

---

## Dataset statistics

| Metric | Value | Notes |
|---|---|---|
| Total institutions geocoded | 1,558 | 100% of IBASS dataset |
| Total accredited programmes | 28,267 | Across all institution types |
| Affiliation suffixes stripped | 221 (14.2%) | Pre-geocoding normalisation |
| State field corrections applied | 120 (7.7%) | Systematic name-derived correction |
| Fixed subject combinations | 60.7% | Exact required subjects specified |
| Flexible subject combinations | 29.3% | Required subjects with substitutions permitted |
| Inferred subject combinations | 10.0% | Heuristic from programme name — flagged in platform |
| Wikipedia enrichment coverage | 58% (899/1,558) | CC BY-SA 4.0 attributed |
| Health facility proximity | 100% | GRID3 Nigeria 2024 dataset |
| Coordinate jitter-flagged | ~35% | Centroid-only locations, queued for verification |

---

## Subject combination framework

JAMB requires candidates to select four subjects. Each accredited programme specifies a subject combination requirement. Programme records in IBASS were classified into three types:

- **Fixed (60.7%):** The programme specifies exact required subjects with no substitution
- **Flexible (29.3%):** The programme specifies required subjects with defined permissible substitutions
- **Inferred (10.0%):** No subject data was present in the source. Likely combinations were assigned using a heuristic engine derived from JAMB's published subject guidelines across twelve discipline categories. These are clearly flagged in the YASA platform interface.

---

## Health facility proximity

Euclidean distance from each geocoded institution to the nearest GRID3 Nigeria Health Facilities dataset record was computed using geodetic distance formulae. Driving time estimates were derived using a 25 km/h average speed assumption. This layer is a novel feature of YASA with no equivalent in any existing Nigerian educational database.

Key findings:
- South West and South South institutions show the shortest mean distances to health facilities
- North East and North West institutions show substantially longer distances, with some exceeding 50 km
- Federal institutions (concentrated in state capitals) show shorter proximity than private institutions on average

---

## Crowdsourced verification (ongoing)

Coordinate positions for jitter-flagged institutions are improved through [YASA Verify](https://yasa.com.ng/verify). Three independent matching submissions from registered contributors trigger a coordinate update. Verified coordinates are reviewed and integrated into the dataset through the monthly data pipeline.

---

## Annual update cycle

The dataset is refreshed each January before the JAMB registration season opens (typically February). Accreditation status, programme listings, and subject combinations reflect the January update. Crowdsourced corrections and approved user submissions are integrated on a rolling monthly basis.

---

## Citing this methodology

If you use YASA data or reference this methodology, please cite:

>Oluwaseun Ipede, Olalekan Alausa and Babalola Adewara. YASA: A Geospatial Intelligence Framework for Educational Institution Discovery and Access Equity in Sub-Saharan Africa (Evidence from Nigeria). ScienceOpen Preprints. 2026. DOI: 10.14293/PR2199.003816.v2
