# SQLStratascratch

[Find the most common grade earned by bakeries] (https://platform.stratascratch.com/coding/9703-find-the-most-common-grade-earned-by-bakeries?code_type=1)
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

Solution: PostgreSQL
select count(grade), grade from los_angeles_restaurant_health_inspections
where program_name like '%BAKERY%'
group by grade;
![image](https://github.com/user-attachments/assets/630ce6cf-32f7-41bb-875b-576032563bb1)
