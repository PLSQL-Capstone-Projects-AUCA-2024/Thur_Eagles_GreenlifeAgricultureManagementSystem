##  SQL Script for Transaction Management
```sql
BEGIN
    -- Start Transaction
    SAVEPOINT before_update_inventory;
````
   ### Step 1: Update Inventory Resources
   ```sql
    UPDATE Inventory
    SET Quantity = Quantity - 5
    WHERE Resource_ID = 201; -- Fertilizer

    UPDATE Inventory
    SET Quantity = Quantity - 10
    WHERE Resource_ID = 202; -- Seeds
````
### Check for errors (example: insufficient inventory)
```sql
    IF (SELECT Quantity FROM Inventory WHERE Resource_ID = 201) < 0 THEN
        ROLLBACK TO before_update_inventory;
        DBMS_OUTPUT.PUT_LINE('Error: Not enough fertilizer in stock. Transaction rolled back to savepoint.');
        RETURN;
    END IF;
````
   ### Step 2: Insert a New Harvest Record
   ```sql
    INSERT INTO HarvestRecords (Harvest_ID, Crop_ID, Harvest_Date, Produce_Amount, Distribution)
    VALUES (306, 101, TO_DATE('2024-04-01', 'YYYY-MM-DD'), 120, 'Market');

    SAVEPOINT after_insert_harvest;
````
   ### Step 3: Simulate an Error (e.g., invalid data in another table)
   ```sql
    UPDATE Crops
    SET Expected_Harvest_Date = NULL -- Violates NOT NULL constraint
    WHERE Crop_ID = 101;
````
  ### Commit the transaction if all steps succeed
  ```sql
    COMMIT;
````
### Error Corrections
```sql
EXCEPTION
    WHEN OTHERS THEN
        -- Rollback to the last savepoint
        ROLLBACK TO after_insert_harvest;
        DBMS_OUTPUT.PUT_LINE('Error occurred. Changes rolled back to last savepoint.');
        ROLLBACK; -- Final rollback if necessary
END;
````
