# Chicago Business License x Parcel Workflow

This repository contains teaching materials and reproducible workflows for linking Chicago business licenses with parcel-level commercial land use data.

Prepared by me as a **Teaching Assistant (TA)** to support class demos, student practice, and project-based learning.

## What This Project Does

- Builds a parcel-first commercial base from assessor / parcel datasets.
- Joins business license records to commercial parcels.
- Exports analysis-ready geospatial outputs (GeoParquet / GeoJSON / GPKG).
- Produces an interactive map to explain matched and unmatched records.

## Repository Structure

- `Dataset/`: source datasets used in class demos.
- `Lecture1_stu_demo/`: lecture 1 teaching slides, notebooks, and examples.
- `Lecture1_stu_demo.ipynb`: lecture 1 student demo notebook.
- `Lecture2_newdemo.ipynb`: parcel-first + multiyear workflow notebook.
- `Outputs/`: generated outputs (ignored for git tracking in most cases).
- `docs/images/`: screenshots and visual assets for this README.

## Core Workflow (High-Level)

1. Load parcel and assessor data for a target year.
2. Filter to commercial parcels using land-use / class logic.
3. Load business license data and standardize geometry.
4. Spatially join licenses to commercial parcels.
5. Export matched/unmatched results for analysis and map visualization.

## Demo Visuals

### 1) Interactive Map (Must-Have)

![Interactive map overview](docs/images/interactive-map-overview.png)

Suggested captures:
- Map full view at city scale.
- One zoomed-in neighborhood example.
- Popup details for a matched record.
- Legend/layer controls panel.

### 2) Workflow Pipeline

![Workflow pipeline](docs/images/workflow-pipeline.png)

Suggested content:
- Step 1: Commercial parcel base
- Step 2: License preprocessing
- Step 3: Spatial join
- Step 4: Exports (GeoJSON / Parquet)

### 3) Data Join Outcome Snapshot

![Join summary table](docs/images/join-summary-table.png)

Suggested content:
- Total licenses (year)
- Matched count / unmatched count
- Match rate

### 4) Parcel-Level Result Example

![Parcel-level matched example](docs/images/parcel-level-example.png)

Suggested content:
- Example parcel geometry
- Linked business count
- Business activity status

## Recommended Screenshot List

For project storytelling, these screenshots are highly recommended:

1. `interactive-map-overview.png` (city-level map intro)
2. `interactive-map-zoom-example.png` (neighborhood zoom-in)
3. `interactive-map-popup-example.png` (record details popup)
4. `workflow-pipeline.png` (method explanation)
5. `join-summary-table.png` (business result summary)
6. `commercial-parcels-before-after.png` (filtering effect)
7. `matched-vs-unmatched-map.png` (comparison view)
8. `output-files-preview.png` (export deliverables)

## How To Run

1. Open the notebooks in VS Code or Jupyter.
2. Use the project Python environment (`.venv`).
3. Run `Lecture1_stu_demo.ipynb` for introductory workflow.
4. Run `Lecture2_newdemo.ipynb` for parcel-first and multiyear workflow.

## Notes

- Large raw/generated files are intentionally excluded from git history.
- If a map HTML is too large, keep it in local outputs and store screenshots in `docs/images/` for documentation.

---

If you want, I can also help you polish this README into a portfolio style version (with cleaner visual hierarchy and bilingual EN/ZH sections).
