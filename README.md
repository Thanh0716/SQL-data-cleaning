# SQL-data-cleaning

This is an educational project on data cleaning and preparation using SQL. The original database in CSV format is located in the file club_member_info.csv. Here, we will explore the steps that need to be applied to obtain a cleansed version of the dataset.

## 1. View data
View 10 first rows
```sql
SELECT *
FROM club_member_info c 
LIMIT 10;
```
Result
|full_name|age|martial_status|email|phone|full_address|job_title|membership_date|
|---------|---|--------------|-----|-----|------------|---------|---------------|
|addie lush|40|married|alush0@shutterfly.com|254-389-8708|3226 Eastlawn Pass,Temple,Texas|Assistant Professor|7/31/2013|
|      ROCK CRADICK|46|married|rcradick1@newsvine.com|910-566-2007|4 Harbort Avenue,Fayetteville,North Carolina|Programmer III|5/27/2018|
|Sydel Sharvell|46|divorced|ssharvell2@amazon.co.jp|702-187-8715|4 School Place,Las Vegas,Nevada|Budget/Accounting Analyst I|10/6/2017|
|Constantin de la cruz|35||co3@bloglines.com|402-688-7162|6 Monument Crossing,Omaha,Nebraska|Desktop Support Technician|10/20/2015|
|  Gaylor Redhole|38|married|gredhole4@japanpost.jp|917-394-6001|88 Cherokee Pass,New York City,New York|Legal Assistant|5/29/2019|
|Wanda del mar       |44|single|wkunzel5@slideshare.net|937-467-6942|10864 Buhler Plaza,Hamilton,Ohio|Human Resources Assistant IV|3/24/2015|
|Joann Kenealy|41|married|jkenealy6@bloomberg.com|513-726-9885|733 Hagan Parkway,Cincinnati,Ohio|Accountant IV|4/17/2013|
|   Joete Cudiff|51|divorced|jcudiff7@ycombinator.com|616-617-0965|975 Dwight Plaza,Grand Rapids,Michigan|Research Nurse|11/16/2014|
|mendie alexandrescu|46|single|malexandrescu8@state.gov|504-918-4753|34 Delladonna Terrace,New Orleans,Louisiana|Systems Administrator III|3/12/1921|
| fey kloss|52|married|fkloss9@godaddy.com|808-177-0318|8976 Jackson Park,Honolulu,Hawaii|Chemical Engineer|11/5/2014|

## 2. Copy new table 
### 2.1 Create new table for cleanding 
```sql
-- club_member_info definition
CREATE TABLE club_member_info_cleanded (
	full_name VARCHAR(50),
	age INTEGER,
	martial_status VARCHAR(50),
	email VARCHAR(50),
	phone VARCHAR(50),
	full_address VARCHAR(50),
	job_title VARCHAR(50),
	membership_date VARCHAR(50)
);
```
### 2.2 Copy all values from original table 
```sql
INSERT INTO club_member_info_cleanded 
SELECT * 
FROM club_member_info;
```
## 3. Clean data
### 3.1 Full name
#### 3.1.1 Whitespace
```sql
UPDATE club_member_info_cleanded
SET full_name  = TRIM(full_name)
```
Result
|full_name|
|---------|
|addie lush|
|ROCK CRADICK|
|Sydel Sharvell|
|Constantin de la cruz|
|Gaylor Redhole|
|Wanda del mar|
|Joann Kenealy|
|Joete Cudiff|
|mendie alexandrescu|
|fey kloss|

### 3.2 Age 
#### 3.2.1 Whitespace
```sql
UPDATE club_member_info_cleanded
SET age = CAST(SUBSTR(age, 1, 2) AS INTEGER)
WHERE age >100 AND age <> ''
```
#### 3.2.2 Add AVG(age)
```sql
UPDATE club_member_info_cleanded
SET age = 42
WHERE age = ''
```
### 3.3 Leading and trailing whitespaces
#### 3.3.1 martial_status
```sql
UPDATE club_member_info_cleanded
SET martial_status = 'single'
WHERE TRIM(martial_status) = ''
```
#### 3.3.2 job_title 
```sql
DELETE FROM club_member_info_cleanded 
WHERE job_title = ''
```
