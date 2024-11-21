## Data Insertion
### Farm Location
```sql
INSERT INTO FarmLocations VALUES (1, 'Rooftop A', 'Rooftop', 200, 6, 'Rainwater');
INSERT INTO FarmLocations VALUES (2, 'Community Garden B', 'Garden', 500, 8, 'Well Water');
INSERT INTO FarmLocations VALUES (3, 'Rooftop C', 'Rooftop', 300, 5, 'Rainwater');
INSERT INTO FarmLocations VALUES (4, 'School Yard D', 'Garden', 400, 7, 'Municipal Water');
INSERT INTO FarmLocations VALUES (5, 'Office Terrace E', 'Rooftop', 150, 4, 'Rainwater');

### Crops
```sql
INSERT INTO Crops VALUES (101, 1, 'Tomatoes', TO_DATE('2024-01-01', 'YYYY-MM-DD'), TO_DATE('2024-03-01', 'YYYY-MM-DD'), 'Daily watering');
INSERT INTO Crops VALUES (102, 2, 'Lettuce', TO_DATE('2024-02-15', 'YYYY-MM-DD'), TO_DATE('2024-03-15', 'YYYY-MM-DD'), 'Weekly fertilizing');
INSERT INTO Crops VALUES (103, 3, 'Carrots', TO_DATE('2024-01-20', 'YYYY-MM-DD'), TO_DATE('2024-04-10', 'YYYY-MM-DD'), 'Regular weeding');
INSERT INTO Crops VALUES (104, 4, 'Spinach', TO_DATE('2024-03-01', 'YYYY-MM-DD'), TO_DATE('2024-04-20', 'YYYY-MM-DD'), 'Partial shade required');
INSERT INTO Crops VALUES (105, 5, 'Peppers', TO_DATE('2024-01-10', 'YYYY-MM-DD'), TO_DATE('2024-03-20', 'YYYY-MM-DD'), 'High sunlight needed');
