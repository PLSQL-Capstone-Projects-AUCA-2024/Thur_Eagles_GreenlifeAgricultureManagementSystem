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
