# Ex. No: 5 Creating Triggers using PL/SQL

## DATE: 31.08.2023

## AIM: To create a Trigger using PL/SQL.

## Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

## Program:

### Create Employee table
```
CREATE TABLE employed(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);
```

### Create Salary log table
```

CREATE TABLE sal_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
```

### PLSQL Trigger Code
```
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
```

### Insert the value
```
-- Insert the values in the employee table
insert into employed values(1,'Eswar','AIDS',1000000);
insert into employed values(2,'Lingesh','SALES',500000);
```

### Update the salary
```
-- Update the salary of an employee
UPDATE employed
SET salary = 60000
WHERE empid = 1;
-- Display the employee table
SELECT * FROM employed;

-- Display the salary_log table
SELECT * FROM sal_log;
```

## Output:
![dbms1_exp5](https://github.com/Thirukaalathessvarar-S/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/121166390/f406b622-dcd8-465d-ac31-56162abee902)

![dbms5_exp2](https://github.com/Thirukaalathessvarar-S/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/121166390/7bc39a56-3c44-42e3-9550-b9fcf2610deb)

## Result:
The program has been implemented successfully.
