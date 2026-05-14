# raster-digital-divide

Territorial Digital Divide: Geospatial Raster Analysis — Cusco Region, Peru.

## Project Description

This project measures the **territorial digital divide** in the Cusco region of Peru by cross-referencing two satellite-derived raster datasets:

- **NASA Black Marble nighttime lights (VNL 2025)** — proxy for urbanization and population density.
- **OSIPTEL mobile coverage kernel (2019, 50 m)** — proxy for internet access.

The pipeline reprojects, aligns, normalizes and combines both layers to produce thematic maps (Digital Divide Index, Total Digital Exclusion, Intervention Priority, Social Exclusion Risk) and a 2×2 territorial classification that exposes inequality patterns between connected urban zones and digitally excluded rural areas.

### Research Question

> Which territories in the Cusco region present the largest mismatch between urbanization (nighttime light) and mobile connectivity, and where should public intervention be prioritized to reduce the digital divide?

## Repository Structure

```
raster-digital-divide/
├── data/                              # input rasters (not tracked by git)
│   ├── VNL_cusco_2025.tif
│   └── kernel_cobmovil2019_50m.tif
├── notebooks/
│   └── digital_divide_cusco.ipynb     # main analysis notebook
├── output/                            # generated artifacts
├── README.md
└── requirements.txt
```

## Dependencies & Installation

Python 3.10+ is required. Install dependencies with:

```bash
pip install -r requirements.txt
```

Required packages (pinned in `requirements.txt`):

- `rasterio`
- `numpy`
- `matplotlib`
- `scipy`
- `seaborn`
- `pandas`

## How to Run

1. **Download the input data** from the Google Drive folder provided in the task description and place the two `.tif` files inside `data/`:
   - `VNL_cusco_2025.tif`
   - `kernel_cobmovil2019_50m.tif`
2. **Install dependencies** as shown above.
3. **Open and run the notebook end-to-end**:

   ```bash
   jupyter notebook notebooks/digital_divide_cusco.ipynb
   ```

   Execute every cell in order from Step 0 (environment setup) through Step 10 (export). The notebook generates all GeoTIFFs and the dashboard automatically inside the `output/` folder.

## Output Files

| File | Description |
|---|---|
| `output/vnl_norm.tif` | Normalized VNL nighttime lights (P2–P98, scaled to [0, 1]). |
| `output/conn_norm.tif` | Normalized mobile coverage, aligned to the VNL grid. |
| `output/ibd_brecha_digital.tif` | Digital Divide Index = `VNL_norm − Conn_norm`, range [−1, 1]. |
| `output/clasificacion_brecha.tif` | 4-class territorial classification (1=Urban Connected, 2=Urban Divide, 3=Rural Connected, 4=Critical Divide). |
| `output/dashboard_brecha_digital.png` | Composite dashboard figure (3×3 grid) at 150 dpi. |

## Main Findings

The Cusco region is overwhelmingly classified as **Critical Divide** (~90% of pixels lack both nighttime light and mobile coverage), highlighting an entrenched digital exclusion concentrated in the rural Andes and high jungle. Urban centers (Cusco city and the Sacred Valley corridor) account for a small share of the territory but show the highest mismatch between population density and connectivity, identifying them as primary candidates for telecommunications investment. The Welch's t-test confirms a statistically significant difference in VNL between Urban Connected and Critical Divide classes (large effect size), validating the binary territorial split as a meaningful policy tool.
