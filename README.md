# Insights from Failed Cab Orders

## Who is Gett?

+ Previously known as GetTaxi, is an Israeli-developed technology platform solely focused on corporate Ground Transportation Management (GTM).
+ They have an application where clients can order taxis, and drivers can accept their rides (offers).
+ At the moment, when the client clicks the Order button in the application, the matching system searches for the most relevant drivers and offers them the order.

## Objective

The primary objective is to understand the distribution of failed orders and identify key factors contributing to unsuccessful outcomes. The analysis is structured to answer specific questions related to order cancellations, rejection reasons, and customer wait times before driver assignment. __(I.e. The customer didn't end up getting a car)__

#### This notebook will explore:

1. Distribution of Order Failure
   + Categorize reasons for failure, differentiating between cancellations before and after driver assignment.
   + Analyze resulting plots to identify the category with the highest number of orders.
2. Temporal Analysis
   + Examine the distribution of failed orders by hours to identify trends.
   + Highlight hours with abnormally high proportions of specific failure categories.
3. Average time to cancel
   + Calculate and plot the average time to cancel, both with and without driver assignment, by the hour.
   + Identify outliers and draw conclusions from the plot.
4. Cancellation Timing
   + Determine when most cancellations occur from an hourly perspective.
   + Investigate factors behind customers canceling orders before a driver is assigned.
5. Customer Wait Time
   + Explore if the wait time for a driver assignment influences order cancellations.
   + Analyze the duration customers are waiting before canceling their orders.
6. ETA Analysis
   + Examine the distribution of average Estimated Time of Arrival (ETA) by hours.
     
## Data Description

### Table 1: data_orders

Data specific to the order

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

### Table 2: data_offers

Simple map with two columns

+ order_gk - order number, associated with the same column from the orders data set
+ offer_id - ID of an offer

## Bonus: Geospatial Analysis

### Using Geospatial Analysis Tools to calculate how many hexes contain 80% of cancellations

A bonus aspect of this analysis involves leveraging Geospatial Analysis Tools to calculate the hexagons containing 80% of cancellations. Uber's open source H3 and Folium libraries are employed for this purpose. H3 provides a hexagonal, hierarchical spatial index, while Folium facilitates interactive data visualization on leaflet maps.

### What is H3?

+ At its core, H3 is a geospatial analysis tool that provides a hexagonal, hierarchical spatial index to gain insights from large geospatial datasets 

### What is Folium?

+ Builds on the data wrangling strengths of the Python ecosystem and the mapping strengths of the leaflet.js library
+ folium makes it easy to visualize data that’s been manipulated in Python on an interactive leaflet map. It enables both the binding of data to a map for choropleth visualizations as well as passing rich vector/raster/HTML visualizations as markers on the map
