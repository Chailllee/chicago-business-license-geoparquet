---
marp: true
paginate: true
theme: default
title: Chicago Business License x Parcel Workflow
description: English slide guide based on Lecture1 student demo
---

# Chicago Business License x Parcel
## Lecture 1 Demo Guide

Business Data Analytics Workflow for Chicago business licenses, assessor class records, and parcel polygons

---

# Project Background

**Learning Goals**

- Understand the project context and core data sources
- Import and inspect local and online public datasets
- Build a commercial parcel subset through PIN to class mapping
- Match business license points to parcel polygons with a spatial join
- Export clean outputs for downstream analytics

---

# Notebook Structure

## Part 1. Preparation and Project Background
## Part 2. Data Import and Dataset Understanding
## Part 3. Combination Workflow (Step 1/2/3)
## Part 4. Scalable Multi-Year Pipeline

---

# Part 1. Preparation

## 1-1. Preparation: Environment and Python Basics

- Recommended Python version: 3.11 or above
- Use a local virtual environment in the project root
- Select the same interpreter for both scripts and notebooks
- Core packages: pandas, geopandas, matplotlib, pyarrow, shapely, pyogrio, fiona
- Optional helpers: requests for APIs, tqdm for progress bars

---

# Part 1. Preparation

## 1-2. Task Background

Chicago business license records contain location information, but they do not directly link to parcel polygons.

**Project objectives**

- Identify commercial parcels from assessor class information
- Match business license locations to parcel geometries
- Build analysis-ready yearly tables
- Save outputs in fast, reusable formats

---

# Part 1. Preparation

## 1-2. Core Challenge and Solution Pattern

- Business licenses are point records with latitude and longitude
- Parcels are polygon features in a shapefile or geospatial package
- The two sources do not share a direct join key
- A commercial-only subset must be built before spatial matching

**Solution pattern**

PIN-Class mapping plus point-in-polygon spatial join

---

# Part 2. Data Import and Source Overview

Three main data inputs drive the demo:

1. Chicago Business Licenses
2. Cook County Assessor Assessed Values
3. Local parcel shapefiles by year

The notebook is designed in a local-first style, with online endpoints kept as optional references.

---

# Part 2. Data Import and Source Overview

## 2-1. Business Licenses Dataset

**Main use in this demo**

- Read the full local CSV for stable classroom execution
- Keep OData and resource endpoints as optional online sources
- Inspect columns before filtering by year or geometry availability

**Key columns**

- LICENSE ID
- LEGAL NAME / DOING BUSINESS AS NAME
- LICENSE DESCRIPTION
- LICENSE TERM START DATE / LICENSE TERM EXPIRATION DATE
- LICENSE STATUS
- LATITUDE / LONGITUDE
- ADDRESS

---

# Part 2. Data Import and Source Overview

## 2-2. Parcel Dataset (Example Year: 2016)

**Main use in this demo**

- Load parcel polygons for one selected year
- Confirm row count and coordinate reference system
- Inspect a few structural columns before joining

**Key columns**

- PIN10: normalized parcel key for cross-dataset matching
- PARCELTYPE: parcel category code
- SHAPE_STAr: area
- SHAPE_STLe: perimeter
- geometry: polygon geometry used in the spatial join

---

# Part 2. Data Import and Source Overview

## 2-3. Why We Need PIN-Class Mapping

**Core logic**

1. Use the assessed values table to map PIN to class
2. Select commercial class codes
3. Convert the assessor PIN format into a parcel-compatible key
4. Join selected PINs to parcel polygons
5. Run the spatial join from license points to commercial parcels

---

# Part 2. Data Import and Source Overview

## 2-3. PIN Format Alignment

**Source format difference**

- Assessor keypin example: 01-02-202-045-0000
- Parcel PIN10 example: 0102202045

**Standardization rule**

- Remove non-digit characters
- Keep the first 10 digits
- Zero-pad when necessary
- Store the result as pin10_key for joining

---

# Part 2. Data Import and Source Overview

## 2-4. Commercial Class Filter

The demo uses a class-code strategy instead of parcel type labels.

**Two-layer selection logic**

- Primary whitelist: core commercial classes from major groups 5, 7, and 8
- Supplement whitelist: mixed-use and partially commercial classes from other groups

**Output of this step**

- A normalized list of target commercial class codes

---

# Part 3. Combination Workflow (Step 1/2/3)

This section turns separate datasets into one analysis workflow.

**Three operational stages**

1. Filter commercial PIN-class records
2. Join parcels with filtered commercial PINs
3. Match business licenses to commercial parcels

---

# Part 3. Combination Workflow (Step 1/2/3)

## Step 1. Filtering PINs by Commercial Classification

**Input**

- Assessor Assessed Values dataset

**Goal**

- Keep only records whose class belongs to the selected commercial list
- Build a clean mapping between raw PIN, class, and normalized pin10_key

---

# Part 3. Combination Workflow (Step 1/2/3)

## Step 1-A. Build Filtered PIN-Class Records

**Processing logic**

- Support both local CSV mode and online API mode
- Read only needed columns when processing large files
- Normalize class codes into digit-only comparison values
- Normalize PIN values into join-ready pin10_key values
- Export deduplicated records in chunks when needed

**Why this matters**

This is the bridge between assessor classification and parcel geometry.

---

# Part 3. Combination Workflow (Step 1/2/3)

## Step 1-B. Summarize and Save

**Main outputs**

- Unique filtered PIN-class table
- Class distribution summary
- PIN10-level summary with class_count and class_list
- Progress and profiling files for reproducibility

**Teaching point**

Keep raw filtered records and parcel-level summaries as separate outputs.

---

# Part 3. Combination Workflow (Step 1/2/3)

## Step 2. Parcel x Assessed Commercial Classes

**Goal**

- Load one parcel layer for a selected year
- Join parcel polygons to the Step 1 commercial PIN summary
- Produce a commercial-only parcel dataset

This creates the geospatial target layer for the next spatial join.

---

# Part 3. Combination Workflow (Step 1/2/3)

## Step 2-A. Load Parcels and Step 1 Outputs

**Processing logic**

- Read the parcel shapefile for a chosen year
- Read the filtered Step 1 PIN-class export
- Normalize parcel PIN10 into the same pin10_key format
- Validate row counts and CRS before merging

**Key check**

If the parcel file or Step 1 export is missing, stop early with a clear error.

---

# Part 3. Combination Workflow (Step 1/2/3)

## Step 2-B. Aggregate, Merge, and Export

**Parcel-level enrichment**

- Group filtered classes by pin10_key
- Compute class_count per parcel
- Build class_list to preserve multi-class parcels
- Inner join to keep only commercial parcels

**Main outputs**

- GeoPackage with commercial parcel geometry
- CSV with commercial parcel attributes

---

# Part 3. Combination Workflow (Step 1/2/3)

## Step 3. Match Business Licenses to Commercial Parcels

**Goal**

- Prepare one year of business license records
- Convert valid license rows into point geometries
- Spatially match those points to commercial parcel polygons
- Save matched results for analysis

---

# Part 3. Combination Workflow (Step 1/2/3)

## Step 3-A. Standardize and Filter Licenses for One Year

**Processing logic**

- Support both local CSV and online API loading
- Standardize column names from possible source variations
- Parse dates and coordinates into analysis-ready types
- Build validity logic for the selected year
- Separate all valid rows from valid rows with usable coordinates

**Important derived fields**

- start_eff
- is_valid_in_year
- active_now
- license_group

---

# Part 3. Combination Workflow (Step 1/2/3)

## Step 3-B. Spatial Join and QA

**Geospatial workflow**

- Convert license latitude and longitude into point geometry
- Reproject points into the parcel CRS
- Apply a within predicate spatial join
- Review matched row counts, unique licenses, and unique parcels

**Quality checks**

- Match rate over valid geocoded licenses
- Distribution by license_group
- Preview of joined attributes

---

# Part 3. Combination Workflow (Step 1/2/3)

## Step 3-C. Export Matched Outputs

**Primary output**

- Geospatial Parquet of matched license records

**Why Parquet**

- Compact storage
- Fast downstream reading
- Good fit for analytics pipelines

Optional preview maps help students visually verify that the join behaves as expected.

---

# Part 4. Multi-Year Extension

The last section converts the one-year workflow into a scalable pipeline.

**Purpose**

- Detect available parcel years
- Add optional Google Drive parcel sourcing
- Reuse the same Step 2 and Step 3 logic across years
- Write a consolidated process log

---

# Part 4. Multi-Year Extension

## 4-1A. Detect Available Years and Output Paths

**Local workflow**

- Search parcel directories such as Dataset/Parcels/Parcel_YYYY
- Detect all available years automatically
- Prepare common output folders for Step 2 and Step 3 results
- Save a process log for multi-year runs

This removes hard-coded year lists from the pipeline.

---

# Part 4. Multi-Year Extension

## 4-1B. Google Drive Shared Link Opening

**Why this exists**

- Some parcel years may be stored in a shared Google Drive folder
- The notebook inspects archive contents before downloading everything

**Key idea**

- Parse the folder page
- Find Parcel_YYYY.zip archives
- Inspect zip members with HTTP range requests
- Decide whether a year contains shapefiles, geojson, or only tables

---

# Part 4. Multi-Year Extension

## 4-2. Define the Reusable One-Year Function

The notebook wraps the yearly logic into one reusable function.

**Function responsibilities**

- Load parcels from Google Drive or local fallback
- Normalize parcel PIN keys
- Build commercial parcels for that year
- Filter licenses for the same year
- Run the spatial join
- Save yearly outputs and return run metadata

---

# Part 4. Multi-Year Extension

## 4-3. Run the Workflow for All Years

**Pipeline execution pattern**

- Load the full license source once
- Load the Step 1 PIN-class source once
- Iterate through TARGET_YEARS
- Skip years that already have outputs when desired
- Save a run log with status, source, row counts, and match rates

This is the production-friendly version of the classroom demo.

---

# Key Outputs Across the Workflow

**Step 1**

- Filtered PIN-class exports
- Class summary tables

**Step 2**

- Commercial parcel GeoPackage
- Parcel attribute CSV

**Step 3**

- Matched license geospatial Parquet

**Part 4**

- Multi-year process log

---

# Teaching Takeaways

1. Public datasets often need key normalization before they can be combined.
2. Parcel filtering should happen before spatial matching to reduce noise.
3. Spatial joins work best after strong tabular preprocessing.
4. Export structure matters if the workflow must scale across multiple years.
5. A good teaching notebook balances reproducibility, clarity, and extensibility.

---

# End

## From Raw Public Data to Analysis-Ready Geospatial Outputs

Chicago Business Licenses x Assessor Classes x Parcel Geometry