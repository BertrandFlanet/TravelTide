![TravelTide](https://drive.google.com/file/d/1KAPQTQxOPgKmgdPhCcyZ-0JzeArO4emD/view?usp=sharing)

# **TravelTide**
## Segmentation_project

### **1 - Introduction**

The main aim of this project is to segment TravelTide user base.
TravelTide is a - fictitious - travelling company that provides an easy-of-use service to book hotel and flight.
In this project, TravelTide user base is composed of USA and Canada citizens.
We conducted two users segmentation, following an RFM and a branching logic.
Additionally we ran a clustering using K-means.
By categorizing users into segments based on behavior inferences, we are able to design perks to attribute to each of the generated groups.
These perks helps us develop marketing strategies to better answer users' needs and interests.


### **2 - Table of Contents**

- [1 - Introduction](#1---introduction)
- [2 - Table of Contents](#2---table-of-contents)
- [3 - Usage](#3---usage)
- [4 - Project Structure](#4---project-structure)
- [5 - Data](#5---data)
- [6 - Analysis](#6---analysis)
- [7 - Results](#7---results)
- [8 - Vizualisations](#8---vizualisations)
- [9 - Conclusions](#9---conclusions)
- [10 - Acknowledgement](#10---acknowledgement)
- [11 - Contact](#11---contact)


### **3 - Usage**

 .ipynb:
Google Colab: Upload directly via the "File" menu or open from Google Drive
Jupyter Notebook: Install Jupyter, start it via terminal, and open the .ipynb file through the interface

 .twb:
Open with Tableau - Tableau Public installation - https://public.tableau.com/


### **4 - Project Structure**

- `data/`: Reference to dataset and used aggregated dataset at various granularity level
- `notebooks/`: Jupyter notebooks with the analysis/segmentation code
- `results/`: Output files, results, project report, .ppt presentation
- `README.md`: Project documentation

### **5 - Data**
TravelTide dataset cannot be shared for privacy reasons.
Although, we can share its structure:
- `flights`<br>
	. trip_id<br>
	. origin_airport<br>
	. destination<br>
	. destination_airport<br>
	. seats<br>
	. return_flight_booked<br>
	. departure_time<br>
	. return_time<br>
	. checked_bags<br>
	. trip_airline<br>
	. destination_airport_lat<br>
	. destination_airport_lon<br>
	. base_fare_usd<br>
- `hotels`<br>
	. trip_id<br>
	. hotel_name<br>
	. nights<br>
	. rooms<br>
	. check_in_time<br>
	. check_out_time<br>
	. hotel_per_room_usd<br>
- `sessions`<br>
	. session_id<br>
	. user_id<br>
	. trip_id<br>
	. session_start<br>
	. session_end<br>
	. flight_discount<br>
	. hotel_discount<br>
	. flight_discount_amount<br>
	. hotel_discount_amount<br>
	. flight_booked<br>
	. hotel_booked<br>
	. page_clicks<br>
	. cancellation<br>
- `users`<br>
	. user_id<br>
	. birthdate<br>
	. gender<br>
	. married<br>
	. has_children<br>
	. home_country<br>
	. home_city<br>
	. home_airport<br>
	. home_airport_lat<br>
	. home_airport_lon<br>
	. sign_up_date<br>


[df_base_sessions.csv]
Aggregation at session level.
Preprocessing:
- Filtering by date: > 2023-01-04
- Filtering by threshold: users who had at least 7 sessions
- Removing duplicate trip references
- Imputing 0 to users who have a negative count of night stays
- Imputing difference between departure and return times for users who completed trip, had a hotel booked but a count of night stay of 0

Feature engineering:
- Creation of metrics for defining thresholds to segment users
. Age
. Month
. Distance
. domestic/international
. Spending per trip w/o_discount if not cancelled - total_spent_w/o_discount_not_cancelled
. Spending per trip w/o_discount if cancelled - total_spent_w/o_discount_cancelled
. Spending per trip with discount if not cancelled - total_spent_discount_not_cancelled
. Spending for hotel w/o_discount if not cancelled - hotel_total_w/o_discount_not_cancelled
. Spending for hotel w/o_discount if cancelled - hotel_total_w/o_discount_cancelled
. Spending for hotel with discount if not cancelled - hotel_total_discount_not_cancelled
. Time diff from end session and departure time(hours)
. Trip duration(hours)
. Session duration (minutes)
. Time between one session and another


[users_base_v2.csv]
Aggregation at user level:
Feature engineering:

TIME:
- Time diff sign_up_date / first_session_start (hour) - t1
- Average trip duration (hour) - from departure to return - t2
- Total trips duration (hour) - from departure to return - t3
- Rate clicks per session_time if trip_booked (minute) - t4
- Rate clicks per session_time if trip_not_booked (minute) - t5
- Avg time diff from end session and departure time (hour) - t6
- Time diff since lastest booked trip (if not cancelled) (hour) - t7
- Time diff since lastest booked trip (if cancelled) (hour) - t8
- Average Time between one booked trip and next trip - t57


DISTANCE:
- Total travelled distance - sum(haversine) - t9
- Average travelled distance per trip - t10
- Rate Price per km(distance) -with discount - t11
- Rate Price per km(distance) -without discount - t12
- Most travelled destination - if count of destination appears > 1 - t13
- Most travelled destination count - if count of destination appears > 1 - t14
- Count of Domestic trips - t15
- Count of International trips - t16
- Ratio domestic/international - t17
- Ratio total distance travelled/#of night(if not cancelled) - t18
- Ratio total distance travelled/#of night(if cancelled) - t19


GENERAL: FLIGHT and HOTEL:
- age bins definition - t177
- Rate Return flight booked - t20
- Rate Return flight not booked - t21
- Ratio #session/#trips (if not cancelled) - t22
- Ratio #session/#trips (if cancelled) - t23
- Number of booked trip (if not cancelled) - t24
- Number of completed trips (cancelled) - t25
- Most booked hotel - t26
- Most booked hotel count - t27
- Most used airlines (mode) - t28
- Most used airlines count - t29
- avg Luggage per trip - t30
- Total luggage - t31
- Ratio checked_bags / trip - t32
- Ratio #bags/seat AS #_bags_per_person(if not cancelled) - t33
- Ratio #bags/seat AS #_bags_per_person(if cancelled) - t34
- Ratio #_bags_per_person/nights(if not cancelled) - t35
- Ratio #_bags_per_person/nights(if cancelled) - t36
- Number of nights - total - t37
- Number of nights (if not cancelled) - t38
- Number of nights (if cancelled) - t39
- Number of rooms - total - t40
- Number of rooms (if not cancelled) - t41
- Number of rooms (if cancelled) - t42
- Number of seats - total - t43
- Number of seats (if not cancelled) - t44
- Number of seats (if cancelled) - t45
- only stayed at hotel, count of stays - t162
- only stayed at hotel, count of stays if discount - t163
- only stayed at hotel, count of stays if no discount - t164
- only stayed at hotel, num of nights - t165
- only stayed at hotel, mean num of nights - t166
- only stayed at hotel, total spent - t167
- only stayed at hotel, avg spent - t168
- only flight, count of stays - t169
- only flight, count of stays with discount - t170
- only flight, count of stays without discount - t171
- only flight, ratio domestic/international - t172
- only flight, distance travelled - t173
- only flight at hotel, distance travelled average - t174
- only flight at hotel, total spent - t175
- only flight at hotel, average spent - t176


DISCOUNT USE:
- Total spent (w/o discount) - t46
- Total avg spent (w/o discount) - t47
- Total spent (with discount) - t48
- Total avg spent (with discount) - t49
- Total discount - t50
- Total discount per hotel - sum(discount hotel) - t52
- Total discount per flight - sum(discount flight) - t52
- Ratio Total cost/Total discount - t53
- Ratio num of discount/#trips - t54
- Ratio num of discount/flight - sum(discountflight) / count(trip_id) - t55
- Ratio num of discount/hotel - sum(discounthotel) / count(trip_id) - t56


SEASONALITY (by season and month):
- Number of trip per month
	- t57
	- t58
	- t59
	- t60
	- t61
	- t62
	- t63
	- t64
	- t65
	- t66
	- t67
	- t68
- Number of trip per season - spring - t69
- Number of trip per season - summer - t70
- Number of trip per season - autumn - t71
- Number of trip per season - winter - t72
- Most travelled destination by month - january - t73
- Most travelled destination by month (count) - january - t74
- Most travelled destination by month - february - t75
- Most travelled destination by month (count)- february - t76
- Most travelled destination by month - march - t77
- Most travelled destination by month (count) - march - t78
- Most travelled destination by month - april - t79
- Most travelled destination by month (count) - april - t80
- Most travelled destination by month - may - t81
- Most travelled destination by month (count) - may - t82
- Most travelled destination by month - june - t83
- Most travelled destination by month (count) - june - t84
- Most travelled destination by month - july - t85
- Most travelled destination by month (count) - july - t86
- Most travelled destination by month - august - t87
- Most travelled destination by month (count) - august - t88
- Most travelled destination by month - september - t89
- Most travelled destination by month (count) - september - t90
- Most travelled destination by month - october - t91
- Most travelled destination by month (count) - october - t92
- Most travelled destination by month - november - t93
- Most travelled destination by month (count) - november - t94
- Most travelled destination by month - december - t95
- Most travelled destination by month (count) - december (- t96
- Most travelled destination by season - spring - t97
- Most travelled destination by season - spring - t98
- Most travelled destination by season - summer - t99
- Most travelled destination by season - summer - t100
- Most travelled destination by season - autumn - t101
- Most travelled destination by season - autumn - t102
- Most travelled destination by season - winter - t103
- Most travelled destination by season - winter - t104
- count of booked night per month - (january) - t105
- count of booked night per month - (february) - t106
- count of booked night per month - (march) - t107
- count of booked night per month - (april) - t108
- count of booked night per month - (may) - t109
- count of booked night per month - (june) - t110
- count of booked night per month - (july) - t111
- count of booked night per month - (august) - t112
- count of booked night per month - (september) - t113
- count of booked night per month - (october) - t114
- count of booked night per month - (november) - t115
- count of booked night per month - (december) - t116
- count of booked night per season - spring - t117
- count of booked night per season - summer - t118
- count of booked night per season - autumn - t119
- count of booked night per season - winter - t120
- count of seats per month:
	- t121
	- t122
	- t123
	- t124
	- t125
	- t126
	- t127
	- t128
	- t129
	- t130
	- t131
	- t132
- count of seats per season
	- t133
	- t134
	- t135
	- t136
- count of bags per month:
	- t137
	- t138
	- t139
	- t140
	- t141
	- t142
	- t143
	- t144
	- t145
	- t146
	- t147
	- t148
- count of bags per season - spring - t149
- count of bags per season - summer - t150
- count of bags per season - autumn - t151
- count of bags per season - winter - t152
- ratio international/domestic trips - t153
- ratio international/domestic trips per season:
	- t154
	- t155
	- t156
	- t157
- ratio checked_bags/seats per season:
	- t158
	- t159
	- t160
	- t161


[TD_segmentation_final.csv]
Final segmentation, labels and perks
Preprocessing
Imputing 0 for Nan


### **6 - Analysis**

The analysis was conducted in the following steps:
1. **Exploratory Data Analysis (EDA)**: Identified key patterns and trends in the data.
2. **Feature Engineering**: Created new features to facilitate definition of thresholds and metrics
3. **RFM**: Conducted a Recency, Frequency, Monetary segmenting
4. **Segmentation by branching**: Conducted a segmentation with a branching method
5. **Perks**: Attributed perks to each generated groups
3. **Extra: Clustering**: Applied K-Means clustering to segment customers into distinct groups.


### **7 - Results**

RFM segmentation:
`'lost'` : 'Conduct surveys or feedback sessions to understand why they stopped purchasing and address any concerns.',
`'hibernating'` : 'Reach out with personalized win-back offers or discounts to encourage them to return.',
`'loyal_customers'`: 'Exclusive loyalty rewards such as early access to new products, VIP events, or special discounts.',
`'at_risk'`: 'Implement targeted re-engagement campaigns to remind them of your value proposition.',
`'potential_loyalists'`: 'Provide personalized incentives to make the leap to loyal customer status, such as double loyalty points or exclusive previews.',
`'about_to_sleep'`: 'Offer loyalty rewards or VIP programs to further incentivize their frequent purchases. ',
`'one timer'`: 'Implement an onboarding email series to introduce them to your products/services.',
`'cant_lose'`: 'Provide exclusive offers or early access to new products/services to maintain their engagement.',
`'champions'`: 'Encourage them to become brand advocates by offering referral bonuses or social media shoutouts.',
`'promising'`: 'Offer incentives for increasing their frequency of purchases, such as referral bonuses or points-based rewards.',
`'need_attention'`: 'Provide targeted offers or personalized customer service interactions to address any issues and encourage further purchases.',
`'new_customers'`: 'Welcome them with a special discount or promotion for their next purchase.'})


Branching segmentation:
User's behaviour segmentation labels and perks:

Multi Traveler                  - `Lambda Traveller` - Last-Minute Deals
Multi Solo Business Short       - `Business expeditive` (short trip) - Partnership discounts for companies that book frequently.
Multi Solo Business Long        - `Business expansive` (long trip) - Reduced rates for long-term hotel stays.
Multi Solo Adventurer Short     - `Solo Casual Traveller` (short trip) - Short trip packages for popular destinations.
Multi Solo Adventurer Long      - `Solo Adventurer` (long trip) - Packages with activities like hiking, diving, and cultural tours.
Multi Group Family Short        - `Familly Excursion` (familly short trip) - Reduced rates for accommodation, meals, and activities.
Multi Group Family Long         - `Familly Adventure` (familly long trip) - Packages with activities such as safaris, theme parks, and outdoor adventures.
Multi Group Separate Short      - `Friend Relaxer` (friends short trip) - Discounts for bookings on short stays.
Multi Group Separate Long       - `Friend Explorer` (friends long trip) - Reduced rates for extended stays.
Multi Group Unite Long          - `Intimate Odysseus` (possible couple or close friends long trip) - Packages with activities like wine tastings, city tours, and spa treatments.
Multi Group Unite Short         - `Intimate Escapade` (possible couple or close friends short trip) - Special rates on short stays.
inactive hopeful                - `inactive fluid` (users who are active on the website but never complied to a trip) - Personalized travel recommendations and discounts to encourage booking.
inactive hopeless               - `inactive frozen` (users who are inactive for a long time) - Automatic enrollment in a loyalty program with immediate benefits to encourage re-engagement.
Unique Traveler                  - `Hapax Traveller` - Offer discounts or rewards for referring friends or family to book trips.
Unique Solo Adventurer Short     - `Solo Tempted Traveller` (short trip) - Exclusive weekend getaway offers for returning customers.
Unique Solo Adventurer Long      - `Solo Curious Adventurer` (long trip) - Discounts on long trips to adventurous destinations for repeat customers.
Unique Group Family Long         - `Familly Mousy Adventure` (familly long trip) - Free baggage.
Unique Group Separate Long       - `Friend Future Explorer` (friends long trip) - Reduced rates on trips for repeat bookings.
Unique Group Unite Short         - `Intimate Aluring Escapade` (possible couple or close friends short trip) - Discounts on spa retreats, dinners.


Clustering with K-Means:
Did provide some results, segmenting users into 3 or 4 groups.
Although, these weren't deemed substantial to be considered.
Nota: it will be sensical to run more experiment with this model if time allows.


### **8 - Visualizations**

Tableau files and visualizations located in:
`results/`


### **9 - Conclusions**

We believe that the proposed system offers solid inferences for our users behavior, as well as complementary intel upon our users health through RFM.
It still requires testing as we need to make sure that the perks we associated with each group correspond to their needs and will translate into a growing activity.
Thus, an A/B test could be performed, testing our proposed perks against randomly attributed perks.
We had also suggest polling our users: enticing them with offers for answering upon their travel habits and preferred perks.

The proposed ramified system could be expanded and scaled if the users base grows.
Other metrics could be considered to produce more adequate segmentations, such as: use of discount; seasonality; destinations; use of airlines; users who only booked hotels or flights.

During our EDA we also noticed areas where TravelTide service could be improved.
Gender: dramatic difference between genders that see almost 90% of our users being female. 
It is below the average standard (80%) and could be investigated further
International vs Domestic travels: we have an almost ⅔ ratio of trip made domestically. 
We would recommend investigating on the reason of such proportion, for possibly unlocking an increase in international travels.
Seasonality: extremely low count of trip recorded in Autumn. 
It is likely due to the threshold we have set for our segmentation, but nonetheless, the figures look concerningly low. This could be another area for improvement.


### **10 - Acknowledgement**

Project made within the frame of Masterschool bootcamp - 07/2024.

### **11 - Contact**

Bertrand Flanet
E-mail: bertrand.flanet@gmail.com
linkedIn: https://www.linkedin.com/in/bertrand-flanet-67b1b2299/
