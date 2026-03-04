# Climate Feature Documentation

This document describes the climate and hydrological variables used to model dry-spell risk during the July-Oct rainy season.

The dataset integrates local land-surface variables, atmospheric conditions, regional hydrology indicators, and large-scale ocean climate drivers to represent the multi-layered physical system governing rainfall breaks and crop stress.

## Data Access (Large Files)

The raw CSVs are large (about 574 MB total) and exceed GitHub size limits. Download them from the shared Google Drive folder:

https://drive.google.com/drive/folders/1WqydluPCwG4Dv-HrhBdy1s0nqQU3JQip?usp=drive_link

Expected local layout (ignored by git):

```
data/
  raw/
    train/
    test/
```

## Dataset Structure

- All feature files are time-indexed (daily resolution).
- During preprocessing, datasets are merged on the date field to form a unified modeling table.
- Training period: 2002-2019
- Evaluation period: 2020-2025 (held out)
- Each row represents a single day within the July-Oct seasonal window.

## Feature Categories

The features are organized into five physical layers:

1. Local soil water state
2. Atmospheric moisture and heat stress
3. Atmospheric stability and circulation
4. Regional hydrology
5. Large-scale ocean climate drivers

This layered structure reflects the physical processes underlying dry-spell formation.

## 1. Local Soil Water State

### 5cm Soil Moisture (CFS)

- Definition: Volumetric soil moisture in the top ~5 cm of soil.
- Units: Fraction (0-1), representing percentage of soil volume occupied by water.
- Physical interpretation: Represents immediate crop water availability in the seed and shallow root zone. Declining values indicate increasing plant stress and vulnerability to rainfall gaps.
- Role in dry-spell modeling: Encodes short-term hydrological memory and surface drying trends.

## 2. Atmospheric Moisture and Heat Stress

### 2m Temperature (temp_trimmed)

- Definition: Daily mean air temperature at 2 meters above the surface.
- Units: C
- Interpretation: Represents sustained thermal exposure influencing evaporation and plant stress.

### Maximum Surface Temperature (ERA5)

- Definition: Daily maximum near-surface temperature.
- Units: C
- Interpretation: Captures peak heat stress events that accelerate soil moisture loss.

### Mean Dew Point Temperature

- Definition: Temperature at which air becomes saturated.
- Units: C
- Interpretation: Higher values indicate moist air; lower values indicate dry air.
- Relevance: Lower dew point increases evaporation demand and drying potential.

### Vapour Pressure Deficit (VPD)

- Definition: Difference between saturation vapor pressure and actual vapor pressure.
- Units: kPa
- Interpretation: Measures atmospheric demand for moisture (atmospheric thirst). Higher VPD means stronger evaporation stress.
- Relevance: Direct indicator of evapotranspiration stress and drought intensity.

## 3. Atmospheric Stability and Circulation

### Sea-Level Pressure (ERA5)

- Definition: Atmospheric pressure adjusted to sea level.
- Units: kPa (or equivalent).
- Interpretation: Represents large-scale synoptic systems. Persistent high pressure suppresses rainfall and promotes dry conditions.

### Surface Pressure (ERA5)

- Definition: Atmospheric pressure at actual surface elevation.
- Units: kPa
- Interpretation: Reflects local atmospheric stability and complements sea-level pressure.

### u10 (10m Zonal Wind)

- Definition: East-west wind component at 10 meters above ground.
- Units: m/s
- Interpretation: Represents horizontal moisture transport and circulation patterns. Persistent anomalies may indicate altered moisture inflow and rainfall suppression.
- Note: Spatially gridded data were aggregated to daily regional averages during preprocessing.

## 4. Regional Hydrology

### Sudd Water Deficit

- Definition: Hydrological deficit indicator associated with the Sudd wetland region (Nile Basin).
- Interpretation: Represents basin-scale moisture storage and hydrological memory.
- Relevance: Higher deficit values indicate reduced regional water availability and lower resilience to rainfall gaps. Adds medium-scale hydrological context beyond local soil moisture.

## 5. Large-Scale Ocean Climate Drivers

### SST - Cameroon Region (Atlantic)

- Definition: Sea surface temperature in a defined Atlantic region near Cameroon.
- Units: C
- Interpretation: Influences West African monsoon strength and moisture transport patterns. Represents seasonal-scale climate forcing.

### SST - Indian Ocean

- Definition: Sea surface temperature in a defined Indian Ocean region.
- Units: C
- Interpretation: Major driver of East African rainfall variability and monsoon circulation. Encodes interannual climate variability affecting dry-spell frequency.

## Multi-Scale Climate Representation

The feature set captures interacting layers of the climate system:

- Fast daily stress signals: soil moisture, temperature, dew point, VPD
- Weather regime indicators: sea-level pressure, surface pressure, wind
- Regional hydrology: Sudd water deficit
- Climate-scale forcing: Atlantic SST, Indian Ocean SST

Dry spells emerge when stress conditions align and persist across these layers.

## Modeling Perspective

This feature design:

- Integrates land, atmosphere, hydrology, and ocean drivers
- Captures both short-term stress and seasonal climate context
- Reflects physically grounded drought formation mechanisms

The dataset enables modeling dry spells as a system-level interaction rather than a single-variable threshold event.
