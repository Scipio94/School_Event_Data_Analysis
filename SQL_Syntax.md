### 1. What is the student population at each campus?
~~~SQL
SELECT  
  CASE 
  WHEN grade BETWEEN 0 AND 2 THEN 'PS'
  WHEN grade BETWEEN 3 AND 5 THEN 'IS'
  WHEN grade BETWEEN 6 AND 8 THEN 'MS'
  WHEN grade BETWEEN 9 AND 12 THEN 'HS'
  END as Campus,COUNT(School_ID) AS School_Population,ROUND(COUNT(School_ID)/1033.00 * 100,0) as School_Population_percentage,RANK () OVER (ORDER BY COUNT(School_ID) DESC ) as Rank
FROM `my-data-project-36654.BTS_Data_Project.BTS_Dataset` 
GROUP BY 
  Campus
ORDER BY 
  School_Population DESC
--1033 is the total student count
~~~

### 2. What is the demographic information of the students enrolled in the school network?
~~~SQL
SELECT
  ethnicity,COUNT(School_ID) AS Ethnicity_Count, ROUND(COUNT(school_id)/1033.00 * 100,0) AS Ethnicity_Percentage
FROM `my-data-project-36654.BTS_Data_Project.BTS_Dataset`
GROUP BY
  Ethnicity 
~~~

### 3. What is the demographic information of each campus?

~~~SQL
SELECT  
CASE 
  WHEN grade BETWEEN 0 AND 2 THEN 'PS'
  WHEN grade BETWEEN 3 AND 5 THEN 'IS'
  WHEN grade BETWEEN 6 AND 8 THEN 'MS'
  WHEN grade BETWEEN 9 AND 12 THEN 'HS' 
  END as Campus,Ethnicity,COUNT(school_id) as Ethnicity_Count
FROM `my-data-project-36654.BTS_Data_Project.BTS_Dataset`
GROUP BY 
  Campus, Ethnicity
ORDER BY 
  Campus 
 ~~~
### 4. What percentage of students were present at the event?
~~~SQL
SELECT  
ROUND(COUNT(School_ID)/1033.00 * 100,1) AS Network_Attendance_Percentage
FROM `my-data-project-36654.BTS_Data_Project.BTS_Dataset` 
WHERE  
  Attended IS true 

-- 394 is the number of students that attended the event in total
-- 1033 is the student population
~~~
### 5. What was the demographic information of the students that attended the event?
~~~SQL
SELECT  
  ethnicity,ROUND(COUNT(School_ID)/394.00 * 100,1) AS Network_Attendance_Percentage
FROM `my-data-project-36654.BTS_Data_Project.BTS_Dataset` 
WHERE  
  Attended IS true 
GROUP BY 
  Ethnicity
-- 394 is the number of students that attended the event in total
~~~

### 6. What was the demographic information of the students that attended the event at each campus ?

~~~SQL
SELECT  
  CASE 
  WHEN grade BETWEEN 0 AND 2 THEN 'PS'
  WHEN grade BETWEEN 3 AND 5 THEN 'IS'
  WHEN grade BETWEEN 6 AND 8 THEN 'MS'
  WHEN grade BETWEEN 9 AND 12 THEN 'HS'
  END as Campus,COUNT(School_ID) AS School_Attendance,ROUND(COUNT(School_ID)/394 * 100,0) as School_Attendance_Percentage, RANK () OVER (ORDER BY COUNT(School_ID) DESC ) as  Rank
FROM `my-data-project-36654.BTS_Data_Project.BTS_Dataset` 
WHERE 
  Attended IS true
GROUP BY 
  Campus
ORDER BY
  School_Attendance DESC

-- 394 is the number of students that attended the event in total
~~~
### 7. What were the language preferences of the students that attended the events at each campus?
~~~ SQL
SELECT 
 COUNT(School_ID) as Langauge_English_Count, ROUND(COUNT(School_ID)/ 394.00 * 100,0) as  Langauge_English_Percentage 
FROM `my-data-project-36654.BTS_Data_Project.BTS_Dataset` 
WHERE 
  English IS true AND Attended IS true

-- 291 English
~~~

~~~ SQL
SELECT 
COUNT(School_ID) as Language_Spanish_Count, ROUND(COUNT(School_ID)/394.00 * 100,0) as  Language_Spanish_Percentage
FROM `my-data-project-36654.BTS_Data_Project.BTS_Dataset` 
WHERE 
 Spanish IS true AND Attended IS true

 -- 91 Spanish
~~~
