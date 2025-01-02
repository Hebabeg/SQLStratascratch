# SQLStratascratch - Easy

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

Solution 1: PostgreSQL
select count(grade), grade from los_angeles_restaurant_health_inspections
where program_name like '%BAKERY%'
group by grade;

Output 1:

![image](https://github.com/user-attachments/assets/630ce6cf-32f7-41bb-875b-576032563bb1)

### Question 2: 

## [Calculate Average Score](https://platform.stratascratch.com/coding/10540-calculate-average-score?code_type=1)

Table name: project_data

![image](https://github.com/user-attachments/assets/1dc29936-ac0c-47cd-b62d-17811ab3839e)

Solution 2: 
select project_id, AVG(score) As average_score from project_data
where team_member_id > 1
group by project_id
order by AVG(score) desc;

Output 2:

![image](https://github.com/user-attachments/assets/9b36ebdb-9af3-42dd-ab95-279daed67c82)

### Question 3: [User Activity Count](https://platform.stratascratch.com/coding/10539-user-activity-count?code_type=1)

Tables: user_profiles, activity_log

![image](https://github.com/user-attachments/assets/a5f3906b-775a-49f8-b0db-f486f9f3c4d4)

Solution 3:
select u.user_id, count(DISTINCT a.activity_type) as at_count from user_profiles u
left join activity_log a on u.user_id = a.user_id
group by u.user_id;

Output 3: 

![image](https://github.com/user-attachments/assets/02f484fd-bfa4-4503-a735-ad8a10f9ae08)

