# Earthquake_Project_Data_Engineering_Fabric

This project showcases a data engineering and analytics solution built with **Microsoft Fabric**. The goal is to ingest worldwide earthquake events from the USGS API, process the data through multiple refinement stages, and visualise the results in Power BI.

## Objectives
- Automate retrieval of earthquake data using Fabric Data Factory.
- Transform and enrich the data with PySpark notebooks in the Bronze, Silver and Gold layers.
- Provide business-ready tables for reporting.
- Share insights via an interactive Power BI dashboard.

## Pipeline Overview
1. **Bronze layer** – `01 Worldwide Earthquake Events API - Bronze Layer Processing (1).ipynb`
   - Fetches data from the USGS API using a start and end date.
   - Saves the raw JSON response to the Fabric lakehouse for traceability.
2. **Silver layer** – `02 Worldwide Earthquake Events API - Silver Layer Processing (1).ipynb`
   - Reads the Bronze JSON file into a Spark DataFrame.
   - Extracts key attributes such as coordinates, magnitude and timestamps.
   - Converts epoch times to timestamp format and writes to a managed table `earthquake_events_silver`.
3. **Gold layer** – `03 Worldwide Earthquake Events API - Gold Layer Processing (1).ipynb`
   - Adds location information (country code) via the `reverse_geocoder` library.
   - Classifies events by significance to create a `sig_class` column.
   - Outputs the final table `earthquake_events_gold` used for analytics.
4. **Visualisation** – `Worldwide Earthquake Events.pbix`
   - A Power BI report consuming the Gold dataset.
   - [Interactive dashboard link](https://app.fabric.microsoft.com/links/PxK3aYkNLB?ctid=e4bd69ff-e6f7-4c2e-b247-41b54ba2490e&pbi_source=linkShare)
   - [Static PDF](https://github.com/user-attachments/files/19463369/Worldwide.Earthquake.Events.pdf)

## Data Source
Data is ingested from the [USGS Earthquake Hazards Program](https://www.usgs.gov/programs/earthquake-hazards).

## Technologies Used
- Python and PySpark
- Microsoft Fabric (Data Engineering, Data Factory, Power BI)

## Data Attributes
Each processed record includes the following fields:

- **id** – Unique identifier of the event
- **latitude** – Latitude in decimal degrees
- **longitude** – Longitude in decimal degrees
- **elevation** – Elevation in metres
- **title** – Descriptive title of the event
- **place_description** – Human-readable location name
- **sig** – Significance score
- **mag** – Magnitude
- **magType** – Magnitude scale used
- **time** – Event timestamp
- **updated** – Timestamp of the latest update

## Running the Notebooks
1. Create a Microsoft Fabric workspace and lakehouse.
2. Upload the notebooks to the workspace.
3. Use Data Factory to schedule the Bronze notebook with the desired `start_date` and `end_date` parameters.
4. Execute the Silver and Gold notebooks sequentially to populate the tables.
5. Open the Power BI report (`Worldwide Earthquake Events.pbix`) to explore the data.

---

This repository provides a simple example of building a multi-stage data pipeline in Microsoft Fabric to analyse earthquake data end-to-end.
