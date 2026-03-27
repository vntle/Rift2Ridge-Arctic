# Arctic Setup

This page describes the Arctic-specific model configurations and case studies included in this repository.

## Tectonic Context

The Arctic Ocean contains two major oceanic basins:

| Basin | Age | Spreading ridge | Half-rate |
|---|---|---|---|
| Eurasia Basin | ~56 Ma – present | Gakkel Ridge | 6–13 mm/yr |
| Amerasia Basin | ~130 Ma (debated) | Extinct ridge | — |

The **Gakkel Ridge** is the slowest-spreading mid-ocean ridge on Earth. Its crust is anomalously thin and locally amagmatic, making it an ideal natural laboratory for studying the limits of seafloor spreading.

## Available Case Studies

### 1. Gakkel Ridge Initiation (`ARCTIC/gakkel01`)

Simulates the transition from continental rifting to ultra-slow seafloor spreading in the Eurasia Basin.

**Key parameters:**

| Parameter | Value |
|---|---|
| Half-spreading rate | 6 mm/yr |
| Mantle potential temperature | 1270 °C |
| Initial crustal thickness | 35 km |
| Simulation duration | 60 Myr |
| Mesh resolution | 500 m (near ridge) |

**Scientific focus:** Onset of melt extraction, thinning of the sub-continental lithospheric mantle, and crustal accretion patterns at ultra-slow rates.

### 2. Western Gakkel Amagmatic Segment (`ARCTIC/gakkel_amag`)

Tests conditions for **amagmatic spreading** — where lithospheric extension occurs entirely by brittle faulting with no melt reaching the surface.

**Key parameters:**

| Parameter | Value |
|---|---|
| Half-spreading rate | 6 mm/yr |
| Mantle potential temperature | 1250 °C |
| Melt extraction threshold | 2% |

**Scientific focus:** Role of mantle temperature and spreading rate in switching between magmatic and amagmatic spreading modes.

### 3. Eurasia Basin Subsidence (`ARCTIC/eurasia_subsidence`)

Examines how sediment loading and isostatic adjustment control bathymetry in a young Arctic basin.

**Key parameters:**

| Parameter | Value |
|---|---|
| Sediment density | 2000 kg/m³ |
| Sedimentation rate | 50 m/Myr |
| Water depth (initial) | 2500 m |

**Scientific focus:** Sediment–tectonics feedback and its effect on thermal subsidence curves.

## Setting Up a New Arctic Case

1. Create a new input folder:

   ```bash
   mkdir -p $dsnmod/data/ARCTIC/<event>/<meshnam>/001
   ```

2. Copy the nearest existing case as a template:

   ```bash
   cp -r $dsnmod/data/ARCTIC/gakkel01/ucr500/001/* \
         $dsnmod/data/ARCTIC/<event>/<meshnam>/001/
   ```

3. Edit `call_main.m` to set the correct `region`, `event`, `meshnam`, and `nnn`.

4. Adjust physical parameters in `change_model.m` for your scenario.

5. Set the COMPSET in `readCASE.m` (e.g., enable melt if needed).

6. Run the simulation (see [Usage](usage.md)).

## Arctic-Specific Considerations

### Cold Mantle

The Arctic mantle is cooler than typical mid-ocean ridges. Use a lower `T_mantle` (1250–1280 °C) and verify that the solidus parameterisation is appropriate for depleted harzburgite.

### Thick Sediment Cover

The Lomonosov Ridge and surrounding shelves have thick Cenozoic sediment sequences. Enable sediment loading if modelling subsidence:

```matlab
% change_model.m
p.sed_load = true;
p.rho_sed  = 2000;    % sediment density [kg/m³]
p.sed_rate = 50e-3;   % sedimentation rate [km/Myr]
```

### Ice Loading

For Pleistocene scenarios, glacial isostatic adjustment (GIA) can be relevant. Ice loading is not yet implemented in this version; refer to the [FAQ](faq.md) for current limitations.

### Ultra-Slow Spreading Numerics

At very low spreading rates (< 8 mm/yr half-rate), explicit time stepping can become numerically stiff. Consider:

- Increasing `eta_min` slightly (e.g., to 5×10¹⁸ Pa·s).
- Using a smaller initial time step and allowing adaptive stepping.
- Checking the CFL condition in the log file.
