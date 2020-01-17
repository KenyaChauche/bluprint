# Ames Housing Data 

## Problem and Background
First-time home buying is an ominous task, and the real estate market is nebulous. When people first start searching for a home, they often have an idea of the home they want, but rarely know what price range this will put them in. I am suggesting an app that will allow a user to customize a limited number of traits and receive a prediction of what they will likely pay for a house of that type. This would allow users to play with different traits and see how being flexible on certain features will affect their budget. 

This project works specifically with a dataset describing homes and their final sale prices in Ames, Iowa. These data range from years 2006 - 2010. This is intended for a trial in a specific geographic location which, depending on use and user engagement, can then be expanded to a wider audience and geographical range. Future expansion would necessitate gathering more housing data for the new target cities so the model can remain accurate.  

## Data Dictionary

*Data documentation originally sourced from http://jse.amstat.org/v19n3/decock/DataDocumentation.txt. It is pared down here for simplicity. Each original column is described here, for information on categorical values and meanings please go to link.*

| Name | Description |
|----|----|
|**Order**| Observation number|
|**PID** | Parcel identification number (use with city website for parcel review) |
|**MS SubClass**| Identifies type of dwelling |
|**MS Zoning**| Identifies general zoning classification |
|**Lot Frontage**| Linear feet of street connected to property |
|**Lot Area**| Lot size in square feet |
|**Street**| Type of road access to property |
|**Alley**| Type of alley access to property | 
|**Lot Shape**| General shape of property |
|**Land Contour**| Flatness of the property |
|**Utilities**| Type fo utilities available |
|**Lot Config**| Lot configuration |
|**Land Slope**| Slope of property |
|**Neighborhood**| Physical locations within Ames city limits |
|**Condition 1**| Proximity to various conditions |
|**Condition 2**| Proximity to various conditions (if more than one applicable) |
|**Bldg Type**| Type of dwelling |
|**House Style**| Style of dwelling | 
|**Overall Qual**| Rates the overall material and finish of the home |
|**Overall Cond**| Rates overall condition of the house |
|**Year Built **| Original constructiond ate |
|**Year Remod/Add**| Remodel date (same as construction date if no remodel) | 
|**Roof Style**| Type of roof |
|**Roof Matl**| Roof material |
|**Exterior 1**| Exterior covering on house | 
|**Exterior 2**| Second exterior covering on house if applicable | 
|**Mas Vnr Type**| Masonry veneer type |
|**Ms Vnr Area**| Masonry veneer area in square feet |
|**Exter Qual**| Evaluates quality of the material on exterior | 
|**Exter Cond**| Evaluates present condition of the material on exterior |
|**Foundation**| Type of foundation | 
|**Bsmt Qual**| Evaluates height of basement | 
|**Bsmt Cond**| Evaluates genera condition of the basement | 
|**Bsmt Exposure**| Refers to walkout or garden level walls |
|**BsmtFin Type 1**| Rateing of bsement finished area | 
|**BsmtFin SF 1**| Type 1 finished square feet |
|**BsmtFin Type 2**| Rating of basement finished area (if multiple types) |
|**BsmtFin SF 2**| Type 2 finished square feet |
|**Bsmt Unf SF**| Unfinished square feet of basement area |
|**Total Bsmt SF**| Total square feet of basement area | 
|**Heating**| Type of heating |
|**HeatingQC**| Heating quality and condition |
|**Central Air**| Central air conditioning |
|**Electrical**| Electrical System | 
|**1st Flr SF**| First floor square feet | 
|**2nd Flr SF**| Second floor square feet if applicable |
|**Low Qual Fin SF**| Low quality finished square feet (all floors) | 
|**Gr Liv Area**| Above ground living area square feet | 
|**Bsmt Full Bath**| Basement full bathrooms | 
|**Bsmt Half Bath**| Basement half bathrooms | 
|**Full Bath**| Full bathrooms above ground | 
|**Half Bath**| Half baths above ground | 
|**Bedroom**| Bedrooms above ground | 
|**Kitchen**| Kitchens above ground | 
|**KitchenQual**| Kitchen quality | 
|**TotRmsAbvGrd**| Total rooms above ground (not including bathrooms) (this is changed later to include bathrooms) | 
|**Functional**| Home functionality | 
|**Fireplaces**| Number of fireplaces | 
|**FireplaceQu**| Fireplace quality | 
|**Garage Type**| Garage location | 
|**Garage Yr Built**| Year garage was built | 
|**Garage Finish**| Interior finish of garage | 
|**Garage Cars**| Size of garage in car capacity | 
|**Garage Area**| Size of garage in square feet | 
|**Garage Qual**| Garage quality |
|**Garage Cond**| Garage condition |
|**Paved Drive**| Paved driveway | 
|**Wood Deck SF**| Wood deck area in square feet | 
|**Open Porch SF**| Open porch area in square feet | 
|**Enclosed Porch**| Enclosed porch area square feet | 
|**3-Ssn Porch**| Three season porch area in square feet | 
|**Screen Porch**| Screen porch area in square feet | 
|**Pool Area**| Pool area in square feet | 
|**Pool QC**| Pool quality | 
|**Fence**| Fence quality (relating to privacy created) | 
|**Misc Feature**| Miscellaneous feature not covered in other categories | 
|**Misc Val**| Dollar value of miscellaneous feature | 
|**Mo Sold**| Month Sold (MM) | 
|**Yr Sold**| Year sold (YYYY) | 
|**Sale Type**| Type of sale | 
|**Sale Condition**| Condition of sale | 
|**SalePrice**| Sale price in dollars | 

## Feature Selection 
The initial selection of parameters had 24 traits. Initial selection was based off of visualization of relationships between sale price and each feature, the apparent strength of that relationship based off that visualization, and information from a heatmap illustrating the correlation between certain numerical traits and sale price. In subsequent versions of preprocessing and modeling, parameters were eliminated to reduce complexity of the model. Despite the initial selection of parameters being 24, once categorical features were one-hot encoded the number of columns ballooned up to over 130. 

Over 6 different versions, features were eliminated based on relative relationship strength (relationships that appeared weaker than others still included in the model were removed), redundancy (having both Total Square Footage and Above Ground Square Footage), and human comprehension. Since the goal of this project is to identify traits to use in a prediction model for an app for first time home buyers, the parameters needed to describe traits that were easily understandable by the average person (hence removing MS SubClass and Zoning in an early version and keeping Neighborhoods instead). 

Features describing quality or condition with words were changed to express quality on a numerical instead to make this parameter compatible with modeling. The feature for Garage Type was simplified to only indicate whether there was a protected garage present. In this case, a protected garage is considered a garage with full walls and overhead coverage and a door so the vehicle parked within would be completely protected. Carports and absent garages were lumped together since average sales price for both of these categories was very similar and they were both far removed from the other garage types when this trait was graphed. 

## Modeling 
This project uses multiple linear regression, scaled linear regression, LASSO regression, and Ridge regression to determine a suitable model for predicting final home sale prices. There were 6 iterations of each of these models for each stage of feature elimination, and in most cases LASSO regression had the best performance. The final model uses LASSO regression, with an $R^2$ training average of 0.842 and an $R^2$ testing average of 0.844. 

## Recommendations 
It is recommended that an app be developed to help users determine their own budget for first time home buying. To strike the balance between customizability and appropriate model complexity it is suggested that the model the app is based on includes these parameters: neighborhood, house style, basement condition, kitchen quality, total rooms garage type, pool quality, total square footage, overall condition/quality average, age at sale, and age of remodel at sale. These parameters should be used in a tool where users can customize each of these things (perhaps with some features behind an "advanced" option). 