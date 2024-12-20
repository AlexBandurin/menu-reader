<p align="center">
<img src="https://github.com/AlexBandurin/Menu_Reader/blob/master/Menu_app_image.png"  width="100%" height="90%">

# Menu_Reader

This is a web application that converts an image file of a restaurant menu into text using Optical Character Recognition (OCR). 
That text is then sent through a Machine Learning (ML) model to output a list of menu items using classification and Natural Language Processing techniques. 
The list is then passed to another ML model to be sorted into categories.

[View the App](https://menu-reader-1ada6a994a40.herokuapp.com/)


## EasyOCR
An **optical character recognition** (OCR) package for converting an image file into distinct pieces of text (textboxes).
EasyOCR implements a deep learning execution based on Pytorch.
[About EasyOCR](https://github.com/JaidedAI/EasyOCR)

## Feature Engineering
23 Menus have been collected from the internet and converted into text through OCR. This text was organized into a table with the help of Python's pandas package,
totaling **over 2500 rows** of text. Through trial and error, 18 features have been selecting for text classification (including text length, word count, character count,
punctuation count, uppercase letter count, numerical character count, etc.)

## Model Building
The table with texts and their corresponding features has been manually labelled as a "menu item" or not (0 or 1) in Excel. This labeled dataset was then ready to be sent 
through an ML model for binary classification. Algorithm tested: Decision Tree (R^2 = 0.858), Random Forest (R^2 = 0.860), and **XGBoost (R^2 = 0.922)**, 
out of which XGBoost was deemed the most accurate. <br>
The menu items generated by this model have been sent through another model that relies on BERT as well as a few additional features that indicate the 
presense of key words within the menu to categorize these items. **BERT** is a machine learning framework for natural language processing. Text was converted 
into **word embeddings** (768 features) to assist with classification modeling.  <br>
[ML Models Notebook](https://github.com/AlexBandurin/Menu_Reader/blob/master/menu_reader_modeling.ipynb)

## Azure Cloud and Web Application
To make this application accessible to any user on the web, it was hosted on **Heroku, a cloud platform** . Flask was used to develop this application. <br>
[Web App Files](https://github.com/AlexBandurin/Menu_Reader/tree/master/menu_reader_app) <br>
The algorithms used for OCR and text classification/categorization are quite memory intesive. To offload these computations, I used Azure Function App.
The image selected by a user is sent to the **Function App in a JSON format via RESTful API interface**. The result (consisting of generated menu items sorted 
into categories) is returned to the web application on which it is displayed. <br>
[Function App Files](https://github.com/AlexBandurin/Menu_Reader/tree/master/menu_function) 


<!---
The following features were used for classification:
- Text (word embeddings)
- width (width of text box)
- height (height of text box)
- uppercase (number of uppercase characters present in text)
- chars (number of characters)
- words (number of words)
- periods (number of periods)
- period_btw_numbers (count of periods between 2 numerical characters)
- number_end (count of numerical character at the end of text)
- numbers (number of numerical characters)
- commas (number of commas)
- exclamation (number of exclamation marks)
- question (number of numerical characters)
- colons (number of colons)
- underscores (number of underscores)
- dollar (number of dollar signs)
- punctuation (number of other punctuation characters)
- 2_periods_cnt	Item (count of 2 consecutive periods)
<br></br>
-->

