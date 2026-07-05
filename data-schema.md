# YASA Global Data Schema — Core Specification

This document outlines the standard GeoJSON Feature properties architecture for the YASA tertiary infrastructure directory.

## 🗺️ Spatial Schema Representation
All spatial data within the production system maps coordinates using the **WGS 84 (EPSG:4326)** coordinate reference system.

| GeoJSON Path | Data Type | Constraint / Formatting | Description |
| :--- | :--- | :--- | :--- |
| `geometry.type` | String | Must equal `Point` | Spatial geometric representation. |
| `geometry.coordinates[0]` | Float | Range: `2.69` to `14.67` | **Longitude** (Decimal Degrees). |
| `geometry.coordinates[1]` | Float | Range: `4.27` to `13.89` | **Latitude** (Decimal Degrees). |

## 🏫 Institutional Attributes (`properties`)

| Attribute Key | Type | Example Value | Description |
| :--- | :--- | :--- | :--- |
| `id` | String | `uni_fed_001` | Unique internal tracking alphanumeric identifier. |
| `name` | String | `University of Lagos` | Full legal name of the tertiary institution. |
| `slug` | String | `unilag` | URL-safe string token for web routing. |
| `coordinate_verified` | Boolean| `true` | Status indicator for manual spatial auditing. |
| `verification_method` | String | `satellite_imagery` | Internal validation trace (`citizen_science`, `on_site_gps`). |
| `ownership` | String | `Federal` | Governance tier (`Federal`, `State`, `Private`). |
| `nuc_status` | String | `Fully Accredited` | Regulatory status via the National Universities Commission. |

## 💰 Fees Sub-Object Structure (`properties.fees`)
Tracked metrics monitoring institutional affordability barriers.

* **`tuition_per_session_ngn`** (Integer): Raw tuition obligation. Set to `0` for Federal institutions where tuition is completely subsidized by the FGN.
* **`total_estimated_per_session_ngn`** (Integer): Summation of accommodation, base levies, and administrative processing overheads.

## 📈 Admission Signals (`properties.admission_signal`)
B2B indicators tracking institutional competitiveness quotas.

* **`acceptance_rate_pct`** (Float): Calculated baseline filtering competitiveness.
* **`signal_tier`** (String): Competitiveness classification category (`Very Competitive`, `Competitive`, `Moderate`).

## Data quality notes

**State field correction:** 7.7% of institutions (120 records) were assigned to incorrect states in the JAMB IBASS source data. YASA corrects these using state references extracted from institution name strings. The corrected state is what appears in the `state` field. The original IBASS state is not retained in the public dataset.

**Coordinate accuracy:** All coordinates are geocoded, not GPS-surveyed. Institutions in rural areas or with limited online presence carry greater positional uncertainty. `coordinate_jittered: true` indicates the institution was assigned a city centroid coordinate and has been queued for correction through [YASA Verify](https://yasa.com.ng/verify).

**Accreditation currency:** `nuc_status` reflects accreditation at the time of data acquisition (January 2025). Accreditation status changes throughout the academic year. Always verify directly with JAMB or the relevant regulatory body before making admission decisions.

**Fee data:** Fee figures are compiled from multiple sources and carry varying confidence levels. The `confidence` field indicates reliability. `max_confirmed` is the highest figure confirmed from a traceable source for that institution type.

---

## Corrections and updates

Found an error? Use [YASA Verify](https://yasa.com.ng/verify) to submit corrections for coordinates, fees, websites, courses, and other fields. All submissions are reviewed before affecting the live dataset.
