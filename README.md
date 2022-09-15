# Surf's Up

## Overview
In this analysis, we are trying to determine the difference of average temperatures in June and December in Oahu, HI to discern the feasibility for a year-round surf and ice cream shop.

## Results

We used SQLAlchemy to pull the data from an SQLite file on the specific month of June.  The data covered the temperatures collected from 2010 to 2017. Here is the query we used:

    june_results = session.query(Measurement.date, Measurement.tobs).filter(extract('month',Measurement.date)==6).all()
    
We compiled this data by converting to a DataFrame and using the ".describe" function and getting the pertinent statistics we needed for out analysis.

    june_df = pd.DataFrame(june_results, columns=['date', 'tobs'])
    june_df.set_index(june_df['date'])
    june_df.describe()
    
 ![June_Summary](https://user-images.githubusercontent.com/108296899/190398065-e3f2a851-d289-42bc-88c8-962fbb31963b.png)

We repeated this code for the month of December to get the comparison summary.

    dec_results = session.query(Measurement.date, Measurement.tobs).filter(extract('month',Measurement.date)==12).all()
    
    dec_df = pd.DataFrame(dec_results, columns=['date', 'tobs'])
    dec_df.set_index(dec_df['date'])
    
 ![Dec_Summary](https://user-images.githubusercontent.com/108296899/190398325-c6073d88-3f3c-4562-bb42-ff7709959515.png)

By looking at the summary statistics we can deduce that:

- The difference in average temperature between June and December is less and 4 °F.

- The standard deviation for those months is also less than 4 °F.

- The minimum and maximum temperatures average difference is 5 °F.

## Summary

This analysis shows that the weather in Oahu, HI changes only slightly throughout the year and remains mostly the same even if you contrast the months. The temperature swing from June to December is minimal and the variance in temperature remains stable in both those months.

To further analize this request, we added precipitation data to the query to see if there was a major change in rainfall between June and December. 
    
##### June

    june_results = session.query(Measurement.date, Measurement.tobs, Measurement.prcp).filter(extract('month',Measurement.date)==6).all()
    june_df = pd.DataFrame(june_results, columns=['date', 'tobs', 'prcp'])
    june_df.set_index(june_df['date'])
    
![June_Sum_Precip](https://user-images.githubusercontent.com/108296899/190401182-57e1f5a5-0b25-401e-86d5-baef50696974.png)

##### December

    dec_results = session.query(Measurement.date, Measurement.tobs, Measurement.prcp).filter(extract('month',Measurement.date)==12).all()
    dec_df = pd.DataFrame(dec_results, columns=['date', 'tobs', 'prcp'])
    dec_df.set_index(dec_df['date'])

![Dec_Sum_Precip](https://user-images.githubusercontent.com/108296899/190401208-f4c8b2fc-8741-439d-820f-10118599f512.png)

We can still see that there is little difference in weather even when factoring precipitation. The data is conclusive that this location would be ideal for a year-round business.
