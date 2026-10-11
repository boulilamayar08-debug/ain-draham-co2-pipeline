# Satellite-Based CO2 Absorption Estimation, Ain Draham (Kroumirie, NW Tunisia)

## Area
- Rectangle lon 8.62 to 8.78, lat 36.72 to 36.84, 18771 ha valid
- Evergreen cork oak and deciduous oak forest, with farmland and the town of Ain Draham

## Data sources
- Sentinel-2 L2A (COPERNICUS/S2_SR_HARMONIZED), SCL cloud mask, median seasonal composites
- ESA WorldCover v200 (10 m land cover)
- SRTM DEM (elevation, slope), 800 m split for the IPCC mountain zone
- GEDI L4B v2 (LARSE/GEDI/GEDI04_B_002, mean AGBD, 1 km, Apr 2019 to Aug 2021)

## Periods
- t1: 2020-06-01 to 2020-09-30
- t2: 2025-06-01 to 2025-09-30

## Method
- NDWI < 0 keeps land, water masked
- AGB = land cover lookup value x NDVI modifier (1 - 0.2 to 1 + 0.2)
- Carbon = AGB x 0.47
- CO2e = carbon x 44/12
- Sequestration = CO2e(t2) - CO2e(t1)

## Biomass lookup values (t d.m./ha)
- tree (10), below 800 m: 65.2 t d.m./ha, subtropical dry forest, Africa, IPCC 2019 Refinement Table 4.7 (Rozendaal et al. 2022, Environ. Res. Lett. 17:014047)
- tree (10), 800 m and above: 35.1 t d.m./ha, subtropical montane forest, Africa, same source, FAO GEZ mountain zone starts at about 800 m
- cropland (40): 10 t d.m./ha, IPCC default for annual cropland
- grass (30), wetland (90): 6.2 t d.m./ha, IPCC 2006 Table 6.4 value, climate zone not verified for this area
- shrub (20): 31.5 t d.m./ha, midpoint of 9 to 54 t/ha reported for maquis understorey in Kroumirie cork oak stands (Ann. For. Sci. 2001), units not verified
- built, bare, snow, water, mangrove, moss: set to 0

## GEDI comparison
- Pipeline mean AGB, 2020 composite: 53.5 t/ha
- GEDI L4B mean AGB: 62.3 t/ha
- Calibration multiplier: 1.164
- GEDI period matches t1 only, not t2

## Results (t CO2e, 5 years, 18771 ha)
- Lookup values as listed: net change 11933
- GEDI-calibrated: net change 13889

## Scope
- Above-ground biomass only, belowground biomass and soil carbon excluded
- No verified root ratios for these land classes

## Limitations
- No field plot validation
- IPCC defaults are continental averages by ecological zone, local cork oak stands can be much denser
- Land cover is fixed between periods, so change comes only from NDVI
- Net change depends directly on the NDVI modifier amplitude, see sensitivity_ndvi_modifier.csv
- The 800 m zone split is an approximation of the FAO ecological zone map
- Two summer composites only, drought, dieback, fire and seasonal differences can change NDVI without changing biomass
- Not compliant with registry MRV methodologies

## Outputs
- summary.csv
- sensitivity_multiplier.csv
- sensitivity_ndvi_modifier.csv
- sensitivity_forest_zone.csv
- stack_t1.tif, stack_t2.tif
