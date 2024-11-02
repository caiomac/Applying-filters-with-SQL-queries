<h1>Applying filters with SQL queries</h1>

<h2>Description</h2>
I was proposing I was a security professional at a large organization. Part of my job was to investigate security issues to help keep the system secure. I discovered some potential security issues that involved login attempts and employee machines.
<br/>
My task was to examine the organization’s data in their <i>employees</i> and <i>log_in_attempts</i> tables. I needed to use SQL filters, by using commands such WHERE together with LIKE, BETWEEN/AND, =, >=, AND, OR and NOT,  to retrieve records from different datasets and investigate the potential security issues.

<br />

<h2>Objectives</h2>

- <b>Retrieve information from different databases through filtering</b>

<h2>Languages and Utilities Used</h2>

- <b>SQL queries</b> 

<h2>Environments Used </h2>

- <b>MariaDB</b>

<h2>Program walk-through:</h2>

<b>Step 1 - Retrieve after hours failed login attempts:</b> 
<br /> 
<br /> 
My team was investigating failed login attempts that were made after business hours. I wanted to retrieve this information from the login activity. I identified all unsuccessful attempts after 18:00. The <b>login_time</b> column in the <b>log_in_attempts</b> table contained information on when login attempts were made. Office hours end at '18:00'. The success column in the <b>log_in_attempts</b> table contained values of TRUE or FALSE to indicate whether the login was successful. MySQL stores Boolean values as 1 for TRUE, and 0 for FALSE. This means that TRUE was represented as 1, and FALSE represented as 0 in the success column.
<br/> 
<br/> 
![1](https://github.com/user-attachments/assets/9f673a7d-a2cc-4f77-8c1e-569f85c21925)
<br />
<br />
By using <b><i>SELECT * FROM log_in_attempts WHERE login_time > '18:00' AND success = 0</b></i>; I was able to display the whole data from the table <b>log_in_attempts</b> that had login_time after 18:00 and the login wasn’t successful. It found 19 unsuccessful login attempts after 18:00. 

<br />
<br />

<b>Step 2 - Retrieve login attempts on specific dates:</b>  
<br/> 
My team was investigating a suspicious event that occurred on '2022-05-09'. I wanted to retrieve all login attempts that occurred on this day and the day before ('2022-05-08'). The login_date column in the <b>log_in_attempts</b> table contained information on the dates when login attempts were made.
<br />
<br />
![2](https://github.com/user-attachments/assets/8ea48460-f08b-4d2f-8b08-9440c2f4f886)
<br />
<br />
By using <b><i>SELECT * FROM log_in_attempts WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';</b></i> I was able to display the whole data from the table <b>log_in_attempts</b> that had login_date equal to  2022-05-09 or 2022-05-09. It found 75  login attempts on these dates. 
<br />
<br />
<br />
<b>Step 3 - Retrieve login attempts outside of Mexico:</b>  
<br/> 
This time, my team was investigating logins that did not originate in Mexico, and I needed to find this information. Note that the country field included entries with 'MEX' and 'MEXICO'. I should use the NOT and LIKE operators and the matching pattern 'MEX%'. 
<br /> 
<br />
![3](https://github.com/user-attachments/assets/c653aa8f-deaf-448a-b524-389d88cae46b)
<br />
<br />
By using <b><i>SELECT * FROM log_in_attempts WHERE NOT country LIKE ‘MEX%’;</b></i> I was able to display the whole data from the table <b>log_in_attempts</b> that had any country that didn’t start with MEX.  It found 144 login attempts in countries except Mexico. 
<br />
<br />
<br />
<b>Step 4 - Retrieve employees in Marketing:</b>  
<br/> 
In the next activities, it was retrieved the information from the <b>department</b> and <b>office</b> columns in the <b>employees</b> table. Firstly I ran the following SQL query to view the columns and values in the employees table: <b><i>SELECT * FROM employees;</b></i>
<br/> 
<br />
![4](https://github.com/user-attachments/assets/974e9011-a4c8-4e88-b7a4-51eed92daecf)
<br />
<br />
My team was updating employee machines, and I needed to obtain the information about employees in the 'Marketing' department who were located in all offices in the East building (such as 'East-170' or 'East-320').
<br />
<br />
![5](https://github.com/user-attachments/assets/c9534e50-a2ec-42a0-91d9-4e123786d898)
<br />
<br />
By using <b><i>SELECT * FROM employees WHERE department = ‘Marketing’ AND office LIKE ‘East%’;</b></i> I was able to display the whole data from the table <b>employees</b> that had Marketing as department and had office starting with East. It returned 7 employees.
<br />
<br />
<br />
<b>Step 5 - Retrieve employees in Finance or Sales:</b>  
<br/> 
Then, my team needed to perform a different update to the computers of all employees in the Finance or the Sales department, and I needed to locate information on these employees.
<br/> 
<br />
![6](https://github.com/user-attachments/assets/08ae191d-b340-4e28-9882-8d605328f180)
<br />
<br />
By using <b><i>SELECT * FROM employees WHERE department = ‘Marketing’ OR department = ‘Sales’;</b></i> I was able to display the whole data from the table <b>employees</b> that had Marketing or Sales as department in any location. It returned 71 employees.
<br />
<br />
<br />
<b>Step 6 - Retrieve all employees not in IT:</b>  
<br/> 
My team needed to make one more update. This update was already made to employee computers in the Information Technology department. The team needed information about employees who are not in that department. I should use the NOT operator to identify these employees.
<br/> 
<br />
![7](https://github.com/user-attachments/assets/12755e48-6068-4b7d-8a9e-2f77bd6b4ef1)
<br />
<br />
By using <b><i>SELECT * FROM employees WHERE NOT department = ‘Information Technology’;</b></i> I was able to display the whole data from the table <b>employees</b> that had employees from all departments with exception of Information Technology. It returned 161 employees.
<br />
<br />
<!--
 ```diff
