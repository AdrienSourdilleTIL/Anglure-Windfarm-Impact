# 🌬️ Impact of the Saint-Vincent-des-Landes Wind Farm on House Prices

This project investigates how the installation of the wind farm in Saint-Vincent-des-Landes (Loire-Atlantique, France) has affected surrounding residential property prices.

## 🎯 Objective

To estimate the **causal impact** of the wind farm on house prices in nearby communes using spatial and temporal property transaction data.

---

## 📍 Context

- **Wind farm location**: Saint-Vincent-des-Landes, Loire-Atlantique (44), France  
- **Coordinates**: Approx. 47.6670°N, -1.3170°E  
- **Commissioning date**: *(insert exact commissioning date once confirmed)*  
- **Analysis window**: 2–3 years before and after commissioning

---

## 📂 Project Structure


---

## 🗃️ Data Sources

- **Housing Transactions**  
  [DVF - Demande de Valeurs Foncières](https://www.data.gouv.fr/fr/datasets/demandes-de-valeurs-foncieres/)  
  Property sales data including price, surface area, location, and date of transaction.

- **Commune Boundaries (Shapefiles)**  
  [INSEE Admin Express](https://www.insee.fr/fr/information/2114819)  
  Official shapefiles to identify and geolocate communes.

- **Geographic Coordinates of Wind Farm**  
  Manually defined or sourced from public maps/satellite data. Approximate location:  
  `Latitude 47.6670° N, Longitude -1.3170° E`

---

## ⚙️ Methodology Overview

1. **Filter** DVF data for relevant years (e.g. 2018–2022).
2. **Select communes** within a 30 km radius of the wind farm as the treatment group.
3. Use surrounding communes (30–60 km away) as a control group.
4. **Aggregate** price per square meter by commune and year.
5. Estimate causal effects using a **difference-in-differences** (DiD) model.

---

## 🧪 Causal Strategy

The core model:

price_per_m2_it = α + β * treated_post_it + γ * treated_i + δ * post_t + X_it + ε_it


Where:
- `treated_post_it` = 1 if commune is within 30 km and after wind farm launch
- `treated_i` = 1 for treatment communes
- `post_t` = 1 for post-treatment period
- `X_it` = optional controls (e.g. income, population)
- `β` captures the effect of the wind farm on property prices

---

## ✅ Project Status

- ✅ DVF data collected (2018–2022)
- 🔲 Filter communes by distance from wind farm
- 🔲 Clean and join datasets
- 🔲 Run DiD model
- 🔲 Visualize results

---

## 👤 Author

Adrien — Data engineer interested in the intersection of energy infrastructure, economics, and spatial analysis.

---

## 📜 License

MIT License. See `LICENSE` file for details.

---

## 🛠️ Environment (optional)

- Python 3.10+
- `pandas`, `geopandas`, `shapely`, `scikit-learn`, `statsmodels`, `matplotlib`, `seaborn`

To install dependencies:
```bash
pip install -r requirements.txt


