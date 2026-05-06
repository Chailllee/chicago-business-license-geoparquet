# Chicago Business License x Parcel Workflow

This repository was prepared by me as a Teaching Assistant for a data analytics training project.
The goal is to teach a complete geospatial workflow from raw public records to parcel-centered, map-ready outputs.

## Teaching Assistant Context

I prepared this project to support course delivery, student practice, and reproducible demonstrations.

Main TA preparation goals:
- Build a clear end-to-end notebook workflow for class
- Keep data processing steps transparent and easy to explain
- Provide reusable outputs for lecture demos and student exercises
- Offer both single-year and multi-year examples

## Project Background

Chicago business license records contain business attributes and coordinates.
Parcel datasets contain polygon boundaries and parcel identifiers.
Assessor class mapping helps identify commercial parcels.

The project combines these sources to answer:
- Which commercial parcels have business activity in a selected year?
- Which commercial parcels have no matched business points?
- How can we export analysis-ready and map-ready datasets for downstream use?

## Data Sources

- Chicago Business Licenses
  - Local CSV used in class workflow
  - Optional OData endpoint references in notebooks
- Cook County Assessor Assessed Values
  - Used to build PIN-to-class mapping
- Parcel geometry files
  - Local shapefiles by year under Dataset/Parcels

## Learning Objectives

- Understand parcel-first and license-to-parcel matching logic
- Build commercial parcel subsets from PIN-class mapping
- Run spatial joins between license points and parcel polygons
- Generate clean yearly outputs (Parquet, GeoJSON, GeoPackage)
- Build interactive maps for communication and QA

## Workflow Overview (Lecture 1 and Lecture 2)

### Lecture 1: Foundation Pipeline

1. Environment and dependency setup
2. Dataset inspection (license, assessed values, parcels)
3. Step 1: PIN-class filtering for commercial classes
4. Step 2: Join filtered PIN classes to parcel polygons
5. Step 3: Spatially match license points to commercial parcels
6. Export yearly outputs for analysis
7. Extend to multi-year processing

### Lecture 2: Parcel-First Commercial Mapping

1. Build commercial parcel base table for selected year
2. Load licenses and derive active/inactive year status
3. Spatial join (parcel-centered view)
4. Export final parcel-centered files
5. Build interactive map preview
6. Run multi-year pipeline
7. Backfill map previews from existing GeoJSON

## Repository Structure

- Lecture1_stu_demo.ipynb: Lecture 1 teaching workflow
- Lecture2_newdemo.ipynb: Lecture 2 parcel-first workflow
- Dataset/: Input datasets used for class demos
- Outputs/: Generated outputs (ignored in git for large artifacts)
- docs/images/: Suggested location for README screenshots

## Suggested Visuals for Project Introduction

To make the project easy to understand for students and reviewers, add screenshots to docs/images and reference them here.

Recommended screenshot set:
- Workflow overview diagram (one-page flow from source data to outputs)
- Lecture 1 key table preview (commercial PIN-class mapping summary)
- Lecture 2 parcel base map snapshot (commercial parcels)
- Spatial join result preview (matched vs unmatched commercial parcels)
- Interactive map screenshot (must-have)
- Multi-year summary table screenshot

Recommended screenshot file names:
- docs/images/01_workflow_overview.png
- docs/images/02_pin_class_mapping_preview.png
- docs/images/03_commercial_parcel_base.png
- docs/images/04_spatial_join_result.png
- docs/images/05_interactive_map.png
- docs/images/06_multiyear_summary.png

## Interactive Map Screenshot Tips (Strongly Recommended)

For your interactive map screenshot, capture one full view with:
- Layer control panel opened
- Matched commercial parcels visible (green)
- Unmatched commercial parcels visible (red)
- Business point layer visible
- Clear title or caption showing analysis year

Optional extra map screenshots:
- Zoomed downtown area (dense business activity)
- Peripheral area (lower density comparison)
- Before/after layer toggle comparison

## How To Update README Screenshots

1. Put images into docs/images
2. Keep the filenames stable using the naming list above
3. Add image links to this README under a new section called Visual Gallery

## Notes

- Very large raw and output files are excluded from git tracking
- Keep this repository focused on teaching notebooks and reproducible logic
- For production pipelines, consider separate storage for heavy artifacts
