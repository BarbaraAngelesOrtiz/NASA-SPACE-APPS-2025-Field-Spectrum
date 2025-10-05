# NASA Space Apps Challenge 2025 Field-Spectrum
# Technical Methodology: Heatwaves and Droughts in Agricultural Fields

## General Description of the Scripts

In recent years, Argentina has faced increasingly extreme climatic events, affecting both natural ecosystems and agricultural production. In January/February 2025, a historic heatwave swept across central and northeastern Argentina, with temperatures soaring above 40°C (104°F). This extreme heat, combined with prolonged drought, caused widespread stress in croplands, water scarcity, and reduced yields. [1][2][3] This type of phenomenon has happened in previous years. [4]
Conversely, in September/October 2024, late-season frosts affected central and southern agricultural regions, with temperatures dropping as low as, 4°C, damaging sensitive crops and impacting local food production.[5][6]

To study these phenomena, two custom scripts were developed and executed using the Sentinel Hub EO Browser tool, leveraging Landsat 8–9 OLI-TIRS Collection 2 Level 1 imagery and Synthetic Aperture Radar (SAR) data. The scripts are designed to visualize and monitor agricultural stress caused by extreme climatic events.

1.	Drought and Heatwave Script
	• Indices and bands: NDVI (B05–B04), NDWI (B03–B05), Brightness Temperature (B10)
  •	Methodology: Vegetation stress is detected through NDVI, water bodies through NDWI, and surface heat via thermal infrared measurements. Pixels affected by drought or heat are highlighted in red, healthy vegetation in green, and water bodies in blue. Cloud pixels are masked to black using the cirrus band (B09).
  •	Target site: Mar Chiquita, Córdoba Province, Argentina. Impacted by a prolonged dry period and extreme heatwave in January and February 2025.

3.	Frost Detection Script
  •	Indices and bands: NDVI (B05–B04), Brightness Temperature (B10), dataMask
  •	Methodology: Frost is identified as pixels with temperatures below 0°C that are not covered by clouds. Cold zones are rendered with a violet-blue gradient, vegetation in green, and clouds masked to black.
  •	Target site: Entre Ríos and Santa Fe provinces, Argentina, affected by late-season frosts in September and October 2024.

By combining these analyses, the scripts allow a temporal visualization of extreme climatic events on agricultural fields. EO Browser’s time-lapse function highlights the evolution of heatwaves, droughts, and frost events, providing a clear and visually compelling narrative of climate impact on croplands.[7][8]

These visualizations can support decision-making for agricultural management, disaster response, and long-term adaptation strategies, providing actionable insights for farmers, policymakers, and environmental agencies. [9] [10]

## Drought and Heatwave Detection

### Concept
Drought and heatwaves are two interrelated phenomena that cause vegetation stress and soil moisture depletion.
By combining vegetation indices with surface temperature and water presence, the script visualizes agricultural areas affected by heat and dryness.

### Satellite source
•	Satellite: Landsat 8–9 Level 1
•	Instruments: OLI (Optical Land Imager) and TIRS (Thermal Infrared Sensor)
•	Spatial resolution: 30 m
•	Spectral bands used:

Band	Description	Unit	Purpose
B03	Green (0.53–0.59 µm)	Reflectance	NDVI / NDWI calculation
B04	Red (0.64–0.67 µm)	Reflectance	NDVI calculation
B05	Near Infrared (0.85–0.88 µm)	Reflectance	NDVI / NDWI
B09	Cirrus (1.36–1.38 µm)	Reflectance	Cloud masking
B10	Thermal Infrared (10.6–11.19 µm)	Brightness Temperature (K)	Surface temperature estimation
 

