### SQL Data
### Scenario
- You are working with a relational database named world, which contains three tables:
- `city`
- `country`
- `countrylanguage`
Your task is to validate the configuration of this database by performing `INSERT`, `UPDATE`, and `DELETE` operations on the country table.
### Lab Overview & Objectives
- This lab teaches you how to modify and manage data within a relational database using SQL commands.
By completing the lab, you will learn to:

✅ 1. Insert rows into a table
- Use the `INSERT INTO` statement to add new data to the country table.
  
✅ 2. Update rows in a table
-Use the `UPDATE` statement to modify existing data while applying conditions via WHERE.

✅ 3. Delete rows from a table
- Use the `DELETE FROM` statement to remove one or more rows in the country table.
  
✅ 4. Import rows from a backup
- Restore or load data using a database backup file to repopulate the table.
  
### Task 1: Connect to a database
1. Open the `AWS Console` → go to `EC2` → `Instances`.
2. Select the instance named `Command Host`.
<img width="1276" height="582" alt="Screenshot 2025-11-25 145202" src="https://github.com/user-attachments/assets/767132b9-0f3e-4dda-b999-cae2bfdd0390" />

3. Choose `Connect` → `Session Manager` → `Connect`.
<img width="1264" height="533" alt="Screenshot 2025-11-25 145410" src="https://github.com/user-attachments/assets/3cde13ea-8432-463b-ac86-abbddedfa035" />

4. If `Connect` is unavailable, wait a few minutes and retry.
5. In the terminal, run:
`sudo su
cd /home/ec2-user/`
6. Connect to the MySQL database using:
`mysql -u root --password='re:St@rt!9'`
7. The MySQL shell allows you to run SQL commands on the database.
8. Use `-u` for username and `-p` for password.
9. If the session becomes unresponsive, reconnect and rerun the setup commands.
10. View existing databases with: `SHOW DATABASES;`
    
### Task 2: Insert data into a table

1. Verify the table exists by running: SELECT  `FROM world.country;`.
  
2. This displays all columns in the `country` table.
   
3. Insert the Ireland row using the full `INSERT INTO world.country VALUES (...); `command.
 
4. Insert the Australia row using the second `INSERT` statement provided.
   
5. Ensure the values match the column order defined in the table schema.
    
6. Confirm both rows were inserted with:
    
7. SELECT ` FROM world.country WHERE Code IN ('IRL','AUS');`
    
8. The query should return two rows: `Australia and Ireland.`
    
9.  The result displays all fields including Code, Name, Continent, Region, Population, GNP, and GovernmentForm
<img width="1275" height="594" alt="Screenshot 2025-11-25 150154" src="https://github.com/user-attachments/assets/dad01565-12bc-4d15-b89f-9709734e585b" />

### Task 3: Update rows in a table

1. Update all rows by setting the Population column to 0 using:
 `UPDATE world.country SET Population = 0;`

2. Because there is no WHERE clause, every row in the table is affected.
 
3. Confirm the update with: SELECT  `FROM world.country;`

4. Next, update both the Population and SurfaceArea columns for all rows.
   
5.  Run: `UPDATE world.country SET Population = 100, SurfaceArea = 100;`
 
6. This again updates every row because no WHERE condition is used.
   
8. Validate the changes with: SELECT  `FROM world.country;`
   
9. The results should show Population = 100 and SurfaceArea = 100 for all rows.
<img width="1272" height="592" alt="Screenshot 2025-11-25 150504" src="https://github.com/user-attachments/assets/3a81b7c8-1109-4654-a626-516133a84050" />

#### Task 4: Delete rows from a table
1. Use caution with DELETE statements because changes may not be reversible.
   
2. Run `SET FOREIGN_KEY_CHECKS = 0;` to temporarily bypass foreign key constraints.
   
3 .Delete all rows using: `DELETE FROM world.country;`

4. Since no WHERE clause is used, every row in the table is removed.
5. Verify deletion with: SELECT `FROM world.country`;
    
<img width="1279" height="598" alt="Screenshot 2025-11-25 150817" src="https://github.com/user-attachments/assets/9da8c95a-b799-42af-998b-e479527dc628" />

### 
1. Exit the MySQL terminal using `QUIT;.`

2. Verify the SQL file exists: ls `/home/ec2-user/world.sql.`

3. Loading many rows manually is slow, so SQL script files automate bulk inserts.

4. Import the dataset using:` mysql -u root --password='re:St@rt!9' < /home/ec2-user/world.sql`.

5. The script creates two more tables and loads data into all three.

6. Reconnect to MySQL: `mysql -u root --password='re:St@rt!9'`.

7. Run `USE world;` then `SHOW TABLES;` to confirm city, country, and countrylanguage.

8. Use SELECT queries to verify all rows were successfully loaded into each table
<img width="1273" height="596" alt="Screenshot 2025-11-25 151431" src="https://github.com/user-attachments/assets/025fe3b4-ba09-42a8-ade1-893e37beae4b" />
<img width="1273" height="590" alt="Screenshot 2025-11-25 151848" src="https://github.com/user-attachments/assets/5eeebb13-23af-4c3c-aeaa-e6667678a094" />
<img width="1275" height="582" alt="Screenshot 2025-11-25 152009" src="https://github.com/user-attachments/assets/23f06b0c-abc1-4057-a108-ef3fce91f802" />





   

    





