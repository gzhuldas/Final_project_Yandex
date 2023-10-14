## Retail: Loyalty Program Analysis

## Technical Description:
Test name: recommender_system_test<br>
Groups: А (control), B (new payment funnel)<br>
Launch date: 2020-12-07<br>
Date when they stopped taking up new users: 2020-12-21<br>
End date: 2021-01-01<br>
Audience: 15% of the new users from the EU region<br>
Purpose of the test: testing changes related to the introduction of an improved recommendation system<br>
Expected result: within 14 days of signing up, users will show better conversion into product page views (the product_page event), instances of adding items to the shopping cart (product_cart), and purchases (purchase). At each stage of the funnel product_page → product_cart → purchase, there will be at least a 10% increase.<br>
Expected number of test participants: 6000<br>


## Data Description:
ab_project_marketing_events_us.csv — the calendar of marketing events for 2020<br>
final_ab_new_users_upd_us.csv — all users who signed up in the online store from December 7 to 21, 2020<br>
final_ab_events_upd_us.csv — all events of the new users within the period from December 7, 2020 through January 1, 2021<br>
final_ab_participants_upd_us.csv — table containing test participants<br>
Structure of ab_project__marketing_events_us.csv:<br>
name — the name of the marketing event<br>
regions — regions where the ad campaign will be held<br>
start_dt — campaign start date<br>
finish_dt — campaign end date<br>
Structure of final_ab_new_users_upd_us.csv:<br>
user_id<br>
first_date — sign-up date<br>
region<br>
device — device used to sign up<br>
Structure of final_ab_events_upd_us.csv:<br>
user_id<br>
event_dt — event date and time<br>
event_name — event type name<br>
details — additional data on the event (for instance, the order total in USD for purchase events)<br>
Structure of final_ab_participants_upd_us.csv:<br>
user_id<br>
ab_test — test name<br>
group — the test group the user belonged to<br>


## Plan EDA:

### Step 1. Open file and perform data preprocessing.

1. Change datatypes if needed
2. Fill NaN values if needed
3. Delete duplicate rows if needed

### Step 2. Perform Exploratory Data Analysis and calculate metrics.

#### Goal: Analyze store traffic.

1. Identify how many clients the store has daily/weekly/monthly, find monthly percentage change
2. Identify how many clients each shop has monthly
3. How often do the customers come back?
4. How often do the loyal program customers buy products? Do they return after one week, two weeks or is the pattern random?

#### Goal: Product analysis.

1. Identify how many clients have loyalty program
2. Identify which products loyalty program clients buy the most (How much revenue did each product bring?)
3. Identify which products non-loyalty program clients buy the most (How much revenue did each product bring?)

#### Goal: Analyze revenue changes.

1. Identify the weekly/monthly revenue
2. Identify top 10 products which were the most profitable
3. Identify top 10 shops by revenue
4. Make cohort analysis to identify: 1. number of orders, 2.average number of orders per customer, 3. average revenue per paying customer, 4.average revenue per customer


## A/B test Plan:

### Step 1. Preprocessing. Find and replace missing values, drop duplicates, change datatypes where needed.\
#### Step 2. EDA. Answer the questions and make conclusions:
1. Study conversion at different stages of the funnel.
2. Is the number of events per user distributed equally among the samples?
3. Are there users who are present in both samples?
4. How is the number of events distributed among days?
5. Are there any peculiarities in the data that you have to take into account before starting the A/B test?
6. Step 2 conclusion.
#### Step 3. A/B test. 
1. Analyze A/B test results.
2. Perform z-test. 
#### Conclusion
