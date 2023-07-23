# Hotel Bookings Exploratory Data Analysis

## Introduction & Objective
We are provided with a hotel bookings dataset. 

In this analysis, we delve into a comprehensive hotel bookings dataset to extract valuable insights and understand the underlying trends in the hospitality industry. Our main goal is to conduct an Exploratory Data Analysis (EDA) on the provided dataset, allowing us to uncover significant patterns and interactions among various factors that influence hotel bookings. Through this exploration, we aim to draw meaningful conclusions that will enhance our understanding of the booking dynamics and provide valuable implications for the industry.

             
## Summary


The study reveals interesting insights about the booking patterns and cancellation trends in City Hotel and Resort Hotel.
The majority of bookings are for two persons, and City Hotel experiences a higher rate of cancellations compared to Resort Hotel.
The customer profile predominantly consists of transient guests from Portugal who often reserve Room Type A with BB category through Travel Agencies (TA) without requiring a deposit.

Notably, first-time customers are more likely to cancel their reservations, while guests who have stayed at the hotel previously tend to keep their bookings intact. The average wait time on the reservation list is around 2-3 days.
Cancellations tend to occur more frequently for reservations made well in advance, and interestingly, the Average Daily Rate (ADR) is higher for canceled reservations, implying that customers might find more competitive rates elsewhere during that period and thus decide to cancel.

Analyzing the historical data, it is evident that June 2016 saw the highest average cancellation rate, while June 2015 recorded the highest average number of reservations.

Taking into account additional findings, such as the popularity of TA/TO as the preferred booking channel and the significant number of European guests, especially from Portugal, hotels can devise strategies to improve customer retention and tailor their services to accommodate the needs of couples, who are the most common type of guests.
Moreover, optimizing the GDS channel could potentially lead to better ADR deals and increased revenue for both hotels.

Lastly, customers planning longer stays may be enticed by the prospect of better deals with lower ADRs, presenting an opportunity for hotels to attract this specific segment of clientele.

![Dashboard 1](https://github.com/alexdc1192/hotel.bookings/assets/118775369/378fd692-4d73-4c62-9204-594a2580358d)


## Challenges

It is very important to clean the dataset correctly and effectively, in order to obtain the most accurate and real study possible. This has been the biggest challenge for this project.
Also, it is important to have a strategic vision for the study, since we need to carry out an analysis focused on the greatest possible utility for this sector.


## Let's go...

## Dataset
We are given a hotel bookings dataset. This dataset contains booking information for a city hotel and a resort hotel. It contains the following features.

```
'hotel':
	- Hotel (H1 = Resort Hotel or H2 = City Hotel)

'is_canceled':
	- Value indicating if the booking was canceled (1) or not (0)

'adults':
	- Number of adults

'children':
	- Number of children

'babies':
	- Number of babies

'meal':
	- Type of meal booked. Categories are presented in standard hospitality meal packages: 
		- Undefined/SC – no meal package
		- BB – Bed & Breakfast
		- HB – Half board (breakfast and one other meal – usually dinner)
		- FB – Full board (breakfast, lunch and dinner)

'country':
	- Country of origin. Categories are represented in the ISO 3155–3:2013 format

'market_segment':
	- Market segment designation. In categories, the term “TA” means “Travel Agents” and “TO” means “Tour Operators”

'distribution_channel':
	- Booking distribution channel. The term “TA” means “Travel Agents” and “TO” means “Tour Operators”

'is_repeated_guest'
	- Value indicating if the booking name was from a repeated guest (1) or not (0)

'previous_cancellations'
	- Number of previous bookings that were cancelled by the customer prior to the current booking

'previous_bookings_not_canceled'
	- Number of previous bookings not cancelled by the customer prior to the current booking

'reserved_room_type'
	- Code of room type reserved. Code is presented instead of designation for anonymity reasons.

'assigned_room_type'
	- Code for the type of room assigned to the booking. 
	  Sometimes the assigned room type differs from the reserved room type due to hotel operation reasons (e.g. overbooking) or by customer request. 
	  Code is presented instead of designation for anonymity reasons.


'booking_changes'
	- Number of changes/amendments made to the booking from the moment the booking was entered on the PMS until the moment of check-in or cancellation

'deposit_type'
	- Indication on if the customer made a deposit to guarantee the booking. This variable can assume three categories: 
		- No Deposit – no deposit was made
		- Non Refund – a deposit was made in the value of the total stay cost
		- Refundable – a deposit was made with a value under the total cost of stay

'agent'
	- ID of the travel agency that made the booking

'company'
	- ID of the company/entity that made the booking or responsible for paying the booking. ID is presented instead of designation for anonymity reasons

'days_in_waiting_list'
	- Number of days the booking was in the waiting list before it was confirmed to the customer

'customer_type'
	- Type of customer

'adr'
	- Average Daily Rate as defined by dividing the sum of all lodging transactions by the total number of staying nights

'required_car_parking_spaces'
	- Number of car parking spaces required by the customer

'total_of_special_requests'
	- Number of special requests made by the customer (e.g. twin bed or high floor)

'arrival_date'
	- Date of arrival

'booking_date'
	- Date of reservation

'type'
	- Internal code for the reservation type

'reservation_type_code'
	- Another internal code for the reservation type

```

- Total number of rows in data: 100000
- Total number of columns: 28
  
## Data Cleaning and Feature Engineering

### (1) Removing Duplicate rows
All duplicate rows were dropped.

### (2) Handling null values
- Null values in columns `company` and `agent` were replaced by 0.
- Null values in column `country` were replaced by 'unknown'.
- Null values in column `children` were replaced by the mean of the column.
  

### (3) Converting columns to appropriate data types

- Changed data type of `children`, `company`, `agent` to int type.
- Changed data type of `arrival_date`, `booking_date` to datetime.

### (4) Removing outliers

- detected out of the ordinary minima in 'adr'
- detected quite out of the ordinary maximums in 'adults', 'children' and 'babies' when compared to their mean
- we maintain numbers of real guests and that make sense in the hotel sector
- records without any host, there is also no point in keeping them
- we leave the average price per room positive


### (5) Creating new columns
- Created new column `guests` by adding `adults`+`children`+`babies`.
- Created new column `year` doing the corresponding conversion of the 'arrival date' column with the datetime library
- Created new column `month` doing the corresponding conversion of the 'arrival date' column with the datetime library
- Created new column `days_in_advance`, I have created the column "days in advance" making the difference between `arrival_date` and `booking date`

## Exploratory Data Analysis

Performed EDA and tried answering the following questions:

```
 Q1) Which agent makes the most no. of bookings?
 Q2) Which room type is in most demand and which room type generatesthe  highest adr?
 Q3) Which meal type isthe  most preffered meal of customers?
 Q4) What isthe  percentage of bookings in each hotel?
 Q5) Which is the most common channel for booking hotels?
 Q6) Which are the most busy months?
 Q7) From which country most of the guests are comin ?
 Q8) How long do people stay at the hotels?
 Q9)  Which hotel seems to make more revenue?
 Q10)  Which hotel hasa  higher lead time?
 Q11)  What is preferred stay length in each hotel?
 Q12)  Which hotel has higher bookings cancellation rate.
 Q13)  Which hotel hasa  high chance that its customer will return for another stay?
 Q14)  Which channel is mostly used forthe  early booking of hotels?
 Q15)  Which channel hasa  longer average waiting time?
 Q16)  Which distribution channel brings betterrevenue-generatingg deals for hotels?
 Q17)  Which significant distribution channel has the highest cancellation percentage?
 Q18)  Does a  longer waiting period or longer lead time causes the cancellation of bookings?
 Q19)  Whether not getting allotted the same room type as demand is the main cause of cancellation for bookings?
 Q20)  Does not alloting the  same room as demanded affect adr? 
 Q21)  What is the trend of bookings within a month?
 Q22)  Which types of customers mostly make bookings?

```

Mainly performed using Matplotlib and Seaborn library and the following graph and plots had been used:
  -  Bar Plot.
  -  Histogram.
   - Scatter Plot.
   - Pie Chart.
   - Line Plot.
   - Heatmap.
     
###  General view:

We observe at first glance which variables are positively correlated:

* Cancellations usually coincide with previous cancellations
*Returning guests do not usually have previous cancellations
* The ADR (average rate) is related to adult and child guests, as well as the year and special requests
* Guests are usually adults and then children
* If there are babies, more special requests and more modifications to the reservation are made

### Conclusions:

The study provides several key conclusions based on the analysis of booking patterns and cancellation trends in City Hotel and Resort Hotel:

1. Booking and Cancellation Patterns: The majority of bookings are made for two persons. City Hotel experiences a higher rate of cancellations compared to Resort Hotel.

2. Customer Profile: The customer profile is predominantly made up of transient guests from Portugal. They often reserve Room Type A with BB category through Travel Agencies (TA) without requiring a deposit.

3. First-time Customers and Cancellations: First-time customers are more likely to cancel their reservations, while repeat guests tend to keep their bookings intact.

4. Wait Time: The average wait time on the reservation list is around 2-3 days.

5. Cancellations and Advance Reservations: Cancellations occur more frequently for reservations made well in advance. Interestingly, canceled reservations tend to have a higher Average Daily Rate (ADR), suggesting that customers might find more competitive rates elsewhere during that period and thus decide to cancel.

6. Historical Trends: June 2016 had the highest average cancellation rate, while June 2015 had the highest average number of reservations.

7. Preferred Booking Channel and Guest Origin: Travel Agencies (TA) and Tour Operators (TO) are the popular booking channels, and European guests, especially from Portugal, form a significant portion of the clientele.

8. Tailoring Services: Hotels can focus on improving customer retention and tailor their services to meet the needs of couples, as they are the most common type of guests.

9. Optimizing GDS Channel: Optimizing the GDS channel could lead to better ADR deals and increased revenue for both hotels.

10. Attracting Longer Stays: Hotels can entice customers planning longer stays with better deals featuring lower ADRs, creating an opportunity to attract this specific segment of clientele.

Overall, the study provides valuable insights that hotels can utilize to enhance their strategies, attract more guests, and improve overall customer satisfaction.
  

