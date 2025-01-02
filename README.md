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

### **Soltuon 4: **

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
