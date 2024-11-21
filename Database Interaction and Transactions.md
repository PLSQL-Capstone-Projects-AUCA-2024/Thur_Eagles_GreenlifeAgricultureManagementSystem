# Database Interaction and Transactions
## Perform SQL Queries and Joins
```sql
---Retrieve Harvest Information by Farm Location
SELECT F.Address AS FarmAddress, C.Crop_Type AS Crop, H.Harvest_Date AS HarvestDate, H.Produce_Amount AS Quantity, H.Distribution
FROM HarvestRecords H
JOIN Crops C ON H.Crop_ID = C.Crop_ID
JOIN FarmLocations F ON C.Farm_ID = F.Location_ID;

---List All Workers and Their Tasks at Farms
SELECT W.Name AS WorkerName, W.Role, W.Tasks_Assigned, F.Address AS FarmLocation
FROM Workforce W
LEFT JOIN FarmLocations F ON W.Tasks_Assigned LIKE '%Planting%' OR W.Tasks_Assigned LIKE '%Weeding%';

---Show Inventory Utilization by Crop Type
SELECT I.Resource_Type AS Resource, C.Crop_Type AS Crop, I.Quantity
FROM Inventory I
JOIN Crops C ON I.Resource_Type = 'Fertilizer' OR I.Resource_Type = 'Seeds';

---Calculate Total Harvest Yield for Each Farm
SELECT F.Address AS FarmAddress, SUM(H.Produce_Amount) AS TotalYield
FROM HarvestRecords H
JOIN Crops C ON H.Crop_ID = C.Crop_ID
JOIN FarmLocations F ON C.Farm_ID = F.Location_ID
GROUP BY F.Address;

