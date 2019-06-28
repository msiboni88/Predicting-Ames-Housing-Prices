# Project 2 - Predicting Home Sale Prices in Ames Iowa
## Data Dictionary
|Feature|Type|Dataset|Description|
|---|---|---|---|
|overall_qual|int|h_df|Overall Quality of Home, scale from 10 (Very Excellent) to 1 (Very Poor), unmodified from original dataset| 
|year_built|float64|h_df|Original Construction Year, unmodified from original dataset| 
|roof_style|float64|h_df|Hip = 1, All other roof types = 0, modified from original dataset| 
|roof_matl|float64|h_df|Wood Shake or Wood Shingle = 1, All other roof materials = 0, modified from original dataset| 
|mas_vnr_area|float64|h_df|Masonry Veneer Area in Square Feet, unmodified from original dataset| 
|exter_cond|int64|h_df|Exterior Condition, scale from 5 (Excellent) to 1 (Poor), modified from original dataset| 
|bsmt_exposure|float64|h_df|Good = 1, Less than good exposure or no basement = 0, modified from original dataset| 
|total_bsmt_sf|float64|h_df|Basement Area in Square Feet, unmodified from original dataset| 
|gr_liv_area|float64|h_df|Above Ground Living Area in Square Feet, unmodified from original dataset| 
|full_bath|int64|h_df|Full Bathrooms Above Grade, ummodified from original dataset| 
|kitchen_qual|int64|h_df|Kitchen Quality, scale from 5 (Excellent) to 1 (Poor), modified from original dataset| 
|fireplaces|int64|h_df|Number of fireplaces, unmodified from original dataset|
|garage_area|float64|h_df|Garage Area in Square Feet, unmodified from original dataset| 
|paved_drive|int64|h_df|Fully Paved Driveway = 1, Partially Paved, Unpaved or No Driveway = 0, modified from original dataset| 
|saleprice|int64|h_df|Sale Price of Home, unmodified from original dataset| 
|has_basement|int64|h_df|Has Basement = 1, Does not have = 0, modified from bsmtfintype 1 and 2| 
|attached_garage|float64|h_df|Built In or Attached = 1, All other types or none = 0, modified from garage_type| 
|offsite_feature|int64|h_df|Near of Adjacent to Positive Offsite Feature = 1, Not Near = 0, modified from condition_1| 
|residential_low|int64|h_df|Zoned as Low Density Residential = 1, Otherwise = 0, modified from ms_zoning| 
|residential_other|int64|h_df|Zoned as Residential: Medium Density, High Density or Park = 1, Otherwise = 0, modified from ms_zoning| 
|floating_village|int64|h_df|Zoned as Floating Village = 1, Otherwise = 0, modified from ms_zoning| 
|commercial|float64|h_df|Zoned as Commercial = 1, Otherwise = 0, modified from ms_zoning|
|str_gravel|float64|h_df|Access to property is Gravel = 1, Otherwise = 0, modified from street| 
|regular_lot|int64|h_df|Lot Shape is Regular = 1, Others = 0, modified from lot_shape| 
|ir2_lot|int64|h_df|Lot Shape is Moderately Irregular = 1, Others = 0, modified from lot_shape|  
|culdesac|int64|h_df|Properties in a Cul-de-sac = 1, Otherwise = 0, modified from lot_config| 
|northridge|int64|h_df|Located in Northridge = 1, Otherwise = 0, modified from neighborhood| 
|northridge_hts|int64|h_df|Located in Northridge Heights = 1, Otherwise = 0, modified from neighborhood| 
|briardale|int64|h_df|Located in Briardale = 1, Otherwise = 0, modified from neighborhood| 
|---|---|---|---|
|log_gr_liv_area|float64|h_df|Natural Log of gr_liv_area Variable| 
|log_total_bsmt_sf|float64|h_df|Natural Log of total_bsmt_sf Variable| 
|sqrt_gr_liv_area|float64|h_df|Square Root of gr_liv_area Variable| 
|square_overall_qual|int64|h_df|Square of overall_qual| 
|inter_qual_rl|int64|h_df|Interaction between overall_qual and residential_low| 
|inter_qual_fv|int64|h_df|Interaction between overall_qual and floating_village| 
|inter_area_fv|float64|h_df|Interaction between gr_liv_area and floating_village| 
|qual_bsmt_sf|float64|h_df|Interaction between overall_qual and total_bsmt_sf| 



## [EDA and Cleaning Notebook](https://github.com/msiboni88/Project_2-Ames_Housing_Prices/blob/master/Ames%20Housing%20Project%20-%20Part%201%20-%20EDA.ipynb)
#### Table of Contents
- Load Data
- Garage Variables EDA
- Size Variables EDA
- Quality Variables EDA
- Access Variables EDA
- Land Variables EDA
- Utilities Variables EDA
- Remaining Variables EDA
- Modifying Test Data Set
- Data Cleaning

#### Highlight: 
I relied heavily on the hue feature for Seadorn pairplots to evaluate categorical data at a glance. 
![Image of Pairplot](https://github.com/msiboni88/Project_2-Ames_Housing_Prices/blob/master/pairplot.png)

## [Modeling Notebook](https://github.com/msiboni88/Project_2-Ames_Housing_Prices/blob/master/Ames%20Housing%20Project%20-%20Part%202%20-%20Modeling.ipynb)
#### Table of Contents
- Import Libraries and Read Data
- Model Iteration Set 1
    - Limits independent variables to: overall_qual, gr_liv_area, year_built, attached_garage
    - From this set of models, it appears that modeling for log y produces a better model
- Model Iteration Set 2
    - Input ALL variables carried over after EDA
    - Run Ridge and LASSO regressions
- Model Iteration Set 3
    - Looking at higher coefficient variables to determine if the variables on their own should be manipulated 
    - Input smaller set of data
    - Created scatter plots of various x versus y with predicted and actual values in two different colors to look for patterns
    - Added the following variables: sqrt_gr_liv_area, log_total_bsmt_sf
- Model Iteration Set 4
    - Added interaction variables: overall_qual X residential_low, overall_qual X floating_village, sqrt_gr_liv_area X floating_village 
    - Removed low coefficient variables
    - Pulled in data previously dropped from original dataset: Fireplaces, Street type Gravel, Zoning type Commercial, Lot types IR2 and Regular
- Model Iteration Set 5
    - Used poly fit to the 2nd degree to create interactions from the following variables: residential_low, overall_qual, gr_liv_area, total_bsmt_sf, floating_village
    - Based on regression coefficients, determind the two new interactions worth adding were: overall_qual^2 and overall_qual X total_bsmt_sf
- *Modeling with sqrt y instead of log y*
    - Upon reviewing all my models and graphs, I noticed that a log fit for y may not have been the best match to the curve. 
    - I reran several of the models with sqrt y instead of loy as the dependent variable. 
    
#### Highlight: 
I hoped to use scatter plots modeling actual values and predicted values versus various independent variables to inform how to modify particular variables. 
![Image of Scatter Plot](https://github.com/msiboni88/Project_2-Ames_Housing_Prices/blob/master/scatter.png)

## [Presentation Notebook](https://github.com/msiboni88/Project_2-Ames_Housing_Prices/blob/master/Ames%20Housing%20Project%20-%20Part%203%20-%20Presentation.ipynb)
#### Table of Contents
- Import Libraries and Read Data
- Data Dictionary
- Price Distribution Graphs
- Model Prediction Graph
- Quality Graphs

#### Highlight:
In order to convey the impact my model shows overall quality having on saleprice, I took the existing train data and ran it through the model 10 times. Each time, I replaced all actual quality value with one of the 10 available quality values. This conveys that, according to my model, all else being equal, improving the qulaity of a home increases its value significantly. 
![Image of Scatter Plot2](https://github.com/msiboni88/Project_2-Ames_Housing_Prices/blob/master/scatter2.png)

## [Presentation](https://github.com/msiboni88/Project_2-Ames_Housing_Prices/blob/master/Siboni_Project2.pdf)
I crafted my presentation to be directed at current home owners in the area. I focused on the easiest changes that these home owners could make to increase the sale price of that home. 

For the presentation, I made my model as easy to interpret as possible while still accurately predicting sale price. I selected one of my better performing Lasso models from the kaggle competition. I then removed variables with near zero coefficients until I had my simplest model that still had an r squared value above 0.9.

To convey clearly how this linear regression weighted variables, I created an image with the font size of the text of each variable directly proportional to its scaled coefficient's size: 
![Image of Function](https://github.com/msiboni88/Project_2-Ames_Housing_Prices/blob/master/function.png)

I then dug in to the metrics that might impact quality and came to the conclusion that adding an attached garage or paved driveway to a home are the most effective ways to increase the sale price of a home. 

