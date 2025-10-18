# Measuring Crime Concentration Near MBTA Stations in Boston

## Team Members
- Mohamad Gong (Project Manager)  
- Yanlun Li  
- Fei Han  
- Kai  
- Rita Feng  
- Abbinaya  

## Overview
This repository houses a geospatial analysis exploring how police‑reported crime concentrates near MBTA rapid‑transit stations in Boston. By combining Boston Police incident reports for **2016–2025** with official station locations and walking‑time buffers from Mapbox, the project examines **when and where** different types of offenses cluster around transit hubs.

## Data Sources
- **Crime Incident Reports** – Incident‑level reports from the Boston Police Department’s new crime incident reporting system. The data capture the type of incident and when and where it occurred; records begin in **June 2015**. Source: [data.boston.gov](https://data.boston.gov/).
- **Offense Codes Lookup** – XLSX file mapping numeric offense codes to descriptive offense names and used to decode the offense code field. Source: [data.boston.gov](https://data.boston.gov/).
- **MBTA Rapid Transit Stations** – Point layer representing the station stops on the five subway, streetcar/trolley, and Silver Line bus lines in the MBTA rapid‑transit network; point features reside in the **MBTA_NODE** class. Source: [mass.gov](https://www.mass.gov/).
- **Police Districts** – GeoJSON file delineating the authoritative police districts for the City of Boston. Source: [data.boston.gov](https://data.boston.gov/).
- **Isochrone Polygons** – Generated via the Mapbox Navigation API to create **1‑, 3‑, and 5‑minute** walking buffers around each station.

## Methodology
### Data Preparation
- Imported and cleaned nine annual crime CSV files.  
- Corrected missing offense names.  
- Dropped approximately **5 %** of records without geocoded coordinates.  
- Loaded station and district geometries with **GeoPandas** and ensured consistent coordinate systems.

### Isochrone Generation
- Used a Mapbox access token to create **1‑, 3‑, and 5‑minute** walking isochrones for each station, producing rings that represent the potential walking area around stations.

### Spatial Joins
- Assigned each incident to the appropriate isochrone ring via nearest‑station spatial joins, classifying incidents as within **1‑, 3‑, 5‑minute** walksheds or **outside** these zones.

### Analysis
- Summarised incidents by year, offense type, station, MBTA line, and police district using **pandas**, **seaborn**, and **contextily** to generate charts and maps.

## Key Findings
- Citywide incidents declined roughly **30–35 %** during **2020–23** and only partially rebounded in **2024–25**.  
- Around **40 %** of crimes occur within a **five‑minute** walk of a rapid‑transit station, with the **three‑minute** ring capturing the largest share.  
- **Larceny and theft** offences are over‑represented near stations, whereas **serious violence** shows weaker proximity patterns.  
- Stations on the **Silver** and **Green** lines—particularly **Park Street**, **Union Park Street**, and **Nubian**—record the highest counts across all rings.  
- Activity peaks from **late morning through early evening** on weekdays, matching commuter and retail flows.  
- The **three‑minute** walkshed contains most actionable, station‑adjacent risk; incident density diminishes beyond **five minutes**.

## Using This Repository
1. **Clone** the repository and install the Python dependencies (`pandas`, `geopandas`, `contextily`, `matplotlib`, `seaborn`, `shapely`).  
2. **Obtain** a Mapbox access token to generate isochrones.  
3. **Download** the crime, station, and district datasets from the sources listed above. Update the paths in the notebook to match your data directories.  
4. **Run** the Jupyter notebook `B09-Measuring-Crime-Concentration-Near-MBTA-Stations-Boston.ipynb` from top to bottom to reproduce the analysis and generate summary tables and visualisations.

## Challenges and Limitations
- Approximately **5 %** of crime records lacked latitude/longitude coordinates and were excluded, which may under‑represent certain districts.  
- Offense code inconsistencies required manual grouping, and reporting practices can introduce temporal biases.  
- The **2025** data was incomplete at the time of analysis; results for that year reflect only **partial‑year** activity.

## References
Crime and station datasets are available via Boston’s open‑data portal and MassGIS:  
- [data.boston.gov](https://data.boston.gov/)  
- [mass.gov](https://www.mass.gov/)  

_See the notebook for a full list of sources and links._
