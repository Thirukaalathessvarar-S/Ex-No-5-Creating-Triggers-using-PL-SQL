# Ex. No: 5 Creating Triggers using PL/SQL

### AIM: To create a Trigger using PL/SQL.

### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

### Program:
-- Create the trigger
CREATE OR REPLACE TRIGGER log_sal_update
BEFORE UPDATE ON employed
FOR EACH ROW
BEGIN
  IF :OLD.salary != :NEW.salary THEN
    INSERT INTO sal_log (empid, empname, old_salary, new_salary, update_date)
    VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  END IF;
END;
/
-- Insert the values in the employee table
insert into employed values(1,'Nagul','AIDS',1000000);
insert into employed values(2,'Santhosh','SALES',500000);

-- Update the salary of an employee
UPDATE employed
SET salary = 60000
WHERE empid = 1;
-- Display the employee table
SELECT * FROM employed;

-- Display the salary_log table
SELECT * FROM sal_log;

### Output:
![dbms_exp5_1](https://github.com/Thirukaalathessvarar-S/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/121166390/beaf0254-4b46-4590-88dc-674b69ccca1d)
![dbms_exp5_2](https://github.com/Thirukaalathessvarar-S/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/121166390/352b1511-149e-46f6-8f28-0ff4a34106d5)
![dbms_exp5_3](https://github.com/Thirukaalathessvarar-S/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/121166390/7eb922df-72bf-4df7-b829-4c0f22a5a3c1)

### Result:
The program has been implemented successfully.
