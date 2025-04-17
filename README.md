# GLY6932_Finalproject
# LANDSLIDE SUSCEPTIBILITY USING SUPPORT VECTOR MACHINE AND GENERALIZED LINEAR MODEL

This project seeks to compare the accuracy of SVM and GLM for predicting landslide susceptibility at Southern Ecuador. The accuracy is measured by the AUROC metric.
Area Under the Receiver Operator Characteristic Curve (AUROC) is good way to assess binomial model fit
# AUROC will be value between 0.5 (no better than random) and 1.0 (perfect prediction).
The Spatial Cross Validation mean AUROC for SVM is 0.75 and that for the GLM is 0.78.
This indicates that GLM is better for the prediction of landslide susceptibility than SVM in this case.

# Landslide Susceptibility Modeling using Support Vector Machines (SVM)

This repository provides a complete Python workflow for **landslide susceptibility modeling** using **Support Vector Machines (SVM)** with **radial basis function (RBF)** kernel. The script performs hyperparameter tuning, spatial cross-validation, and model export.

##  Summary

- Uses terrain variables (slope, curvature, elevation, etc.) to predict landslide occurrence
- Performs **randomized hyperparameter search** for `C` and `gamma`
- Evaluates performance using **StratifiedKFold** and **GroupKFold** for spatial cross-validation
- Outputs model performance (AUROC) and saves the best model as a `.joblib` file


##  Input Requirements

The input file `lsl.csv` must contain the following columns:

| Column         | Description                                 |
|----------------|---------------------------------------------|
| `x`, `y`       | Coordinates of each observation             |
| `lslpts`       | Binary label for landslide occurrence (TRUE/FALSE) |
| `slope`        | Slope angle                                 |
| `cplan`        | Plan curvature                              |
| `cprof`        | Profile curvature                           |
| `elev`         | Elevation                                   |
| `log10_carea`  | Log10-transformed catchment area            |


## Workflow Overview

1. Load Data from `lsl.csv`
2. Define SVM pipeline with `StandardScaler` and `SVC` (RBF kernel)
3. Randomized Hyperparameter Tuning:
   - Search over `C = 2^[-12, ..., 15]`
   - Search over `gamma = 2^[-15, ..., 6]`
   - 5-fold stratified cross-validation using AUROC as metric
4. Train final model with best parameters
5. Create spatial folds using `KMeans` on `x, y`
6. Evaluate using spatial cross-validation (5-fold `GroupKFold`)
7. Save the best model as `svm_model.joblib`


##  Output Products
svm_model.joblib: Trained best SVM model for future prediction

Terminal output showing:
Best AUROC from tuning
Best hyperparameters
Mean AUROC from spatial cross-validation


## Landslide Susceptibility Modeling using GLM in Python

This repository contains a Python workflow for modeling landslide susceptibility in southern Ecuador using **Generalized Linear Models (GLM)** . The model predicts the probability of landslide occurrence and evaluates model performance through **spatial cross-validation** and **AUROC** metrics.

## Files Included
1. lsl is landslide dataset from southern Ecuador and its object kind is a data.frame. It has 350 observations by 8 variations as the dimensions.
2. study_mask is a polygon showing the land use characteristic as natural from the landslide data set of southern Ecuador. It has 1 observation by 2 variables as the dimensions.
3. `lsl.csv` — Point dataset with landslide occurrences and coordinates
4. `study_mask.shp` (+ associated files) — Shapefile defining the study area boundary
  
- ## Terrain variables that are in lsl that we will use as predictors of landslides
1. `slope`:  slope angle (°)
2. `cplan`: plan curvature (rad m^−1^) expressing the convergence or divergence of a slope and thus water flow
3. `cprof`: profile curvature (rad m^-1^) as a measure of flow acceleration, also known as downslope change in slope angle
4. `elev`: elevation (m a.s.l.) as the representation of different altitudinal zones of vegetation and precipitation in the study area
5. `log10_carea`: the decadic logarithm of the catchment area (log10 m^2^) representing the amount of water flowing towards a location

- ## other parameters in the lsl
X and Y coordinates and lslpts which is TRUE or FALSE for landslide occurrence

## Model Workflow
1. Load landslide data 
2. Extract terrain attributes from landslide data
3. Fit a logistic regression (GLM) model
4. Evaluate with spatial cross-validation (GroupKFold)
5. Plot predictions over a basemap
6. Export susceptibility maps as GeoTIFFs
7. Clip final raster with study area shapefile

##  Output Products
1. `susceptibility_map_with_basemap.png` — Point-based susceptibility map on a basemap
2. `susceptibility_map.tif` — Full raster of predicted landslide probability
3. `susceptibility_map_clipped.tif` — Clipped raster using `study_mask.shp`

## Output Figures



##  Requirements

Install dependencies using `pip`:

pip install pandas numpy matplotlib rasterio geopandas scikit-learn contextily scipy


##  Reference
Muenchow, J., Brenning, A., & Richter, M. (2012). Geomorphometric characterization of landslide-prone terrain.

##  COLAB LINK
https://colab.research.google.com/drive/1h-jJGvl93yJsCXluw_PgrLfaEKZimsOm?usp=sharing


