# Metronetwork-MexicoCity
Data repository and processing workflow for InSAR time-series analysis and structural deformation.
This repository contains data access links, supplementary files, and a comprehensive methodological summary of the InSAR time-series and structural deformation analysis conducted for Mexico City Metro network (June 2020 – March 2026).

---

## 📂 1. Data Sources & Access Links

### A. Synthetic Aperture Radar (SAR) Data & HyP3 Processing
The raw radar datasets used in this study originate from the **Sentinel-1** satellite, covering Mexico City with **246 pairs of Sentinel-1 SLC images** from June 2020 to March 2026.
* **Raw Data Access:** Users can freely search and download the raw Sentinel-1 datasets via the [Alaska Satellite Facility (ASF) Vertex](https://search.asf.alaska.edu/#/).
* **Interferogram Generation (GAMMA via HyP3):** Using NASA’s HyP3 service, **291 interferograms** were generated, establishing a dense network of phase observations.

### B. Time-Series Inversion & Processing Workflow (MintPy)
While NASA provided the individual maps, **MintPy** acts as the Time Series Processor to stitch them all together:
1. **Atmospheric Correction & Preparation:** MintPy reads the interferogram files and performs advanced atmospheric corrections using meteorological models (e.g., ERA5) to remove noise caused by water vapor.
2. **Inversion & Phase Unwrapping:** MintPy solves a complex system of equations for every single pixel, converting phase connections into **179 independent displacement epochs/maps**.
3. **Golden Files Output:** The final output yields key products, most notably the **3D Time Cube (`timeseries.h5`)**. This file contains the centimeter-scale movement for each pixel across all recorded dates (2020–2026), serving as the final target variable fed into our Transformer model for predictive analysis.

### C. Metro Station & Infrastructure Data
* **Line and Stations Geometry:** Spatial data for the metro lines and stations were obtained from the [CDMX Open Data Portal](https://www.datos.cdmx.gob.mx/dataset/lineas-y-estaciones-del-metro/resource/288b10dd-4f21-4338-b1ed-239487820512). *(A copy of these files is available in the [`data/`](./data/) folder of this repository).*
* **Station Usage & Statistics:** Additional operational and passenger statistics were retrieved from the [CDMX Metro Official Statistics](https://www.metro.cdmx.gob.mx/estacion-por-uso-y-tipo).

### D. Soil Type and Geotechnical Data
* **Soil Classification:** Regional soil and geological information were acquired from the [INEGI Map Viewer](https://www.inegi.org.mx/app/mapas/). *(Sample or vector files used in this study are provided in the [`data/soil/`](./data/soil/) directory).*

---

## ⚙️ Summary of Methodological Pipeline
1. **Interferometric Processing:** 246 Sentinel-1 SLC image pairs processed via NASA HyP3 (GAMMA engine) yielding 291 interferograms.
2. **Time-Series Analysis:** MintPy SBAS inversion, atmospheric filtering (ERA5), and reference point calibration producing 179 independent displacement maps.
3. **Model Integration:** Generation of the 3D Time Cube (`timeseries.h5`) as the definitive target variable for downstream deep learning (Transformer) predictive modeling.

---

## 📝 Citation
If you utilize these insights, data links, or methodological frameworks in your research, please refer to our corresponding publication.
