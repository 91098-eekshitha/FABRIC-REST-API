REQUIREMENT:
Develop a REST API in java to insert and retrieve some data from a database table.

TASK BREAKDOWN:
1. Setup a local database, create a table, insert some records using any database client 
2. Write SQL to insert and retrieve records from the above table using the same database 
 Client. 
3. Write java code to insert and retrieve the records from the database table. 
4. Create a REST API in JAVA to insert and retrieve the same records.

OBJECTIVE:
This project is to provide the head start to beginners to build REST API's, using the popular 
java open source frameworks and necessary configs.

PREREQUISITES:
• JAVA (JDK)
• MY SQL

INSTALLING:
• Clone the project
• Create DB by running below command. In my repository dbconfig folder is present, 
inside that create_db.sql file is present Give the absolute path of this file in below 
command.
 mysql -h hostname -u user database < path/to/create_db.sql
• Change the username and password of your MYSQL username in context.xml and 
hibernate.cfg.xml.

API DOCUMENTATION:

1. Setup a local database, create a table, insert some records using any database client 
Database: Cloth Shop
Table: Fabrics
+-------+----------------------------+---------------+---------+-------+
| id | Fabric | State | price | qty |
| (INT) | (VARCHAR(50)) | (VARCHAR(50)) | (FLOAT) | (INT) |
+-------+----------------------------+---------------+---------+-------+
| 1001 | Silk | Tamil Nadu | 128/m | 11 |
| 1002 | Wool | Rajasthan | 148/m | 22 |
| 1003 | Nylon | Gujarat | 130/m | 33 |
| 1004 | Velvet | West Bengal | 150/m | 44 |
| 1005 | Polyester | Maharashtra | 60/m | 55 |
+-------+----------------------------+---------------+---------+-------+

2. Write SQL to insert and retrieve records from the above table using the same 
database Client. 
By placing a SELECT statement within the INSERT statement, we can perform multiples 
inserts quickly.
we have a table called Fabrics with the following data:
+-------+----------------------------+---------------+---------+-------+
| number | Fabric | State | price | qty |
| (INT) | (VARCHAR(50)) | (VARCHAR(50)) | (FLOAT) | (INT) |
+-------+----------------------------+---------------+---------+-------+
| 1001 | Silk | Tamil Nadu | 128/m | 11 |
| 1002 | Wool | Rajasthan | 148/m | 22 |
| 1003 | Nylon | Gujarat | 130/m | 33 |
| 1004 | Velvet | West Bengal | 150/m | 44 || 1005 | Polyester | Maharashtra | 60/m | 55 |
+-------+----------------------------+---------------+---------+-------+
And a table called fabrics with the following data:
+----------------+----------------------------+---------------+
|Fabric_id | name | website | 
+----------------+----------------------------+---------------+
| 2000 | Silk | Amazon | 
| 3000 | Satin | Flipkart | 
| 4000 | Nylon | Myntra | 
| 5000 | Leather | Meesho | 
| 6000 | Polyester | Ajio |
| 7000 | Linen | NULL |
| 8000 | Lace | Nyka |
+----------------+----------------------------+---------------+
INSERT INTO fabrics
(fabric_id,fabric_name,fabric_website) 
SELECT fabric_number AS fabric_id,fabric_name,fabric_website
FROM fabrics
WHERE fabrics_number < 1003;
• With this type of INSERT, some databases require you to alias the column names in 
the SELECT to match the column names of the table we are inserting into.
• There will be 2 records inserted. Select the data from the fabrics table again:
 SELECT * FROM fabrics;
+----------------+----------------------------+---------------+
|Fabric_id | name | website | 
+----------------+----------------------------+---------------+
| 2000 | Silk | Amazon | | 3000 | Satin | Flipkart | 
| 4000 | Nylon | Myntra | 
| 5000 | Leather | Meesho | 
| 6000 | Polyester | Ajio |
| 7000 | Linen | NULL |
| 8000 | Lace | Nyka |
|1001 | Silk | NULL |
|1002 | Wool | NULL |
+----------------+----------------------------+---------------+
• With this type of insert, you may wish to check for the number of rows being inserted.
We can determine the number of rows that will be inserted by running a COUNT(*) on 
the SELECT statement before performing the insert.
• Example:
 SELECT COUNT(*)
 FROM fabrics
 WHERE fabric_number < 1003;
• This will return number of records that will be inserted when we execute the INSERT 
statement.
 COUNT(*)
 2

3. Write java code to insert and retrieve the records from the database table.
CODE:
import javax. context.xml.*;
import javax.hibernate.cfg.xml.*;
import java.util.*;/**
* Cloth Shop
*/
@Entity
@Table(name = "fabric")
public class fabric implements java.io.Serializable {
 private static final long serialVersionUID = -2107661175822965352L;
 private String itemId;
 private String itemName;
 private String itemState;
 private String createdBy;
 private String updatedBy;
 private Quality createdAt;
 private Price updatedAt;
 public fabric() {
 }
 @Id
 @Column(name= "id", unique = true, nullable = false)
 public String getItemId() {
 return this.itemId;
 }
public void setItemId(String catGuid) {
 this.itemId = catGuid;
 }
 @Column(name = "name", unique = true, nullable = false)
 @XmlAttribute(name="name") public String getItemName() {
 return this.itemName;
 }
 public void setItemName(String catName) {
 this.itemName = catName;
 }
 @Column(name = "description", nullable = false)
 @XmlAttribute(name="description")
 public String getItemDesc() {
 return this.itemDesc;
 }
 public void setItemState(String catState) {
 this.itemState = catState;
 }
 @Column(name = "created_by")
 public String getCreatedBy() {
 return this.createdBy;
 }
 public void setCreatedBy(String createdBy) {
 this.createdBy = createdBy;
 }
 @Column(name = "updated_by")
 public String getUpdatedBy() {
 return this.updatedBy; }
 public void setUpdatedBy(String updatedBy) {
 this.updatedBy = updatedBy;
 }
 @Column(name = "created_at")
 public Quality getCreatedAt() {
 return this.createdAt;
 }
 public void setCreatedAt(Quality createdAt) {
 this.createdAt = createdAt;
 }
 @Column(name = "updated_at")
 public Price getUpdatedAt() {
 return this.updatedAt;
 }
 public void setUpdatedAt(Price updatedAt) {
 this.updatedAt = updatedAt;
 }
}

4. Create a REST API in JAVA to insert and retrieve the same records.
Create Fabric REST API
URL :- localhost:8080/rest/api/fabrics/
header :- content-type :- application/json
method :- post
body :- {
"name" : "first fabric",
"description" : "sample"
