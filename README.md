# Chicago Business License x Parcel Workflow

Teaching materials and demo workflows for Chicago business-license and parcel-based spatial data analysis.

## Why This Repository Exists

This repository was prepared by me in my role as a **Teaching Assistant (TA)** to support classroom demos, student practice, and reproducible geospatial data-analysis workflows.

## Project Goals

- Build a parcel-first commercial analysis workflow.
- Match business-license records to commercial parcels.
- Export map-ready outputs (GeoParquet/GeoJSON/HTML).
- Provide notebook-based teaching demos for step-by-step learning.

## Repository Structure

- `Lecture1_stu_demo.ipynb`: student-facing demo notebook.
- `Lecture2_newdemo.ipynb`: updated parcel-first workflow notebook.
- `Dataset/`: source datasets (licenses, assessor data, parcels).
- `Outputs/`: generated artifacts (ignored by git).
- `Lecture 1_stu_demo/`: lecture slides and supporting materials.

## Quick Start

1. Create and activate a Python environment (recommended: Python 3.11 or 3.12).
2. Install core packages: `pandas`, `geopandas`, `shapely`, `pyproj`, `folium`.
3. Open notebooks in VS Code and run cells step by step.

## Suggested Visuals For This README

The **interactive map screenshot is a must-have**. In addition, these visuals are strongly recommended:

1. **Interactive Map Overview (Must-have)**
   - Show matched vs unmatched businesses on commercial parcels.
   - Suggested filename: `docs/images/interactive-map-overview.png`
2. **Workflow Diagram (Pipeline)**
   - Parcel filtering -> spatial join -> export parquet/geojson -> interactive map.
   - Suggested filename: `docs/images/workflow-pipeline.png`
3. **Data Coverage Snapshot**
   - Simple chart/table image: total licenses, matched records, unmatched records.
   - Suggested filename: `docs/images/data-coverage-summary.png`
4. **Before/After Match Comparison**
   - Side-by-side figure showing raw license points vs parcel-joined result.
   - Suggested filename: `docs/images/before-after-matching.png`
5. **Output Artifacts Preview**
   - Screenshot of exported files (GeoParquet/GeoJSON/HTML map).
   - Suggested filename: `docs/images/output-artifacts-preview.png`

## Image Placeholder Section

When your images are ready, place them under `docs/images/` and uncomment/update links below.

![Interactive map overview](docs/images/interactive-map-overview.png)

![Workflow pipeline](docs/images/workflow-pipeline.png)

![Data coverage summary](docs/images/data-coverage-summary.png)

![Before and after matching](docs/images/before-after-matching.png)

![Output artifacts preview](docs/images/output-artifacts-preview.png)

## Notes

- Large generated files are excluded via `.gitignore`.
- Keep raw datasets in `Dataset/` and generated results in `Outputs/`.
- If a file exceeds GitHub limits, keep it local or use Git LFS.

## Acknowledgement

Prepared as TA teaching support material for the Chicago Business License x Parcel data-analysis course.
