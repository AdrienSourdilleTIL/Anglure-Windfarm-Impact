# 🌬️ Anglure Windfarm Impact on Property Prices

## Overview
This project investigates the effect of the Anglure windfarm on nearby residential property prices in France. Using publicly available property transaction data (valeurs foncières), we apply a difference-in-differences (DiD) approach with spatial variation to isolate the impact of the windfarm's construction on the nearby housing market.

## 🎯 Objective
Estimate the **causal impact** of the wind farm on house prices in nearby communes using spatial and temporal property transaction data.

**Key question:**  
Does the construction of a windfarm negatively affect nearby property prices?

## 📍 Context
- **Wind farm location:** Anglure (51), France  
- **Coordinates:** 48.6424°N, 3.7871°E  
- **Commissioning date:** 2018-10-01  
- **Analysis window:** 2–3 years before and after construction

## 🗃️ Data Sources
- **Housing Transactions**  
  [DVF - Demande de Valeurs Foncières](https://www.data.gouv.fr/fr/datasets/demandes-de-valeurs-foncieres/)  
  Includes price, surface area, location, and date of transaction.

- **Commune Boundaries (Shapefiles)**  
  [INSEE Admin Express](https://www.insee.fr/fr/information/2114819)  
  Official shapefiles to identify and geolocate communes.

- **Wind Farm Coordinates**  
  Manually defined or sourced from public maps/satellite data:  
  `Latitude 48.6424°N, Longitude 3.7871°E`

---

## 🧪 Methodology
Constructed a panel dataset of property sales (2014–2024), geolocated transactions, and calculated distances from the windfarm. Compared properties near (treated) vs. far (control), before and after construction.

Regression model:

```python
model = smf.ols(
    "log_valeur_fonciere ~ post*treated + post*treated*distance_km + surface_reelle_bati + surface_terrain + C(type_local) + C(year) + C(code_postal)",
    data=df
).fit(cov_type='cluster', cov_kwds={'groups': df['code_commune']})
```
- **Dependent variable:** Log of sale price  
- **Treatment:** Properties near windfarm, post-construction  
- **Controls:** Property size, land size, property type, year, postal code  
- **Errors clustered by:** Commune


## Results
- `post:treated` coefficient: –2.17 (p < 0.001) → Significant price drop post-construction near windfarm  
- `post:treated:distance_km` coefficient: +0.82 (p < 0.001) → Impact lessens with distance  
- Effect is strongly localized, proximity drives price decline

## Conclusion
Strong evidence that the windfarm's construction negatively impacted nearby property values, with the effect fading over distance—likely due to localized nuisances like noise and visual impact.

---

## 👤 Author
Adrien Sourdille — Data engineer interested in energy infrastructure, economics, and spatial analysis.

---

## 📜 License
MIT License. See `LICENSE` file for details.

---

## 🛠️ Environment (optional)
- Python 3.10+  
- Libraries: `pandas`, `geopandas`, `shapely`, `scikit-learn`, `statsmodels`, `matplotlib`, `seaborn`

Install dependencies with:  
```bash
pip install -r requirements.txt
