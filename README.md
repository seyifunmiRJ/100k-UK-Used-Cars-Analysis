# Project Name: 100,000 UK Used Cars Analysis 
This analysis aims to conduct an in-depth analysis of scraped data from used car listings, comprising of 100,000 UK used cars entries. The datasets include information such as model, year, price, transmission type, mileage, fuel type, road tax, miles per gallon (mpg), and engine size segmented by Audi, BMW, Ford, Hyundi, Mercedes, Skoda, Toyota, Vauxhall and Volkswagen (VW) car manufacturers respectively.

------
# Project objective: Problem Statement
The objective of this analysis is to provide valuable insights for stakeholders to make informed decisions in the UK used car market by examining metrics such as Age of car, Average price per model, Road Tax and Mileage. Using Power BI, it will answer questions such as average price per manufacturer, correlation between price and mileage, fuel type distribution, impact of road tax on price, and trends in mileage and price over time. 

------------
# Data Sourcing:
This data was sourced from Kaggle via https://www.kaggle.com/datasets/adityadesai13/used-car-dataset-ford-and-mercedes

--------
# Data Cleaning and Manipulation:
To ensure accuracy and the reliability of the analysis, the data was cleaned and manipulated using the power query editor in Microsoft Excel. 
I noticed the cclass and focus tables had 2 missing columns (tax and mpg) as compared to other tables and the tables were supposed to be included in the Mercedes and Ford car manufacturer’s tables respectively. I created the missing columns in cclass and focus and proceeded to merge them into their appropriate car manufacturer’s table then removed duplicates.
With nine (9) distinct car manufacturer’s tables left, I put each tables in sheets and saved the entire dataset as a single Excel file (UK used cars consolidated). I loaded the dataset into Power BI desktop and proceeded to clean the wholesome data in power query then close and applied it.
At the table view on power BI desktop, I created the following new columns using DAX;
 	
 ### Age of Car – “AgeOfCar = MAX('UK used cars consolidated'[year]) - 'UK used cars consolidated'[year]”
 	
  ### Price Per Mileage – “pricePerMileage = 'UK used cars consolidated'[price] / 'UK used cars consolidated'[mileage]”
 
 ### Average Price Per Model – “AvgPricePerModel = 
    AVERAGEX(
        FILTER(
            'UK used cars consolidated',
            'UK used cars consolidated'[model] = EARLIER('UK used cars consolidated'[model])
        ),
        'UK used cars consolidated'[price]
    )”

In order to import the brand logos as slicers, I created a new table, Brand Logos, where I added the logos weblink. DAX used:

### Brand Logos = 
UNION (
    ROW ( "Brand", "audi", "LogoURL", "https://automarken-liste.com/wp-content/uploads/2021/02/Audi-Logo-1536x1152.png" ),
    ROW ( "Brand", "bmw", "LogoURL", "http://logos-download.com/wp-content/uploads/2016/02/BMW_logo_big_transparent_png.png" ),
    ROW ( "Brand", "ford", "LogoURL", "http://www.pngmart.com/files/4/Ford-Logo-PNG-Transparent-Image.png" ),
    ROW ( "Brand", "hyundi", "LogoURL", "https://pluspng.com/img-png/hyundai-logo-png-hyundai-logo-512-png-by-mahesh69a-on-deviantart-512x512.png" ),
    ROW ( "Brand", "mercedes", "LogoURL", "https://freepngimg.com/download/mercedes_benz/24420-6-mercedes-benz-logo-transparent.png" ),
    ROW ( "Brand", "skoda", "LogoURL", "https://logos-world.net/wp-content/uploads/2021/04/Skoda-Emblem-700x394.png" ),
    ROW ( "Brand", "toyota", "LogoURL", "http://www.pngall.com/wp-content/uploads/2016/04/Toyota-Logo-Free-Download-PNG.png" ),
    ROW ( "Brand", "vauxhall", "LogoURL", "https://tse3.mm.bing.net/th?id=OIP.HudZaNvuMsl5TE86NOoCXwHaEK&pid=Api" ),
    ROW ( "Brand", "vw", "LogoURL", "https://www.pngplay.com/wp-content/uploads/3/Volkswagen-Logo-Free-PNG.png" )
)

----------
# Data Modelling:
I modeled the tables, UK Used Cars Consolidated and Brand Logos, using a many-to-one cardinality in the model view. This enables the Brand Logos table to filter the UK Used Cars Consolidated table. This means that one brand logo corresponds to many used car listings.

------
# Data Visualization:
Interactive Dashboard - https://app.powerbi.com/view?r=eyJrIjoiZWZjYmE3YjctYzE4My00MmJmLWIyYjQtOWUwNjlkYjkzOGMyIiwidCI6IjI3ZWZhYWQ3LWRiZjItNDQ0ZC1hZTE4LWM3ZTU0YzcwNWU4MyJ9

---------
# Findings:
•	The average price of cars in the dataset is £16,870, with an average age of 3 years, average road tax of £120, and average mileage of 23,103 miles.
•	Mercedes has the highest average price of £24,000, followed by Audi, BMW, VW, Skoda, Hyundi, Toyota and Ford, while Vauxhall has the lowest average price of £10,000.
•	Petrol is the most common fuel type, accounting for 49.13% of the distribution, followed by diesel at 47.43%, and hybrid at 3.44%. Cars powered electrically and others have low significance in the distribution, depicting the need to improve technology in these areas.
•	The column chart indicates that high-price brands like Mercedes and BMW have higher prices compared to their mileage, while mid-priced brands such as Audi, VW, and Skoda show a more balanced price-to-mileage ratio. Value brands like Hyundai, Toyota, Ford, and Vauxhall, particularly Vauxhall, offer better mileage for their price, emphasizing efficiency and cost-effectiveness. 
•	The scattered plot shows that while there is a general trend of higher-priced car models having higher road taxes, the relationship is not strictly linear, and there are several outliers and clusters indicating variability in road tax within certain price ranges.
•	The line chart shows price and mileage over the years increasing along the trend, this confirms the positive correlation seen in the scatter plot. As mileage increases, there is a general trend of price increasing as well. 

While slicing through the reports with the brand logo slicer, it showed the same findings for individual brands same as the overall dataset. The lower-priced brands tend to provide better mileage, highlighting their value for consumers focused on fuel efficiency. 

-----------------------
# Recommendations:
Consumers should prioritize less expensive brands such as Vauxhall, Hyundai, Toyota, and Ford if they seek cost effectiveness and better mileage, with Vauxhall offering the most value at an average price of £10,000. The analysis shows that these brands provide better mileage for their price, emphasizing fuel efficiency. Expensive brands like Mercedes and BMW, while offering luxury, have higher prices relative to their mileage, making them less efficient in terms of cost per mile.
Petrol and diesel vehicles are the most commonly produced in the market, with hybrid and electric cars making up a small percentage, indicating a potential area for technological advancement and market growth in alternative fuel vehicles. 
Road Tax is not dependent on Price or Mileage; therefore, consumers should take this as a personal preference or according to their budget.
