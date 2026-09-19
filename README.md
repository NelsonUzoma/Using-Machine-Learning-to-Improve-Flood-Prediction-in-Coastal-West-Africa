# CoastGuard AI

**Flood Indicative Neural Network (FINN): AI-powered flood prediction and early warning for coastal West Africa**

CoastGuard is a flood early-warning platform for vulnerable coastal communities. FINN is the prediction engine inside it. CoastGuard turns FINN's outputs into clear risk levels, explanations and alerts that communities, emergency responders and local decision-makers can act on before a flood becomes a disaster.

**Live prototype:** https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/

> **Status: research prototype.** The interactive demo uses synthetic data, and its risk score comes from a transparent weighted formula standing in for the trained FINN model. It is not a real forecast and must not be used for real emergency decisions. See [Current status](#current-status) for exactly what is real and what is simulated.

---

## Overview

Flooding is a major environmental and humanitarian challenge in coastal West Africa. Rapid urbanization, climate change and limited infrastructure have increased the frequency and severity of flood events in cities such as Lagos, Accra and Cotonou.

Traditional forecasting relies on hydrological monitoring networks that are sparse in the region. CoastGuard investigates how machine learning can combine several environmental signals to estimate flood risk earlier and at a more local level, and, just as importantly, how to present that risk in a form people can understand and act on.

Initial development focuses on vulnerable coastal areas of **Nigeria and Ghana**.

## What CoastGuard does

1. **Ingests environmental data:** rainfall, river discharge and water levels, elevation, soil moisture, land use, distance to the coast, satellite observations and historical flood records.
2. **Predicts flood risk (FINN):** estimates flood likelihood for each location and time step.
3. **Explains the prediction:** shows which environmental factors contributed most to the risk score.
4. **Translates it into action:** maps scores to four levels with plain-language guidance.
5. **Delivers alerts:** SMS-style messages and dashboard warnings, with local-language alerts planned.

### Risk levels

| Level | Flood likelihood | Guidance |
|---|---|---|
| Low | under 25% | No action needed. Keep drains clear. |
| Moderate | 25% to 50% | Stay alert, clear drains, know your nearest higher ground. |
| High | 50% to 75% | Prepare now. Move valuables up, charge phones, avoid low roads. |
| Critical | over 75% | Move to higher ground or a shelter. Never cross floodwater. |

## The interactive prototype

Open `index.html` (or the live link above). It has three sections:

- **Outlook:** a map of seven coastal locations (Takoradi, Accra, Keta, Lagos, Warri, Port Harcourt, Calabar) with a 72-hour timeline. Four weather situations are included: an ordinary day, heavy rainfall, storm surge on a spring tide, and a disastrous flood. As risk crosses High and Critical, the prototype triggers a simulated emergency alert with a banner, siren, vibration and an alert log.
- **Try FINN:** a demo mode where you enter rainfall, river level, soil moisture, elevation, distance to coast, land cover and tide, and get an instant risk level with an explanation.
- **How it works:** the pipeline, candidate data sources, known limits and next steps.

Alert text is available in English and a Nigerian Pidgin preview. Further African languages are planned and should be reviewed by native speakers.

## Current status

| Real in this repository | Simulated in the prototype |
|---|---|
| Research framing and methodology | All rainfall, river, soil and tide values (synthetic scenarios) |
| Dashboard, map, timeline and risk-level design | The risk score (a weighted formula standing in for trained FINN) |
| Explanation and alert-writing logic | Location values such as elevation (illustrative, not measured) |
| Demo mode for entering conditions | Alert delivery and subscriber counts |

## Repository contents

```
index.html                              Interactive prototype (single file, no build step)
Flood_Prediction_West_Africa.pdf        Research paper: motivation, proposed methods, expected outcomes
code/flood_prediction_model.py          Example script showing how environmental variables could train a flood model
data/sample_dataset_description.txt     Description of the datasets the research requires
README.md                               This file
```

## Methodology (planned)

- **Data:** candidate sources to evaluate and validate for the region include CHIRPS and GPM IMERG (rainfall), GloFAS (river discharge), Copernicus DEM or SRTM (elevation), SMAP or ESA CCI (soil moisture), ESA WorldCover (land cover), Sentinel-1 (flood extent), and national agency and Dartmouth Flood Observatory records for flood history.
- **Baselines first:** Random Forest, XGBoost and LightGBM models are trained before any neural network.
- **FINN:** a neural network is adopted as the FINN engine only if it outperforms the simpler baselines. If it does not, CoastGuard stays the platform name and FINN refers to whichever model performs best.
- **Evaluation:** validated against historical flood events, with metrics suited to rare events (precision, recall, false-alarm rate and lead time), not accuracy alone.
- **Explainability:** feature-contribution methods such as SHAP so every alert can say why it was raised.

## Limitations

- River gauge coverage and historical flood records in the region are sparse and patchy.
- Floods are rare events, so training data is heavily imbalanced.
- Predictions need validation with local agencies such as NEMA and NADMO and with community partners before anyone relies on them.
- Alerts in local languages need review by native speakers.

## Roadmap

- [x] Interactive prototype with simulated scenarios and alert flow
- [ ] Collect and clean real rainfall, elevation, soil moisture and flood-history data for pilot areas
- [ ] Train and compare baseline models, then a neural network
- [ ] Report honest, reproducible performance metrics
- [ ] Rebuild the interface in Streamlit with Folium maps using real model output
- [ ] Add local-language alerts (for example Twi, Ga, Ewe, Yoruba, Hausa)
- [ ] Pilot with local stakeholders

## Tech stack

Python, Pandas, NumPy, scikit-learn, XGBoost, LightGBM, Matplotlib, Seaborn, Jupyter Notebook, GeoPandas, Rasterio, Folium, Streamlit, Git and GitHub. The current prototype is plain HTML, CSS and JavaScript.

## Motivation

Flood events in coastal West Africa often cause severe economic damage and displace communities. Machine learning can integrate multiple environmental signals and find patterns that conventional models miss, but only if it is built around African data conditions and delivered in a form communities can use. CoastGuard aims to show that locally relevant, accessible climate-resilience tools are practical.

## Author

**Nelson Uzoma**, Nigeria

Early-Career researcher and engineer working across AI/ML research, frontier AI safety and alignment, technical governance and AI/ML engineering. African Maths Ambassador, American Honor Society member, and incoming Computer Science student at Howard University.

CoastGuard AI grows out of an independent research project, *Using Machine Learning to Improve Flood Prediction in Coastal West Africa*, and was developed for the Hack-AI-Thon.

LinkedIn: <https://www.linkedin.com/in/nelson-uzoma-659266421?>

## Disclaimer

CoastGuard AI is a research and demonstration project. The prototype's numbers, forecasts and alerts are simulated. Do not use it to make real flood-safety decisions. For real warnings, follow your national and local emergency agencies.
