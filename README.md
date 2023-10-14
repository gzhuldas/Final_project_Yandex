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

#### Step 1. Preprocessing. Find and replace missing values, drop duplicates, change datatypes where needed.
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

## Examples of graphs:

![image](https://github.com/gzhuldas/Final_project_Yandex/assets/72769986/490520f2-6bb9-4683-bf3b-e193c00fa5f7)

![image](https://github.com/gzhuldas/Final_project_Yandex/assets/72769986/dcd76941-3698-44e6-aa30-607dd325ec97)

![image](https://github.com/gzhuldas/Final_project_Yandex/assets/72769986/5b6fca5c-af1a-493e-b73d-7913a3a503a1)

![image](https://github.com/gzhuldas/Final_project_Yandex/assets/72769986/da2d49f1-40fc-443c-a38a-c09e7c475da4)

![image](https://github.com/gzhuldas/Final_project_Yandex/assets/72769986/de796be2-13e9-43aa-8caa-b86e3a98ef56)

![image](https://github.com/gzhuldas/Final_project_Yandex/assets/72769986/39a74a46-5e34-447f-a24f-acbeb62e6fa0)

![image](https://github.com/gzhuldas/Final_project_Yandex/assets/72769986/d1883f76-866c-4aa7-a1a3-82223028121c)

![image](https://github.com/gzhuldas/Final_project_Yandex/assets/72769986/aea32ad0-07ed-470b-9a2a-67eda215242a)


#### Conclusion
The loyalty program has shown to be quite successful as clients who sighed up for it actually are more consistent and make as big and sometimes even bigger purchases than the general customers.Unfortunately, it was not possible to identify which offers, discounts and products were exclusive to loyalty program customers but it seems like the most popular products among these clients are available for general customers as well.LPCs are very consistent and most of them bought products on a regular basis, the analysis identified at least 20 people who made more than 5 purchases, all of them are probably LPCs.Even though the cohort analysis has shown that the number of customers decreased each consecutive month  (except for December cohort when some clients returned in February), the average transactions number stayed the same or even increased for some months.

The EDA was divided into following steps: events funnel, number of events per user, events distribution among days and search for peculiarities in the data. The funnel analyzed in this project showed the number of times one user went through one stage, i.e. one user could have logged in multiple times and it is still represented in the funnel. Counting unique or nonunique user ids at each funnel stage does not change one important observation - according to the funnel the final step 'purchases' has larger number of users than the previous step 'product cart'. This is probably due to the 'Buy Now' button or other options which can offer users to buy products skipping some steps and go directly to the purchase stage. 

The number of events were analyzed for AB groups. Group B has much less users but the average amount of events per user is comparable to that of group A, which means that users from group B visit the site more often. There are no users who are present in both groups. The number of events ditribution among days showed that it was decreasing till 2020-12-13 and then it spiked and continued to increase till 2020-12-21, which is due to the fact that no new users were accepted for the test. Right after Christmas Eve the number of events gradually decreased to 0.

There were users who skipped some steps as well as those who went through all of them. The data investigation showed that some users skipped all steps and went directly to the purchase stage. Some part of users skipped product cart stage. The data actually has two funnel stage types: login->product_page->purchase and login->product_page->product_cart->purchase. These peculiarities in the dataset were taken into account before hypothesis testing

Hypotheses testing part includes 4 hypotheses which correspond to each funnel stage. Daily conversion rate graphs were analyzed for two groups. Group B showed better results for some conversion stages, more specifically product_page->product_cart and product_page->purchase. In general the graphs are a little distorted as the data was not divided into different funnel types. 

The statistical significance of difference between groups' conversion rates was checked. According to the test group A showed better results for these stages of funnel: login -> product page and product page -> purchase. Other funnel stages did not show any statistical difference. This means that the expected results were not achieved and the company should should stop the test since the expected number of participants was reached and the test did not show desirable results.

