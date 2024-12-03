## 1. Triggers
### Trigger to Update Inventory After Harvest
### This trigger ensures inventory (like fertilizers or tools) is automatically updated when a harvest record is inserted.
```sql
CREATE OR REPLACE TRIGGER UpdateInventoryAfterHarvest
AFTER INSERT ON HarvestRecords
FOR EACH ROW
BEGIN
    -- Update inventory to reflect resource usage during the harvest
    UPDATE Inventory
    SET Quantity = Quantity - 10
    WHERE Resource_Type = 'Fertilizer';

    -- Log the action
    INSERT INTO AuditTable (Action, Table_Name, Change_Date, Changed_By)
    VALUES ('INSERT', 'HarvestRecords', SYSDATE, USER);
END;
/
````
### Purpose: Automates the reduction of inventory after a harvest, ensuring real-time updates.
### Audit Logging: Tracks changes for accountability.
### Advantages: Reduces manual intervention and enforces data consistency.
## 2. Cursors
### Cursor to Assign Tasks to Workers
### This cursor assigns specific tasks to available workers based on their roles.
```sql
DECLARE
    CURSOR assign_cursor IS
    SELECT Worker_ID, Role FROM Workforce WHERE Role = 'Volunteer';
    v_task VARCHAR2(50);
BEGIN
    FOR worker IN assign_cursor LOOP
        -- Assign tasks based on the worker's role
        IF worker.Role = 'Volunteer' THEN
            v_task := 'Weeding';
        ELSE
            v_task := 'Irrigation Management';
        END IF;

        UPDATE Workforce
        SET Tasks_Assigned = v_task
        WHERE Worker_ID = worker.Worker_ID;

        DBMS_OUTPUT.PUT_LINE('Assigned ' || v_task || ' to Worker ID ' || worker.Worker_ID);
    END LOOP;
END;
/
````
### Purpose: Automates task assignment to reduce manual effort.
### Dynamic Tasking: Adapts assignments based on worker roles.
### Debugging: Outputs assignments for verification.

## 3. Attributes and Functions
### Function to Calculate Total Yield for a Farm
### This function calculates the total produce harvested from a specific farm.
```sql
CREATE OR REPLACE FUNCTION CalculateTotalYield(farm_id IN FarmLocations.Location_ID%TYPE)
RETURN NUMBER IS
    total_yield NUMBER;
BEGIN
    -- Calculate the total harvest yield for the given farm
    SELECT SUM(H.Produce_Amount) INTO total_yield
    FROM HarvestRecords H
    JOIN Crops C ON H.Crop_ID = C.Crop_ID
    WHERE C.Farm_ID = farm_id;

    RETURN total_yield;
END;
/
````
### Usage
```sql
SELECT CalculateTotalYield(1) AS TotalYield FROM DUAL;
````
### Purpose: Provides a quick summary of total yields for analysis.
### Dynamic Typing: Uses %TYPE for flexibility.
### Reusability: Encapsulates logic, making it reusable across the application.
## 4. Packages
### Farm Management Package
### This package groups related procedures and functions for better organization.

### Package Specification:
```sql
CREATE OR REPLACE PACKAGE FarmManagement AS
    PROCEDURE AssignTask(worker_id IN Workforce.Worker_ID%TYPE, task IN VARCHAR2);
    FUNCTION CalculateFarmYield(farm_id IN FarmLocations.Location_ID%TYPE) RETURN NUMBER;
END FarmManagement;
/
````
### Package Body
```sql
CREATE OR REPLACE PACKAGE BODY FarmManagement AS
    -- Procedure to assign a task to a worker
    PROCEDURE AssignTask(worker_id IN Workforce.Worker_ID%TYPE, task IN VARCHAR2) IS
    BEGIN
        UPDATE Workforce
        SET Tasks_Assigned = task
        WHERE Worker_ID = worker_id;

        DBMS_OUTPUT.PUT_LINE('Task "' || task || '" assigned to Worker ID ' || worker_id);
    END AssignTask;

    -- Function to calculate total yield for a farm
    FUNCTION CalculateFarmYield(farm_id IN FarmLocations.Location_ID%TYPE) RETURN NUMBER IS
        total_yield NUMBER;
    BEGIN
        SELECT SUM(H.Produce_Amount) INTO total_yield
        FROM HarvestRecords H
        JOIN Crops C ON H.Crop_ID = C.Crop_ID
        WHERE C.Farm_ID = farm_id;

        RETURN total_yield;
    END CalculateFarmYield;
END FarmManagement;
/
````
### Encapsulation: Groups related logic to improve readability and security.
### Reusability: Procedures and functions can be reused across multiple modules.
### Modularity: Simplifies debugging and maintenance.

## 5. Auditing
### Auditing Changes to Workforce Table
### This trigger logs changes to the Workforce table, including updates and deletions.
```sql
CREATE OR REPLACE TRIGGER WorkforceAudit
AFTER UPDATE OR DELETE ON Workforce
FOR EACH ROW
BEGIN
    IF UPDATING THEN
        INSERT INTO AuditTable (Action, Table_Name, Change_Date, Changed_By, Details)
        VALUES ('UPDATE', 'Workforce', SYSDATE, USER, 'Updated Worker ID: ' || :OLD.Worker_ID);
    ELSIF DELETING THEN
        INSERT INTO AuditTable (Action, Table_Name, Change_Date, Changed_By, Details)
        VALUES ('DELETE', 'Workforce', SYSDATE, USER, 'Deleted Worker ID: ' || :OLD.Worker_ID);
    END IF;
END;
/
````
### Purpose: Tracks changes to ensure accountability and compliance.
### Detailed Logging: Records the exact action and affected record.
### Security: Helps monitor unauthorized changes.
## Conclusion
### Triggers: Automate workflows and enforce rules without user intervention.
### Cursors: Handle row-by-row operations efficiently.
### Functions: Encapsulate logic for calculations and improve modularity.
### Packages: Enhance code organization, reusability, and security.
### Auditing: Ensure data integrity and accountability through change tracking.
