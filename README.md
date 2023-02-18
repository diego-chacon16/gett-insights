# Insights from Failed Cab Orders

## Who is Gett?

+ Previously known as GetTaxi, is an Israeli-developed technology platform solely focused on corporate Ground Transportation Management (GTM).
+ They have an application where clients can order taxis, and drivers can accept their rides (offers).
+ At the moment, when the client clicks the Order button in the application, the matching system searches for the most relevant drivers and offers them the order.

## Purpose of this Project

### We would like to investigate some matching metrics for orders that did not completed successfully, i.e., the customer didn't end up getting a car.

#### This notebook will explore:

1. Distribution of orders according to reasons for failure: cancellations before and after driver assignment, and reasons for order rejection. Analyse the resulting plot. Which category has the highest number of orders?
2. Distribution of failed orders by hours. Is there a trend that certain hours have an abnormally high proportion of one category or another? What hours are the biggest fails? How can this be explained?
3. What is the average time to cancel on average? Plot the average time to cancellation with and without driver, by the hour. If there are any outliers in the data, it would be better to remove them. Can we draw any conclusions from this plot?

 + When are most of these cancellations happening from an hour perspective?
 + What are the drivers behind so many customers cancelling their orders before a driver is assigned?
 + Could the Customer wait time for a driver being assigned to their order be a leading cause?
 + How long are Customers approximately waiting to cancel their order prior to a driver being assigned?
 
4. Distribution of average ETA by hours. How can this plot be explained?

## Data Description

We have two data sets: data_orders and data_offers, both being stored in a CSV format. The data_orders data set contains the following columns:

+ order_datetime - time of the order
+ origin_longitude - longitude of the order
+ origin_latitude - latitude of the order
+ m_order_eta - time before order arrival
+ order_gk - order number
+ order_status_key - status, an enumeration consisting of the following mapping:
   - 4 - cancelled by client,
   - 9 - cancelled by system, i.e., a reject
+ is_driver_assigned_key - whether a driver has been assigned
+ cancellation_time_in_seconds - how many seconds passed before cancellation

The data_offers data set is a simple map with 2 columns:

+ order_gk - order number, associated with the same column from the orders data set
+ offer_id - ID of an offer


## Bonus

### Using Geospatial Analysis Tools to calculate how many hexes contain 80% of cancellations

+ Use Uber's open source H3 and Folium libraries to build analysis
+ Build a table to sum the cumulative percentage of cancellations
+ This can be done by creating a count of the order_gk column, and then apply a cumulative percentage

### What is H3?

+ At its core, H3 is a geospatial analysis tool that provides a hexagonal, hierarchical spatial index to gain insights from large geospatial datasets 

### What is Folium?

+ Builds on the data wrangling strengths of the Python ecosystem and the mapping strengths of the leaflet.js library
+ folium makes it easy to visualize data that’s been manipulated in Python on an interactive leaflet map. It enables both the binding of data to a map for choropleth visualizations as well as passing rich vector/raster/HTML visualizations as markers on the map
