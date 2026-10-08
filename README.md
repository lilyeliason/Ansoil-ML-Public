# Modeling Soil Geochemical Variability Across Antarctic Ice-Free Regions Using Machine Learning
 
**Lily K. Eliason¹, Rob Ferguson¹, Byron Adams², Noah Fierer³, Joshua J. LeMonte¹**
 
¹ Brigham Young University, Department of Geological Sciences
² Brigham Young University, Department of Biology
³ University of Colorado Boulder

 --
 
**Can machine learning predict soil chemistry in places no one has sampled?**
 
We paired 171 lab-analyzed soil samples from 28 locations with environmental data available across the continent, then trained Random Forest and XGBoost models to predict 67 geochemical targets at 15,769 ice-free grid cells.
 
## Key findings
 
- Random Forest and XGBoost outperform earlier MLR and KNN models.
- 18 of 67 properties reach R² ≥ 0.30 (XGBoost, native units). δ¹⁵N predicts best (R² 0.660).
- Mineral-bound (acid digest) elements predict far better than their water-soluble forms.
- 22.7% of ice-free terrain falls outside the training range and is left unmapped. These areas, especially the NW Antarctic Peninsula and North Victoria Land, are the top sampling priorities.

## Data
 
**Soil geochemistry.** Lab-analyzed soil samples are available through the Environmental Data Initiative: https://portal.edirepository.org/nis/mapbrowse?packageid=knb-lter-mcm.275.1
 
Dragone, N.B., M.K. Childress, C. VanderBurgh, I.D. Hogg, L.G. Sancho, C.K. Lee, J.E. Barrett, B.J. Adams, J.J. LeMonte, R. Willmore, C.A. Quandt, and N. Fierer. 2025. Geochemical, physicochemical, and genomic data from a continental-scale survey of microbial diversity in Antarctic soils (2003-2023) ver 1. Environmental Data Initiative. https://doi.org/10.6073/pasta/b4858653c587864f0111aba4c3014d61 (Accessed 2026-10-02).
 
**Environmental predictors.** Nine predictor variables, encoded as 22 model features:
 
| Group | Variables | Source |
|---|---|---|
| Geographic | Projected coordinates (EPSG:3031), region, distance to coast |
| Topographic | Elevation, slope, aspect (sin/cos encoded) |
| Climatic | Mean annual temperature, precipitation |
| Geological | Lithology (9 classes, one-hot encoded) |
 
## Methods
 
- **Models:** Multilinear Regression (previous), K-nearest neighbors (previous), Random Forest, and XGBoost.
- **Validation:** Leave-one-location-out cross-validation (LOLO-CV). Each of the 28 locations is held out in turn, so every score reflects prediction at a site the model never saw.¹
- **Reproducibility:** Random Forest and XGBoost are each run across five random seeds; results are reported as mean ± SD.
- **Tuning:** Hyperparameters were selected by randomized search on the same LOLO folds (Random Forest: 54 draws from a fixed grid; XGBoost: 500 random draws). n_estimators is tuned directly; no early stopping on held-out data.
- **Transforms:** Trace metals use log1p, selected dissolved ions use natural log, and leachate composition uses centered log-ratio (CLR). All R² values on the poster are reported in native measurement units.
- **Mapping:** Grid cells outside the training range of any covariate are left unmapped rather than extrapolated.
## Code availability
 
Code will be made available upon publication. 

## References

1. Meyer, H., Reudenbach, C., Hengl, T., Katurji, M., and Nauss, T., 2018, Improving performance of spatio-temporal machine learning models using forward feature selection and target-oriented validation: Environmental Modelling & Software, v. 101, p. 1–9, https://doi.org/10.1016/j.envsoft.2017.12.001.
2. Willmore, Rachel, "Geochemical Characterization and Predictive Soil Mapping of Ice-Free Regions in Antarctica" (2024). Theses and Dissertations. 11070. https://scholarsarchive.byu.edu/etd/11070
3. Siqueira, R.G., Moquedace, C.M., Fernandes-Filho, E.I., Francelino, M.R., and Schaefer, C.E.G.R., 2024, Modelling and prediction of major soil chemical properties with Random Forest: Machine learning as tool to understand soil-environment relationships in Antarctica: Catena, v. 235, 107677, https://doi.org/10.1016/j.catena.2023.107677.
4. Siqueira, R.G., Moquedace, C.M., Francelino, M.R., Schaefer, C.E.G.R., and Fernandes-Filho, E.I., 2023, Machine learning applied for Antarctic soil mapping: Spatial prediction of soil texture: Geoderma, v. 432, 116405, https://doi.org/10.1016/j.geoderma.2023.116405.
5. McBratney, A.B., Mendonça Santos, M.L., and Minasny, B., 2003, On digital soil mapping: Geoderma, v. 117, p. 3–52, https://doi.org/10.1016/S0016-7061(03)00223-4.
6. Bower, D.M., et al., 2021, Geochemical zones and environmental gradients for soils from the central Transantarctic Mountains, Antarctica: Biogeosciences, v. 18, p. 1629–1644, https://doi.org/10.5194/bg-18-1629-2021.
7. Breiman, L., 2001, Random forests: Machine Learning, v. 45, p. 5–32, https://doi.org/10.1023/A:1010933404324.
8. Chen, T., and Guestrin, C., 2016, XGBoost: A scalable tree boosting system: Proceedings of the 22nd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, p. 785–794, https://doi.org/10.1145/2939672.2939785.
9. Buccianti, A., and Grunsky, E., 2014, Compositional data analysis in geochemistry: Journal of Geochemical Exploration, v. 141, p. 1–5, https://doi.org/10.1016/j.gexplo.2014.03.022.
10. Dragone, N.B., M.K. Childress, C. VanderBurgh, I.D. Hogg, L.G. Sancho, C.K. Lee, J.E. Barrett, B.J. Adams, J.J. LeMonte, R. Willmore, C.A. Quandt, and N. Fierer. 2025. Geochemical, physicochemical, and genomic data from a continental-scale survey of microbial diversity in Antarctic soils (2003-2023) ver 1. Environmental Data Initiative. https://doi.org/10.6073/pasta/b4858653c587864f0111aba4c3014d61 (Accessed 2026-10-02).
11. Matsuoka, K., Skoglund, A., Roth, G., et al., 2021, Quantarctica, an integrated mapping environment for Antarctica, the Southern Ocean, and sub-Antarctic islands: Environmental Modelling & Software, v. 140, 105015, https://doi.org/10.1016/j.envsoft.2021.105015.
12. Howat, I.M., Porter, C., Smith, B.E., Noh, M.-J., and Morin, P., 2019, The Reference Elevation Model of Antarctica: The Cryosphere, v. 13, p. 665–674, https://doi.org/10.5194/tc-13-665-2019.


## Image credits
 
- Figure 1: Shackleton Glacier, photo by Byron Adams.
- Map basemaps: Reference Elevation Model of Antarctica (REMA), Polar Geospatial Center.¹³

## Acknowledgments
 
Acknowledgments

This research was funded by the National Science Foundation and the Department of Geological Sciences at Brigham Young University.

Soil samples, laboratory analyses, and the multiple linear regression baseline come from the thesis work of Rachel Willmore.² We thank Abidemi Aremu, Audrey Hughes, Austen Lambert, Alan Ketring, Caleb Harris, Danny Lopez Cedeno, Forrest Jarvis, Kate Hales, Kara Hunter, Lynette Juarez, Lindy Miller, Meagan Boden, Maleah Moore, Mardell Overson, Sierra Stewart, and Seth Wuthrich for laboratory work, and Kevin Rey for guidance on the laboratory analysis. We also thank Dr. Ruth Kerry for her support.

Climate data were accessed through the Norwegian Polar Institute's Quantarctica package.¹² Digital elevation models were provided by the Byrd Polar and Climate Research Center and the Polar Geospatial Center under NSF-OPP awards 1043681, 1542736, 1543501, 1559691, 1810976, and 2129685, with data access via OpenTopography under NSF-EAR awards 1948997, 1948994, and 1948857.¹³
 
