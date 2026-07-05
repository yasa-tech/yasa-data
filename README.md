# YASA: Nigeria's Free Geospatial Higher Education Finder

**YASA (Your Admission, Spatial & Accessible)** is Nigeria's first nationally comprehensive, geocoded, and freely accessible database of JAMB-eligible higher institutions, delivered as a live, open-access web platform.

🌐 **Live Platform:** [yasa.ng](https://yasa.ng)
🗺️ **Verify Data:** [yasa.ng/verify](https://yasa.ng)
📧 **Research Access:** research@yasa.ng
📧 **inquiries & others:** info@yasa.ng
---

## 📊 What YASA Covers

* **1,558 Higher Institutions** — Every single JAMB IBASS-eligible university, polytechnic, monotechnic, college of education, and affiliated vocational college in Nigeria.
* **28,267 Accredited Programmes** — Mapped with exact UTME subject combination requirements.
* **Geocoded Spatial Coordinates** — The only complete, publicly accessible geocoded version of this institutional dataset in West Africa.
* **Health Facility Proximity Tracking** — Exact physical distance to the nearest GRID3-listed health centre for every listed campus.
* **Wikipedia-Enriched Metadata** — Founding years, institutional mottos, campus images, and local structural context.
* **Free to use** — Zero user registration walls for discovery, zero fees, and completely easy to navigate.

---

## 🎯 The Problem It Solves

In 2025, nearly 2 million Nigerians sat for the UTME. While JAMB's IBASS database remains the authoritative record of eligible institutions, it contains zero coordinate data, lacks cross-institutional search engines, and features no program-level geographic filtering by subject combination.

Some prospective students cannot easily identify which polytechnics near them offer a specific nursing or engineering program matching their exact JAMB subjects. YASA bridges this information gap, removing commercial barriers between data-compromised terrains and the students who need them.

---

## 🧪 Key Findings From the Data

Building this database surfaced two systematic data quality issues in standard IBASS reporting that affect any regional research relying on national geographic classifications:

* **14.2% of institution names** embed affiliation references that cause standard geocoding services to return incorrect coordinates—anchoring to a parent university instead of the actual physical campus.
* **7.7% of institutions (120 records)** are mistakenly assigned to the wrong Nigerian state within the source database due to geographical naming references.

Both empirical findings are documented in our research paper currently under a journal peer review. 

---

## 🔬 Citizen Science — YASA Verify

Coordinate accuracy for flagged higher institutions is continuously optimized through [YASA Verify](https://yasa.ng/verify)—a crowdsourced citizen science engine. 

To prevent data compromise, our validation script operates under a consensus model: **three independent matching submissions trigger an automated coordinate update.** Contributors earn leaderboard points, public badges, and—at 10 verified institutions—a downloadable institutional Certificate of Contribution.

---

## 🔑 Research & Data Access

This geocoded dataset serves as the foundation for peer-reviewed research on West African educational access equity. We strictly protect our data pipeline and do not distribute raw, bulk database files to protect our research integrity.

* **For Research Access:** Email research@yasa.ng. 
Coming soon: We will grant secure, structured **Tier 3 API access keys** and regional data teaser extracts to verified researchers under an official Data Use Agreement requiring academic attribution.

### To Cite YASA:
```text
Oluwaseun Ipede, Olalekan Alausa and Babalola Adewara. YASA: A Geospatial Intelligence Framework for Educational Institution Discovery and Access Equity in Sub-Saharan Africa (Evidence from Nigeria). ScienceOpen Preprints. 2026. DOI: 10.14293/PR2199.003816.v2
```

---

## 🌍 Expand YASA to Your Country — YASA Africa

YASA's underlying methodology is built to scale smoothly across national tertiary admission networks facing similar structural data constraints (e.g., Ghana's CSSPS, Kenya's KUCCPS, or Tanzania's TCU).

We are actively seeking **country partners and institutional co-authors** to expand **YASA Africa**. If you represent a university department, regional research group, or civic technology organization interested in deploying this geospatial framework in your nation, please connect with us:

📧 **Contact:** research@yasa.ng | [yasaafrica.com](http://yasaafrica.com)

---

## 🛠️ What's in This Repository

This repository serves as our public sample sandbox and technical documentation layer. To protect YASA's long-term data governance, intellectual property, and proprietary pipeline, **the production scrapers, core database scripts, and ranking algorithms remain private.**

| Path | Contents |
| :--- | :--- |
| 📁 `sample-institutions.json` | **The Teaser Dataset:** 12-institution structured JSON sample proving data schema. |
| 📁 `data-schema.md` | field definitions, metadata rules, and institutional keys. |
| 📁 `data-quality.md` | Underlying geocoding methodology and regional anomaly statistics. |
| 📁 `contributing.md` | Guidelines for formatting field error submissions via YASA Verify. |

---

## 📜 Licensing

* **Sample Sandbox Data:** [CC BY 4.0](https://creativecommons.org)
* **Wikipedia Metadata Content:** [CC BY-SA 4.0](https://creativecommons.org) (Attributed per Wikimedia Terms)
* **Health Facility Layer Data:** [CC BY 4.0](https://creativecommons.org) (Attributed to GRID3 Nigeria)

---
*YASA is an autonomous, free public utility registered with the Corporate Affairs Commission (CAC), Nigeria. It holds no official commercial relationship with JAMB, the NUC, or any listed tertiary institution.*
