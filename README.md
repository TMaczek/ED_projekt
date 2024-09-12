# Data Exploration project

Project for Data Exploration course. We worked with Python notebooks, preparing data, updating our finding weekly and presenting our result to the group at the end.

## Dataset
We used the [Banana Index](https://www.kaggle.com/datasets/joebeachcapital/banana-index) dataset. It contains data of:

- **emissions** - CO2 or its equivalent for other greenhouse gases. Produced emissions values are given per 1 kg of food, 1000 kcal, 100g protein and 100g fat.
- **land use** - given for same metrics as emissions.
- **Banana index** - a value that was used to compare the products enviromental impact with banana in article that this dataset originated from.

## Analysis
We familiarized with dataset and removed some empty values. We deciced on 5 columns that we will proceed our analysis with. Values in other columns were based on those 5, so we could always calculate them again. After ploting corelation matrix for emission colums we noticed already very high corelation between land use and emissions, which will come up a few times later.   
![download](https://github.com/user-attachments/assets/efb94f2a-9741-4da2-abcd-f85db059e7da)  

## Outliers
We took two approached to finding outliers: first with **three sigma rule** for every column. Results here were easy to interpet. 
- For emissions in kg, all the beef products were found. Meat productions obviously results in most emissions.  ![download](https://github.com/user-attachments/assets/2fc393b2-9d4f-40a2-a0df-2bf4da0567e8)
- Emissions for 1000 kcal gave similar results, with **cottage cheese** replacing one of beef products, but it is dairy based so it's fairly understandable.  ![download](https://github.com/user-attachments/assets/c1e3d884-38ee-4539-96b2-90bdac0156ee)
- Results for emissions for 100g proteing were product high in sugars.  ![download](https://github.com/user-attachments/assets/5acc3d36-14ef-4751-94a9-aff023bab11e)

- For 100g fat we got fruit and lean products like **cottage cheese** again and **prawns**.  ![download](https://github.com/user-attachments/assets/af22bb76-db11-48ba-a08d-ceff7f230c59)

- For land use we got exactly same items as for emissions in kg, confirming their high corelation. ![download](https://github.com/user-attachments/assets/d6728fd4-dddd-42f1-9ce6-948ff1f012fe)


Second approach was to use **K nearest neighbors** algorithm on all data dimensions at once. We managed to find such parameters, that our result here were all previously found with three sigma rule. Below is show one of the plots from this part. In the notebook you can find ones with other columns compared.
![download](https://github.com/user-attachments/assets/7b474d44-46d5-45a0-b322-df14091acfc2)


## Clustering
This was the tricky part due to small size of dataset. We used **hierarchical clustering** with n=9. Our result are presented below. Because two colums are so highly corelated, we decided to use only one of them in plots, managing to show all relations between columns here.  ![download](https://github.com/user-attachments/assets/fb4ad6e3-814e-4ecc-abf0-73467e62a3ee)

Resulting clusters were descibed as follows (keep in mind, general trends are descibed)
1. Food with animal origin (meat products and milk products mostly)
2. Tomato products and fished (generally lean with low land use)
3. Fruits and rice (bit higher in calories but still low land use)
4. Beans and nuts (products decently high in calories while still with low land used)
5. Lamb products
6. Chicken, fish and mushrooms (somewhat caloric with not that high land use)
7. Plant products part 1 (mostly ones high in vitamins)
8. Butter and marmalade (yes, only those two)
9. Plant products part 2 (starchy products like wheat, potatoes etc.)

Keep in mind, that sizes of those groups were pretty small (group 8 beaing only 2 products), and group 8 was 53 items which was about 1/3 of whole dataset. Even when increasing **n** parameter up to 20, group 8 remained untouched while the others split into even smaller ones. We decided to remove group 7 and mark them as outliers.

## Classification
Using **OneVsOneClassifier**. Result were good, but still we see here dominance of one cluster.  
![download](https://github.com/user-attachments/assets/b13ffb3c-3264-4c14-8ae8-45c18758d4f7)  

## Data from other dataset
We prepared some additional data from [Agribalyse](https://agribalyse.ademe.fr/app). Despite the language barrier we managed to create our small dataset based on data there. While trying to classify items from Agribalyse using our previous model, result were not as expected. Majority of new product were classified as plant products. Our original dataset was dominated heavily with vegan options while being more balanced would be ideal and might have resulted in better clusterization.
