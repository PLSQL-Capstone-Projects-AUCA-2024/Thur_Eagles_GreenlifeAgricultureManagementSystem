
```sql
Summary of Database Operations
1. Table Creation
   we designed a relational database schema for an Greenlife agriculture management system. Here’s a breakdown of the tables:

FarmLocations:

Stores information about farms, including their location, type, size, sunlight availability, and water sources.
Primary Key: Location_ID.
Crops:

Manages crops grown at specific farm locations, with details about planting/harvest dates and care requirements.
Primary Key: Crop_ID.
Foreign Key: Farm_ID references FarmLocations(Location_ID).
Workforce:

Tracks workforce details, such as names, roles, tasks, hours worked, and special skills.
Primary Key: Worker_ID.
HarvestRecords:

Records information about crop harvests, including dates, amounts, and distribution methods.
Primary Key: Harvest_ID.
Foreign Key: Crop_ID references Crops(Crop_ID).
Inventory:

Keeps track of resources (e.g., fertilizers, seeds) with supplier details, costs, and quantities.
Primary Key: Resource_ID.
2. Data Insertion
Sample data was added to each table to represent real-world scenarios:

FarmLocations: Included five farm locations with various types, sizes, sunlight levels, and water sources.
Crops: Added crops with planting and expected harvest dates, linked to specific farms.
Workforce: Recorded a mix of employees and volunteers with their roles and tasks.
HarvestRecords: Captured details about harvest amounts and their distribution.
Inventory: Listed resources with supplier, cost, and quantity details.
3. SQL Joins
Joins were used to extract meaningful relationships between tables:

INNER JOIN: Combines rows from two tables where a matching condition exists. For example:

Retrieving crops, farm addresses, and care requirements (Crops + FarmLocations).
OUTER JOIN: Includes all rows from one or both tables, even if no match exists.

LEFT JOIN: Lists all farm locations with their crops (if any).
RIGHT JOIN: Lists all crops with their associated farms (if any).
FULL OUTER JOIN: Combines results from both sides, including unmatched rows from both tables.
CROSS JOIN: Generates all possible combinations of rows from two tables.



The schema is normalized and uses primary and foreign keys effectively to maintain data integrity.
Relationships are well-defined, supporting efficient queries.
Data Utility:

Sample data covers a wide range of use cases, such as resource tracking, workforce management, and crop distribution.
Joins:

Joins demonstrate the relationships between entities, enabling flexible data retrieval.
They provide insights into farm operations, such as which farms grow which crops or which workforce members handle specific tasks.
