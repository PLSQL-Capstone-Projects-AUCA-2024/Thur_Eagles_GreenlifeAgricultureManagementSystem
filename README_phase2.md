# GreenLife Urban Agriculture Management System
## Project Overview
GreenLife is an initiative to transform unused urban areas into productive farms that supply fresh food, reduce pollution, and promote green spaces in cities. This project, the GreenLife Urban Agriculture Management System, 
provides a structured database solution to manage key aspects of urban farms, including farm locations, crop growth, workforce tasks, inventory, and produce distribution.
Purpose and Objectives
The GreenLife Urban Agriculture Management System is designed to optimize urban farm operations by tracking resources, workforce assignments, crop lifecycles, and produce distribution. 
The objectives are to improve decision-making, streamline operations, and support sustainable urban agriculture. This database system aligns with GreenLife's mission to promote healthier and greener cities.
Key Entities and Attributes
## 1. Farm Locations
### Purpose: Stores data on each farm location, such as location details, type, size, and environmental conditions.
**Attributes:**
- Location_ID: Unique ID for each farm.
- Address: Address of the farm.
- Type: Type of farm (e.g., rooftop or in garden).
- Size: Farm size in square meters.
- Sunlight_Availability: Hours of sunlight available daily.
- Water_Source: Information about water accessibility at each farm.

## 2. Crops
### Purpose: Contains records of crops grown on each farm, with planting dates, harvest timelines, and care requirements.
**Attributes:**
- Crop_ID: Unique identifier for each crop type.
- Farm_ID: Links to the farm location where the crop is planted.
- Crop_Type: Name/type of the crop (e.g., tomatoes, lettuce).
- Planting_Date: Date of planting.
- Expected_Harvest_Date: Expected date for harvesting.
- Care_Requirements: Special care and maintenance needs for each crop.

## 3. Workforce
### Purpose: Manages details of the workforce, including volunteers and employees, involved in farm operations.
**Attributes:**
- Worker_ID: Unique ID for each worker.
- Name: Name of the worker.
- Role: Position (e.g., volunteer, employee).
- Tasks_Assigned: Tasks assigned to each worker.
- Hours_Worked: Total hours worked by each worker.
- Special_Skills: Skills relevant to farm tasks (e.g., planting, maintenance).

## 4. Harvest Records
### Purpose: Tracks harvest information, such as produce quantity and distribution channels.
**Attributes:**
- Harvest_ID: Unique ID for each harvest event.
- Crop_ID: ID linking to the specific crop harvested.
- Farm_ID: ID of the farm where the crop was harvested.
- Harvest_Date: Date of the harvest.
- Quantity: Amount of produce harvested.

## 5. Inventory and Resources
### Purpose: Tracks essential resources, including seeds, tools, fertilizers, and other supplies.
**Attributes:**
- Item_ID: Unique ID for each inventory item.
- Item_Name: Name of the item (e.g., seeds, fertilizer).
- Quantity: Current stock quantity of each item.
- Cost: Cost per item.
- Supplier_Info: Information about suppliers of each item.

## Relationships and Workflow

- Each farm location can grow multiple crops.
- Each crop is tied to a specific farm location.
- Workforce members can be assigned tasks across multiple farms.
- Harvest records connect crops to their corresponding farms and produce distribution channels.
- Inventory tracks resources needed across all farms, ensuring that each location has the supplies required.

## ER Diagram
The ER diagram (Entity-Relationship Diagram) illustrates connections between entities like farms, crops, workforce, harvest records, and inventory items, showing how they work together in the management system.

![Screenshot 2024-11-14 at 19 02 04](https://github.com/user-attachments/assets/64ed7417-7c17-440a-9a82-dffa4435e4fc)









