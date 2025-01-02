# SQLStratascratch - Easy
All solutions - PostgreSQL

## Question 1:
### [Find the most common grade earned by bakeries](https://platform.stratascratch.com/coding/9703-find-the-most-common-grade-earned-by-bakeries?code_type=1)

Table name: los_angeles_restaurant_health_inspections

Columns: activity_date: date
employee_id: text
facility_address: text
facility_city: text
facility_id: text
facility_name: text
facility_state: text
facility_zip: text
grade: text
owner_id: text
owner_name: text
pe_description: text
program_element_pe: bigint
program_name: text
program_status: text
record_id: text
score: bigint
serial_number: text
service_code: bigint
service_description: text

### **Solution 1:**

    select count(grade), grade from los_angeles_restaurant_health_inspections
    where program_name like '%BAKERY%'

group by grade;

Output 1:

![image](https://github.com/user-attachments/assets/630ce6cf-32f7-41bb-875b-576032563bb1)

## Question 2: 

### [Calculate Average Score](https://platform.stratascratch.com/coding/10540-calculate-average-score?code_type=1)

Calculate the average score for each project, but only include projects where more than one team member has provided a score.
Your output should include the project ID and the calculated average score for each qualifying project.

Table name: project_data

![image](https://github.com/user-attachments/assets/1dc29936-ac0c-47cd-b62d-17811ab3839e)

### **Solution 2:**

    select project_id, AVG(score) As average_score from project_data
    
    where team_member_id > 1
    
    group by project_id
    
    order by AVG(score) desc;

Output 2:

![image](https://github.com/user-attachments/assets/9b36ebdb-9af3-42dd-ab95-279daed67c82)

## Question 3: 

### [User Activity Count](https://platform.stratascratch.com/coding/10539-user-activity-count?code_type=1)

Count the unique activity types for each user, ensuring users with no activities are also included.
The output should show each user's ID and their activity type count, with zero for users who have no activities.

Tables: user_profiles, activity_log

![image](https://github.com/user-attachments/assets/a5f3906b-775a-49f8-b0db-f486f9f3c4d4)

### **Solution 3:**

    select u.user_id, count(DISTINCT a.activity_type) as at_count from user_profiles u
    
    left join activity_log a on u.user_id = a.user_id
    
    group by u.user_id;

Output 3: 

![image](https://github.com/user-attachments/assets/02f484fd-bfa4-4503-a735-ad8a10f9ae08)

## Question 4:

### [Aggregate Listening Data](https://platform.stratascratch.com/coding/10367-aggregate-listening-data?code_type=1)

You're tasked with analyzing a Spotify-like dataset that captures user listening habits.
For each user, calculate the total listening time and the count of unique songs they've listened to. In the database duration values are displayed in seconds. Round the total listening duration to the nearest whole minute.

Table: listening_habits

![image](https://github.com/user-attachments/assets/1213d05a-c47f-4a7d-98ab-9dc569471c3d)

### **Soltuon 4:**

    select user_id, count(DISTINCT song_id) as unique_songs, SUM(listen_duration)/60 as duration_in_seconds from listening_habits
    
    group by user_id;

Output 4: 

![image](https://github.com/user-attachments/assets/3faf42fa-cf72-4ffb-974f-5fcbfc00dfc6)

## Question 5: 

### [Weekly Orders Report](https://platform.stratascratch.com/coding/10363-weekly-orders-report?code_type=1)

For each week, find the total quantity across all orders of that week. Include only the orders that are from the first quarter of 2023.
The output should contain 'week' and 'quantity'.

Table: orders_analysis

![image](https://github.com/user-attachments/assets/98bb904b-3963-4cd4-bab4-01a19204458f)

### **Solution 5:**

    select week, sum(quantity) from orders_analysis
    
    where week between '2023-01-01' and '2023-04-30'
    
    group by week
    
    order by week asc;

Output 5:

![image](https://github.com/user-attachments/assets/fe27892d-c2ab-40b7-887b-75fce13342b6)

##Question 6:

### [Top Monthly Sellers](https://platform.stratascratch.com/coding/10362-top-monthly-sellers?code_type=1)

You are provided with an already aggregated dataset from Amazon that contains detailed information about sales across different products and marketplaces. Your task is to list the top 3 sellers in each product category for January. The output should contain 'seller_id' , 'total_sales' ,'product_category' , 'market_place', and 'sales_date'.

Table: sales_data

![image](https://github.com/user-attachments/assets/9a32f699-5270-4c00-b520-9d27c06a499d)

### **Solution 6:**

      with jan_sales as (select 
          seller_id, 
          sum(total_sales) as sales,
          product_category,
          market_place,
          sales_date from sales_data
          where sales_date between '2024-01-01' and '2024-01-31'
          group by 1,3,4, 5
          ),
      ranked_sellers as (select
          seller_id, 
          sales,
          product_category,
          sales_date,
          market_place,
          rank() over (PARTITION by product_category order by sales desc) as rank
          from jan_sales
    )   
    
    select seller_id, sales, product_category, market_place, sales_date
    
    from ranked_sellers
    
    where rank <=3;

![image](https://github.com/user-attachments/assets/1dcdf89f-3147-4e7d-a590-e626dbe7129f)

## Question 7:

### [Peak Online Time](https://platform.stratascratch.com/coding/10361-peak-online-time?code_type=1)

You are given a dataset from Amazon that tracks and aggregates user activity on their platform in certain time periods. For each device type, find the time period with the highest number of active users. The output should contain 'user_count', 'time_period', and 'device_type', where 'time_period' is a concatenation of 'start_timestamp' and 'end_timestamp', like ; "start_timestamp to end_timestamp".

Table: user_activity

![image](https://github.com/user-attachments/assets/7c71a0d4-17db-447e-90f0-8695412cc78a)

### **Solution 7:**

    select device_type, sum(user_count) as user_count, concat(start_timestamp,' to ', end_timestamp) as time_period from user_activity
    GROUP BY device_type, time_period
    ORDER BY user_count DESC
    limit 4;

![image](https://github.com/user-attachments/assets/8e1854e4-99c7-4b39-8813-853132e813ee)

## Question 8:

### [Number Of Unique Facilities And Inspections Per Municipality](https://platform.stratascratch.com/coding/9702-number-of-unique-facilities-and-inspections-per-municipality?python=&code_type=1)

Count the number of unique facilities per municipality zip code along with the number of inspections. Output the result along with the number of inspections per each municipality zip code. Sort the result based on the number of inspections in descending order.

Table: los_angeles_restaurant_health_inspections

![image](https://github.com/user-attachments/assets/13479c58-7238-452e-b314-32d78b0f6781)


### **Solution 8:**


    select facility_zip, count(DISTINCT facility_name) as unique_facilities, count(service_description) as total_inspections 
    from los_angeles_restaurant_health_inspections
    group by 1
    order by 3 desc;

![image](https://github.com/user-attachments/assets/e75e28d4-0d81-48b9-839e-67c7b41affd7)

























