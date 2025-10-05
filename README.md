# 🌎 NASA Space Apps Challenge 2025 Field-Spectrum
# 🛰️ Technical Methodology: Heatwaves and Droughts in Agricultural Fields 

## General Description of the Scripts

In recent years, Argentina has faced increasingly extreme climatic events, affecting both natural ecosystems and agricultural production. In **January/February 2025**, a historic heatwave swept across central and northeastern Argentina, with temperatures soaring above 40°C (104°F). This extreme heat, combined with prolonged drought, caused
widespread stress in croplands, water scarcity, and reduced yields. \[1\]\[2\]\[3\] This type of phenomenon has happened in previous years. \[4\]

Conversely, in **September/October 2024**, late-season frosts affected central and southern agricultural regions, with temperatures dropping as low as, 4°C, damaging sensitive crops and impacting local food production.\[5\]\[6\]

To study these phenomena, two custom scripts were developed and executed using the **Sentinel Hub EO Browser tool**, leveraging **Landsat 8-9 OLI-TIRS Collection 2 Level 1** imagery and **Synthetic Aperture Radar (SAR) data**. The scripts are designed to visualize and monitor agricultural stress caused by extreme climatic events.\[11\]

1.  **Drought and Heatwave Script**

    -   **Indices and bands:** NDVI (B05-B04), NDWI (B03-B05), Brightness Temperature (B10)

    -   **Methodology:** Vegetation stress is detected through NDVI, water bodies through NDWI, and surface heat via thermal infrared measurements. Pixels affected by drought or heat are highlighted in **red**, healthy vegetation in **green**, and water bodies in  **blue**. Cloud pixels are masked to black using the cirrus band (B09).

    -   **Target site:** Mar Chiquita, Córdoba Province, Argentina. Impacted by a prolonged dry period and extreme heatwave in January and February 2025.

Here the [Drought and Heatwave script](./Script/drought%20%2B%20heat%20wave.txt)

2.  **Frost Detection Script**

    -   **Indices and bands:** NDVI (B05-B04), Brightness Temperature (B10), dataMask

    -   **Methodology:** Frost is identified as pixels with temperatures  below 0°C that are **not covered by clouds**. Cold zones are rendered with a **violet-blue gradient**, vegetation in green, and clouds masked to black.

    -   **Target site:** Entre Ríos and Santa Fe provinces, Argentina, affected by late-season frosts in September and October 2024.
  
Here the [Drought and Heatwave script](./Script/frost.txt)

By combining these analyses, the scripts allow a **temporal visualization of extreme climatic events** on agricultural fields. EO Browser's time-lapse function highlights the evolution of heatwaves, droughts, and frost events, providing a **clear and visually compelling narrative** of climate impact on croplands.\[7\]\[8\]

These visualizations can support **decision-making for agricultural management**, disaster response, and long-term adaptation strategies, providing actionable insights for farmers, policymakers, and environmental agencies. \[9\] \[10\]

Here you can see satellite images and timelapses of the project: [satellite images](satellite%20images%20)

--------

## Drought and Heatwave Detection

### Concept

Drought and heatwaves are two interrelated phenomena that cause vegetation stress and soil moisture depletion.

By combining vegetation indices with surface temperature and water presence, the script visualizes **agricultural areas affected by heat
and dryness**.

### Satellite source

-   **Satellite:** Landsat 8-9 Level 1

-   **Instruments:** OLI (Optical Land Imager) and TIRS (Thermal Infrared Sensor)

-   **Spatial resolution:** 30 m

-   **Spectral bands used:**

| Band | Description                     | Unit                    | Purpose                          |
|------|----------------------------------|--------------------------|----------------------------------|
| B03  | Green (0.53–0.59 µm)             | Reflectance              | NDVI / NDWI calculation          |
| B04  | Red (0.64–0.67 µm)               | Reflectance              | NDVI calculation                 |
| B05  | Near Infrared (0.85–0.88 µm)     | Reflectance              | NDVI / NDWI                      |
| B09  | Cirrus (1.36–1.38 µm)            | Reflectance              | Cloud masking                    |
| B10  | Thermal Infrared (10.6–11.19 µm) | Brightness Temperature (K) | Surface temperature estimation |


### Processing logic

1.  **Cloud Masking**

Cirrus clouds are identified using **Band 9**. Pixels with B09 \> 0.01 are considered clouds and rendered in black.

The cloudiness of the timelapse was filtered by 30%.

2.  **Vegetation Index (NDVI)**

$$NDVI = \frac{B05 - B04}{B05 + B04} $$

Normalized between 0.1 and 0.8 to highlight vegetation vigor. Low NDVI indicates vegetation stress or bare soil.

3.  **Water Index (NDWI)**

$$NDWI = \frac{B03 - B05}{B03 + B05} $$

NDWI \> 0.1 identifies water bodies, which are rendered in blue to distinguish rivers or flooded zones.

4.  **Surface Temperature Proxy**

Band 10 provides **Brightness Temperature (BT)**, used as a proxy for land surface temperature.

The thermal signal is normalized between 290 K (≈17 °C) and 320 K (≈47 °C). Higher normalized temperature values correspond to **heatwave conditions**.

### Color Composition

-   **Red (R):** Normalized temperature, highlights heat stress

-   **Green (G):** NDVI, vegetation health

-   **Blue (B):** NDWI, water presence

### Visual interpretation

-   🟢 **Green:** Healthy vegetation

-   🔴 **Reddish tones:** Dry and hot areas (drought or heatwave)

-   🔵 **Blue:** Water bodies

-   ⚫ **Black:** Clouds

This combination enables temporal visualization in EO Browser time-lapse mode, allowing users to **observe the progression of droughts and heatwaves** across agricultural landscapes.

### Details of the script: Drought and Heatwave

In the following figures it is possible to observe the evolution of the region before and after the heatwave event in Argentina.

-   **Figure A (during the event, early January 2025):** After the heat wave, extreme temperatures (red/white), loss of vegetation cover (reduced green), and drought indicators are observed.

-   **Figure B (during/after the event, March 2025):** The region shows abundant vegetation and visible bodies of water, along with moderate temperatures (soft colors).

![2025-01-13-00_00_2025-01-13-23_59_Landsat_8-9_L1_Custom_script](https://github.com/user-attachments/assets/41b942c3-36d6-4e14-908f-4e39cfd961f8)
*Figure A. January 2025, Argentina (Santa Fe and Entre Rios Province)*

![2025-03-18-00_00_2025-03-18-23_59_Landsat_8-9_L1_Custom_script](https://github.com/user-attachments/assets/429ddb78-b23d-4fb4-b775-cc9c089b4a04)
*Figure B. March 2025, Argentina (Santa Fe and Entre Rios Province)*

![AWS_LOTL1-1257623640140761-timelapse](https://github.com/user-attachments/assets/010cffaa-a358-469a-85ae-34ff33dd2261)
<br> *Timelapse December and April 2025, Argentina (Santa Fe and Entre Rios Province 25 km resolution)*

Furthermore, the figures below show the evolution of drought in a lagoon called Mar Chiquita in Argentina last summer.

-   **Figure C (normal stage before the event, August 2024)**: The lagoon is at it normal extension, the region shows abundant vegetation and visible bodies of water, along with moderate temperatures (soft colours).

-   **Figure D (during the event, January 2025)**: At the peak of the drought and heatwave, the Mar Chiquita lagoon exhibits a marked reduction in surface area, extreme temperatures (red/white) and loss of vegetation cover (reduced green) on the fields surrounding it.

![2024-08-13-00_00_2024-08-13-23_59_Landsat_8-9_L1_Custom_script](https://github.com/user-attachments/assets/af4b572b-deaf-487d-b55f-6c65a047f9cc)
*Figure C. August 2024, Mar Chiquita, Argentina (Cordoba Province)*

![2025-01-12-00_00_2025-01-12-23_59_Landsat_8-9_L1_Custom_script](https://github.com/user-attachments/assets/7e6c9de2-d7fa-4171-b87c-118ef9e6bd5a)
*Figure D. January 2025, Mar Chiquita,Argentina (Cordoba Province)*

![AWS_LOTL1-379883988684818-timelapse](https://github.com/user-attachments/assets/f49d61bd-f300-422b-a72a-e2c15fad26ce)
<br> *Timelapse June 2024 to May 2025, Argentina (Mar Chiquita, 5 km resolution)*

![AWS_LOTL1-588973063144651-timelapse](https://github.com/user-attachments/assets/86dc93ec-60a9-47a6-a66d-a91f796f93a9)
<br> *Timelapse June 2024 to May 2025, Argentina (Mar Chiquita, 10 km resolution)*

--------

## Frost Detection

### Concept

Frost occurs when the land surface temperature drops below 0 °C. Frosts that develop outside the typical winter months are known as late-season frosts, and they are highly damaging to agriculture because they can kill young plants and tender buds, significantly affecting crop yields.

This script isolates **cold zones** while filtering out clouds to avoid confusion with cold cloud tops.

### Satellite source

-   **Satellite:** Landsat 8-9 Level 1

-   **Bands used:**

| Band      | Description      | Unit                    | Purpose                 |
|------------|------------------|--------------------------|--------------------------|
| **B03**    | Green             | Reflectance              | Cloud detection (NDGR)   |
| **B04**    | Red               | Reflectance              | NDGR / NDVI              |
| **B05**    | Near Infrared     | Reflectance              | NDVI                     |
| **B10**    | Thermal Infrared  | Brightness Temperature (K) | Frost detection        |
| **dataMask** | Valid pixel mask | —                        | Masking invalid regions  |


### Processing logic

1.  **Cloud Detection**

Uses both **spectral and thermal tests**:

-   NDGR = (B03 − B04) / (B03 + B04)

-   Brightness thresholds: B03, B04 \> 0.2

-   Thermal filter: very cold clouds B10 \< 265 K If any condition is met, the pixel is masked as cloud.

The cloudiness of the timelapse was filtered by 35%.

2.  **Vegetation Index (NDVI)**

Keeps natural green tones for cropland and vegetation under normal temperature.

3.  **Frost Detection**

Pixels where B10 \< 273 K (0 °C) and **no clouds** are detected are considered frost-affected.

4.  **Thermal Gradient**

Temperatures between **265 K (−8 °C)** and **273 K (0 °C)** are normalized.\
The colder the pixel, the **more violet-blue** it appears.

### Color Composition

-   **Green:** Vegetation

-   **Blue-Violet:** Frost / cold surfaces

-   **Black:** Clouds

### Visual interpretation

This visualization helps identify **localized frost events** and assess **potential agricultural damage**, separating cold land surfaces from high, cold clouds.

### Details of the script: Frost

In the following figures it is possible to observe the impact of a late frost registered in September/October 2024 in Argentina, when winter conditions unexpectedly extended into the beginning of the planting season.

-   **Figure E (reference image, September 2024):** vegetation shows signs of recovery after winter, represented in green tones, with no significant cold stress detected.

-   **Figure F (frost event, October 2024):** areas in blue tones indicate surface temperatures close to or below 0 °C, where frost occurred in croplands. The intensity of the blue scale highlights the most affected agricultural zones. This event represents a late frost that can damage early crops and delay the seasonal cycle.

![2024-09-16-00_00_2024-09-16-23_59_Landsat_8-9_L1_Custom_script](https://github.com/user-attachments/assets/c9953834-d01b-483e-850d-b59e30ec4d7d)
*Figure E. September 2024, Argentina (Santa Fe and Entre Rios Provinces)*

![2024-10-18-00_00_2024-10-18-23_59_Landsat_8-9_L1_Custom_script](https://github.com/user-attachments/assets/1b07845b-f5f8-41d2-b3ce-16c3e002e57c)
*Figure F. October 2024, Argentina (Santa Fe and Entre Rios Provinces)*

![AWS_LOTL1-1263704297926784-timelapse](https://github.com/user-attachments/assets/75b2ed2a-4dfe-4887-91e8-c0e683e1e6f3)
<br> *Timelapse September to November 2024, Argentina (Santa Fe and Entre Rios Province 25 km resolution)*

-----------

## Conclusion

The investigation, "Fields between drought, heat waves and frost: Observing changes in agriculture from space," was driven by a personal urgency rooted in the Argentine farming communities impacted by climate extremes, directly addressing the core mission of the "Through the Radar Looking Glass" challenge by turning satellite observations into a vital diagnostic tool. 

We developed two custom Landsat 8–9 scripts to reveal the physical drivers of climate stress: one quantifying the collapse in crop health caused by historic drought and heatwave conditions, and the other providing a critical time-series analysis of damaging late-season frost events. 

By transforming complex data into a clear visual narrative, the project delivers actionable insights for immediate disaster response and supports the long-term adaptation strategies essential for the resilience of the agricultural system.

We extend our heartfelt thanks to NASA and the Space Apps community for providing a platform where personal stories, scientific inquiry, and global collaboration converge. This challenge empowered us to turn data into impact and to honor the land and people who inspired this work. 

![WhatsApp Image 2025-10-05 at 11 20 00 PM](https://github.com/user-attachments/assets/02e1e5be-7924-4a29-b670-6f8c31619020)

----------------

## References

\[1\] Reuters, February 2025,
[https://www.reuters.com/markets/commodities/wilted-leaves-argentinas-farms-signal-bigger-hit-soy-corn-harvest-2025-02-03/](%20https://www.reuters.com/markets/commodities/wilted-leaves-argentinas-farms-signal-bigger-hit-soy-corn-harvest-2025-02-03/)

\[2\] Copernicus
<https://emergency.copernicus.eu/news/droughts-and-heatwaves-threaten-south-americas-water-resources-a-new-copernicus-report-shows/>

\[3\] NASA Earth Observatory, February 2025,
<https://earthobservatory.nasa.gov/images/154005/summer-heat-wave-in-south-america>

\[4\] Accuweather, Mar 2023,
<https://www.accuweather.com/en/weather-news/endless-brutal-heat-argentinas-late-season-heatwave-has-no-similarities-in-history/1498132>

\[5\] Therisk.global, September 2024,
<https://therisk.global/registry/early-frost-grips-central-and-southern-argentina-record-low-temperatures-reach-4c-in-rio-grande>

\[6\] TN, October 2024,
<https://tn.com.ar/campo/2024/10/04/heladas-tardias-impactaron-en-los-cultivos-de-las-principales-regiones-agropecuarias/>

\[7\] Sentinel Hub
<https://docs.sentinel-hub.com/api/latest/data/landsat-8/>

\[8\] USGS EROS Archive, March 2020,
<https://www.usgs.gov/centers/eros/science/usgs-eros-archive-landsat-archives-landsat-8-9-operational-land-imager-and>

\[9\] Thong- Cường- Phuong-Lam , May 2024, \[Analysis of urban heat
islands combining Sentinel 2 and Landsat 8 satellite images in Hochiminh
city\]
[https://www.researchgate.net/publication/381810500_Analysis_of_urban_heat_islands_combining_Sentinel_2\_and_Landsat_8\_
satellite_images_in_Hochiminh_city](https://www.researchgate.net/publication/381810500_Analysis_of_urban_heat_islands_combining_Sentinel_2_and_Landsat_8_%20satellite_images_in_Hochiminh_city)

\[10\] Onačillová- Gallay- Paluba- Péliová , August 2022, \[Combining
Landsat 8 and Sentinel-2 Data in Google Earth Engine to Derive Higher
Resolution Land Surface Temperature Maps in Urban Environment\]
<https://www.researchgate.net/publication/362844593_Combining_Landsat_8_and_Sentinel-2_Data_in_Google_Earth_Engine_to_Derive_Higher_Resolution_Land_Surface_Temperature_Maps_in_Urban_Environment>

\[11\] [Sentinel Hub EO
Browser](https://apps.sentinel-hub.com/eo-browser/)

------

## Author

**Bárbara Ángeles Ortiz** 

**Emanual Rebot** <br>

**Andrea Ortiz** 

![Status](https://img.shields.io/badge/status-finished-brightgreen) 📅 October 2025

## Acknowledgments

<img width="665" height="321" alt="image" src="https://github.com/user-attachments/assets/bb325b41-57ff-4a5e-9021-0a261bf65eb3" />

