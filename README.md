# lecture

Seminar at the School of Digital Humanities and Computational Social Science, Korea Advanced Institute of Science and Technology (KAIST)

- Guest Lecturer: Kyungmin Lee, Ph.D. (kmlee@udel.edu)
- Date: Nov 12, 2025

This notebook is created for learning the basic process of image segmentation (e.g., parking lots, roofs, trees).
The notebook contains information about five steps:

Step 1. Load Satellite Images Using the Google Maps API

Step 2. Label Pixels

Step 3. Create Patches

Step 4. Build a Random Forest Classifier

Step 5. Visualize Predicted Images

Before processing the notebook, please note that you need to 1) change the file directory name and 2) obtain your Google Maps API key to run the code.

If you have any further questions, please feel free to email me.

The results will be shown in the figures below:

## Figure 1. KAIST Satellite Image Tiles
![KAIST Satellite Maps](output/fig1.png)

Download Google Maps satellite images using the Static Maps API. The figure shows a 3 × 3 grid of satellite images, each adjusted by moving 0.003 degrees in latitude and longitude from the School of Digital Humanities and Computational Social Science, KAIST (map0_0.png).

## Figure 2. KAIST Satellite Image Test Tile
![KAIST Satellite Image Test Tile](output/fig2.png)

This notebook uses map0_0.png as the baseline image for testing the application of a Random Forest model in image segmentation. Three object categories—parking lots, roofs, and trees—were manually annotated, with 100 labeled pixels for each class to construct the training dataset. 

Patches were generated because the Random Forest model, like most machine learning classifiers, is trained on small localized image regions rather than on single pixels or entire images. Each patch was extracted around a labeled pixel and converted into descriptive features such as color, texture, and edge intensity. Using these features, the Random Forest model learned to associate characteristic visual patterns within each 32×32 region with their corresponding object classes (i.e., parking lot, roof, or tree).

## Figure 3. Random Forest Prediction
![Random Forest Prediction](output/fig3.png)

The results show the patch-level Random Forest classification used to detect parking lots, roofs, and trees. Since ground-truth labeled pixel information is provided, the process represents supervised image segmentation.

However, because both the training and testing data are derived from the same image, the F1-scores are likely over-optimistic due to spatial leakage. More advanced methods can be applied to avoid spatial leakage, such as (1) training and evaluating on different image tiles (e.g., map0_1, map0_2).



