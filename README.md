# Chicago Business License x Parcel Workflow

This repository was prepared by me as a Teaching Assistant for course materials and demo workflows around Chicago business-license data, parcel data, and commercial parcel matching.

The project is designed to show how to move from raw public data to reusable spatial analysis outputs. It combines business-license records, assessed-value class information, and parcel geometries so students can understand both the data-engineering side and the spatial-analysis side of the workflow.

## Project Background

Chicago business-license records contain business names, license metadata, and point locations from latitude and longitude. Parcel files contain polygon boundaries and parcel identifiers. These two sources do not come with a clean one-to-one join key for commercial analysis.

To solve that, the project uses a two-stage logic:

1. Build a commercial parcel filter from assessor class information.
2. Match business-license points onto parcel polygons with spatial joins.

This makes it possible to identify which commercial parcels have business activity in a given year, which commercial parcels do not, and how the workflow can scale across multiple years.

## Project Goals

- Understand the relationship between Chicago business licenses, assessor class data, and parcel geometry.
- Build a PIN-based commercial parcel subset before doing spatial matching.
- Match business-license points to parcel polygons.
- Export clean outputs for downstream analytics and mapping.
- Demonstrate both a teaching-oriented step-by-step workflow and a parcel-first workflow.

## Repository Workflows

### Lecture 1: Step-by-step teaching workflow

The first lecture notebook focuses on a more explicit teaching sequence:

1. Introduce the project context and the main datasets.
2. Inspect business-license data and parcel data.
3. Build a commercial PIN-class mapping from assessed-value records.
4. Join the commercial PIN mapping to parcel polygons.
5. Spatially match business-license points onto commercial parcels.
6. Export matched outputs for later analysis.
7. Extend the workflow into a reusable multi-year pipeline.

Main file:
- `Lecture1_stu_demo.ipynb`

## Lecture 2: Parcel-first commercial mapping

The second lecture notebook reorganizes the same problem around commercial parcels as the main unit of analysis:

1. Start from parcel polygons for one analysis year.
2. Use the Step 1 PIN-class output to classify parcels as commercial or non-commercial.
3. Keep commercial parcels as the base table.
4. Load license records for the selected year.
5. Attach business points to parcel polygons by spatial join.
6. Preserve both matched and unmatched commercial parcels.
7. Export parcel-centered outputs and interactive map outputs.
8. Extend the parcel-first logic to a multi-year pipeline.

Main file:
- `Lecture2_newdemo.ipynb`

## Core Data Sources

- Chicago Business Licenses
- Cook County Assessor Assessed Values
- Local parcel shapefiles by year

The notebooks use local-first paths for teaching stability, while still documenting official portal or API sources where useful.

## Main Output Types

- Commercial parcel base tables
- Commercial parcel GeoPackage outputs
- Matched business-license GeoParquet or Parquet outputs
- GeoJSON outputs for map-ready sharing
- Interactive HTML maps for parcel-first exploration

## Why This Project Is Useful For Teaching

This project is useful in class because it combines several important skills in one realistic workflow:

- tabular data cleaning
- field normalization between datasets
- PIN-based joins
- point-in-polygon spatial joins
- parcel-level aggregation
- multi-year pipeline thinking
- export design for analytics and visualization

It also gives students a concrete example of how public-sector business data can be reorganized into a spatial analysis product that is easier to inspect, explain, and reuse.

## Repository Structure

- `Dataset/`: local source data used by the notebooks
- `Outputs/`: generated analysis outputs and map products
- `Lecture1_stu_demo.ipynb`: teaching-oriented end-to-end workflow
- `Lecture2_newdemo.ipynb`: parcel-first commercial mapping workflow

## Notes

Large raw files and generated outputs are intentionally filtered from Git tracking where appropriate so the repository stays pushable and easier to share on GitHub.