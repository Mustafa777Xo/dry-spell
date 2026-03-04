# Climate Feature Documentation

This document describes the climate and hydrological variables used to model dry-spell risk during the July–October rainy season.

The dataset integrates local land-surface variables, atmospheric conditions, regional hydrology indicators, and large-scale ocean climate drivers to represent the multi-layered physical system governing rainfall breaks and crop stress.

⸻

## Dataset Structure

All feature files are time-indexed (daily resolution).
During preprocessing, datasets are merged on the date field to form a unified modeling table.

Training period: 2002–2019
Evaluation period: 2020–2025 (held-out)

Each row represents a single day within the July–October seasonal window.

⸻

## Feature Categories

The features are organized into five physical layers:
	1.	Local Soil Water State
	2.	Atmospheric Moisture & Heat Stress
	3.	Atmospheric Stability & Circulation
	4.	Regional Hydrology
	5.	Large-Scale Ocean Climate Drivers

This layered structure reflects the physical processes underlying dry-spell formation.

⸻

### 1. Local Soil Water State

> 5cm Soil Moisture (CFS)

**Definition**
Volumetric soil moisture in the top ~5 cm of soil.

**Units**
Fraction (0–1), representing percentage of soil volume occupied by water.

**Physical Interpretation**
Represents immediate crop water availability in the seed and shallow root zone.
Declining values indicate increasing plant stress and vulnerability to rainfall gaps.

**Role in Dry-Spell Modeling**
Encodes short-term hydrological memory and surface drying trends.

⸻

### 2. Atmospheric Moisture & Heat Stress

2m Temperature (temp_trimmed)

Definition
Daily mean air temperature at 2 meters above the surface.

Units
Degrees Celsius (°C)

Interpretation
Represents sustained thermal exposure influencing evaporation and plant stress.

⸻

Maximum Surface Temperature (ERA5)

Definition
Daily maximum near-surface temperature.

Units
Degrees Celsius (°C)

Interpretation
Captures peak heat stress events that accelerate soil moisture loss.

⸻

Mean Dew Point Temperature

Definition
Temperature at which air becomes saturated.

Units
Degrees Celsius (°C)

Interpretation
Higher values indicate moist air; lower values indicate dry air.

Relevance
Lower dew point increases evaporation demand and drying potential.

⸻

Vapour Pressure Deficit (VPD)

Definition
Difference between saturation vapor pressure and actual vapor pressure.

Units
kPa

Interpretation
Measures atmospheric demand for moisture (“atmospheric thirst”).

Higher VPD → stronger evaporation stress.

Relevance
Direct indicator of evapotranspiration stress and drought intensity.

⸻

3. Atmospheric Stability & Circulation

Sea-Level Pressure (ERA5)

Definition
Atmospheric pressure adjusted to sea level.

Units
kPa (or equivalent)

Interpretation
Represents large-scale synoptic systems.

Persistent high pressure suppresses rainfall and promotes dry conditions.

⸻

Surface Pressure (ERA5)

Definition
Atmospheric pressure at actual surface elevation.

Units
kPa

Interpretation
Reflects local atmospheric stability and complements sea-level pressure.

⸻

u10 (10m Zonal Wind)

Definition
East–West wind component at 10 meters above ground.

Units
m/s

Interpretation
Represents horizontal moisture transport and circulation patterns.

Persistent anomalies may indicate altered moisture inflow and rainfall suppression.

Note: Spatially gridded data were aggregated to daily regional averages during preprocessing.

⸻

4. Regional Hydrology

Sudd Water Deficit

Definition
Hydrological deficit indicator associated with the Sudd wetland region (Nile Basin).

Interpretation
Represents basin-scale moisture storage and hydrological memory.

Higher deficit values indicate reduced regional water availability and lower resilience to rainfall gaps.

Relevance
Adds medium-scale hydrological context beyond local soil moisture.

⸻

5. Large-Scale Ocean Climate Drivers

SST – Cameroon Region (Atlantic)

Definition
Sea Surface Temperature in a defined Atlantic region near Cameroon.

Units
Degrees Celsius (°C)

Interpretation
Influences West African monsoon strength and moisture transport patterns.

Represents seasonal-scale climate forcing.

⸻

SST – Indian Ocean

Definition
Sea Surface Temperature in a defined Indian Ocean region.

Units
Degrees Celsius (°C)

Interpretation
Major driver of East African rainfall variability and monsoon circulation.

Encodes interannual climate variability affecting dry-spell frequency.

⸻

Multi-Scale Climate Representation

The feature set captures interacting layers of the climate system:

Fast Daily Stress Signals
	•	Soil moisture
	•	Temperature
	•	Dew point
	•	VPD

Weather Regime Indicators
	•	Sea-level pressure
	•	Surface pressure
	•	Wind

Regional Hydrology
	•	Sudd water deficit

Climate-Scale Forcing
	•	Atlantic SST
	•	Indian Ocean SST

Dry spells emerge when stress conditions align and persist across these layers.

⸻

Modeling Perspective

This feature design:
	•	Integrates land, atmosphere, hydrology, and ocean drivers
	•	Captures both short-term stress and seasonal climate context
	•	Reflects physically grounded drought formation mechanisms

The dataset enables modeling dry spells as a system-level interaction rather than a single-variable threshold event.