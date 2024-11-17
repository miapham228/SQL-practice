# SQL-practice
1. My answer for SQL excercises EASY PART
Q1 Show first name, last name, and gender of patients whose gender is 'M'

`SELECT first_name, last_name, gender
FROM patients
WHERE gender='M'`

Q2 Show first name and last name of patients who does not have allergies. (null)

`SELECT first_name, last_name
FROM patients
WHERE allergies is null`

Q3 Show first name of patients that start with the letter 'C'

`SELECT first_name
FROM patients
WHERE first_name like "C%"`

Q4 Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)

`SELECT first_name, last_name
FROM patients
WHERE weight >= 100 and weight <= 120`

Q5 Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'

`UPDATE patients
SET allergies = 'NKA'
WHERE allergies is NULL;`

Q6 Show first name and last name concatinated into one column to show their full name.

`SELECT CONCAT(first_name, " ", last_name) as full_name
FROM patients`

Q7 Show first name, last name, and the full province name of each patient. Example: 'Ontario' instead of 'ON'

`SELECT patients.first_name, patients.last_name, province_names.province_name
FROM patients
JOIN province_names
ON patients.province_id = province_names.province_id`

Q8 Show how many patients have a birth_date with 2010 as the birth year.

`SELECT COUNT(birth_date)
FROM patients
WHERE YEAR(birth_date) is 2010`

Q9 Show the first_name, last_name, and height of the patient with the greatest height.

`SELECT first_name, last_name, max(height) 
FROM patients`

Q10 Show all columns for patients who have one of the following patient_ids: 1,45,534,879,1000

`SELECT *
FROM patients
WHERE patient_id in (1,45,534,879,1000)`

Q11 Show the total number of admissions

`SELECT COUNT(patient_id)
FROM admissions`

Q12 Show all the columns from admissions where the patient was admitted and discharged on the same day.

`SELECT *
FROM admissions
WHERE discharge_date = admission_date`

Q13 Show the patient id and the total number of admissions for patient_id 579.

`SELECT patient_id, COUNT(patient_id)
FROM admissions
WHERE patient_id = 579`

Q14 Based on the cities that our patients live in, show unique cities that are in province_id 'NS'?

`SELECT DISTINCT(city)
FROM patients
WHERE province_id = "NS"`

Q14 Write a query to find the first_name, last name and birth date of patients who has height greater than 160 and weight greater than 70

`SELECT first_name, last_name, birth_date
FROM patients
WHERE height > 160 and weight > 70`

Q15 Write a query to find list of patients first_name, last_name, and allergies where allergies are not null and are from the city of 'Hamilton'

`SELECT first_name, last_name, allergies
FROM patients
WHERE allergies NOT null and city is "Hamilton"`

2. My answer for SQL excercises MEDIUM PART

Q1 Show unique birth years from patients and order them by ascending.

`SELECT DISTINCT(YEAR(birth_date)) 
FROM patients
ORDER BY birth_date ASC`

Q2 Show unique first names from the patients table which only occurs once in the list. For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. If only 1 person is named 'Leo' then include them in the output.

`SELECT first_name
FROM patients
GROUP BY first_name
HAVING COUNT(*) = 1`

Q3 Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.
`SELECT
  patient_id,
  first_name
FROM patients
WHERE
  first_name LIKE 's%s'
  AND len(first_name) >= 6;`

Q4 Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'.

`SELECT
  patients.patient_id,
  first_name,
  last_name
FROM patients
  JOIN admissions ON admissions.patient_id = patients.patient_id
WHERE diagnosis = 'Dementia';`

Q5 Display every patient's first_name.
Order the list by the length of each name and then by alphabetically.

`SELECT first_name
FROM patients
order by
  len(first_name),
  first_name;`

Q6 Show the total amount of male patients and the total amount of female patients in the patients table.
Display the two results in the same row.

`SELECT
(SELECT COUNT(*) FROM patients WHERE gender IS 'M') AS male_count,
(SELECT COUNT(*) FROM patients WHERE gender IS 'F') AS female_count;`

Q7 Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.

`SELECT
  first_name,
  last_name,
  allergies
FROM patients
WHERE
  allergies IN ('Penicillin', 'Morphine')
ORDER BY
  allergies,
  first_name,
  last_name;`

Q8 Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.

`SELECT
  patient_id,
  diagnosis
FROM admissions
GROUP BY
  patient_id,
  diagnosis
HAVING COUNT(*) > 1;`

Q9 Show the city and the total number of patients in the city.
Order from most to least patients and then by city name ascending.

`SELECT
  city,
  COUNT(*) AS num_patients
FROM patients
GROUP BY city
ORDER BY num_patients DESC, city asc;`

Q10 

  
