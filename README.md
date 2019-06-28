# Project 2 - Predicting Home Sale Prices in Ames Iowa

## Presentation Focus: 
I crafted my presentation to be directed at current home owners in the area. I focused on the easiest changes that these home owners could make to increase the sale price of that home. 

For the presentation, I wanted my model to be as easy to interpret as possible while still accurately predicting sale price. I selected one of my better performing Lasso models from the kaggle competition. I then removed variables with near zero coefficients until I had my simplest model that still had an r squared value above 0.9. 

To convey clearly how this linear regression weighted variables, I created an image with the font size of the text of each variable directly proportional to its scaled coefficient's size: 
![Image of Function](https://github.com/msiboni88/Project_2-Ames_Housing_Prices/blob/master/function.png)
