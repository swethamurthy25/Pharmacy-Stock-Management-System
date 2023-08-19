# Pharmacy-Stock-Management-System

## DDL Commands

### Creation of database:

```sql
CREATE DATABASE Pharmacy_Stock_Management;
GO
```

![image](https://github.com/swethamurthy25/Pharmacy-Stock-Management-System/assets/112581595/c642665e-22c4-46fc-a712-9f04c90d5576)


### Creation of Tables:

#### Table Name: Customer 

We have included the primary key constrain on CustomerId

```sql
USE Pharmacy_Stock_Management;
GO

CREATE SCHEMA ORMModel1;
GO

CREATE TABLE ORMModel1.Customer
(
    customerId int IDENTITY (1, 1) NOT NULL,
    countryName nvarchar(20) NOT NULL,
    customerName nvarchar(25) NOT NULL,
    customerOrderNr int NOT NULL,
    emailAddress nvarchar(20) NOT NULL,
    membershipDateYmd date NOT NULL,
    membershipID int NOT NULL,
    stateCode nchar(20) NOT NULL,
    address nvarchar(30),
    age int,
    genderTitle nvarchar(max),
    zipcodeCode int,
    CONSTRAINT Customer_PK PRIMARY KEY(customerId)
);
```

![image](https://github.com/swethamurthy25/Pharmacy-Stock-Management-System/assets/112581595/1e97fb20-8777-453c-ae6c-6256dc0d8613)


#### Table Name: Stores 

We have added the primary key constraint on storesId

```sql
Use Pharmacy_Stock_Management;
Go

CREATE TABLE ORMModel1.Stores
(
	storesId int IDENTITY (1, 1) NOT NULL,
	store_Name nvarchar(20) NOT NULL,
	address nvarchar(30),
	cityName nvarchar(10),
	contactNumberInt int,
	countryName nvarchar(20),
	stateCode nchar(20),
	zipcodeCode int,
	CONSTRAINT Stores_PK PRIMARY KEY(storesId)
)
```

![image](https://github.com/swethamurthy25/Pharmacy-Stock-Management-System/assets/112581595/05e60ae9-30fe-4e87-ad3a-9c13c3c0c567)


#### Table Name: Product

We have added the primary key constraint on productid.

```sql
Use Pharmacy_Stock_Management;
Go

CREATE TABLE ORMModel1.Products
(
	productsId int IDENTITY (1, 1) NOT NULL,
	priceNr nvarchar(20) NOT NULL,
	prod_Name nvarchar(30),
	shelf_LifeInt nvarchar(10),
	storesId int,
	unit nvarchar(20),
	unit_SizeInt nvarchar(10),
	vendorIDInt int,
	CONSTRAINT 	_PK PRIMARY KEY(productsId),
)
```

![image](https://github.com/swethamurthy25/Pharmacy-Stock-Management-System/assets/112581595/189362d1-71af-405a-8d49-6a2064a49751)

### Adding Foreign Key constraint on storesId 

The storesId (pk) from the stores table is used as the foreign key here in the Products table

```sql
ALTER TABLE ORMModel1.Products ADD CONSTRAINT Products_FK FOREIGN KEY (storesId) REFERENCES ORMModel1.Stores(storesId) ON DELETE NO ACTION ON UPDATE CASCADE
GO
```

![image](https://github.com/swethamurthy25/Pharmacy-Stock-Management-System/assets/112581595/b8f37b02-d922-4085-98ab-5f032f4a4195)

### Table Name: Manufacturer 

We have made the manufacturerId as the primary key. The customerId (pk) from the Customer table is used as the foreign key here in the manufacturer table. We have also used the NOT NULL constraint on a few of the fields.

```sql
CREATE TABLE ORMModel1.Manufacturer
(
	manufacturerId int IDENTITY (1, 1) NOT NULL,
	accountBeginDateYmd int NOT NULL,
	contactNumberInt int,
	vendorLicenseInt int NOT NULL,
	vendorName nvarchar(30) NOT NULL,
	cityName nvarchar(10),
	countryName nvarchar(20),
	emailAddress nvarchar(20),
	vendorAddress nvarchar(20),
	stateCode nchar(10),
	zipCode int,
	customerId int,
	CONSTRAINT Manufacturer_PK PRIMARY KEY(manufacturerId),
	CONSTRAINT Manufacturer_FK FOREIGN KEY(customerId) REFERENCES ORMModel1.Customer(customerId) 
)
```

![image](https://github.com/swethamurthy25/Pharmacy-Stock-Management-System/assets/112581595/630d9d4a-d5ee-4eec-9e84-6e23f103d65c)


### Table Name: Inventory 

We have made the inventoryId as primary key and two foreign key constraints.

FK1 - The productsId (pk) from the Products table is used as the foreign key here.

FK2 – The storesId (pk) from the Stores table is used as the foreign key here. 

We have also used the NOT NULL constraint on a few of the fields.

```sql
CREATE TABLE ORMModel1.Inventory
(
	inventoryId int IDENTITY (1, 1) NOT NULL,
	expiry_DateYmd date NOT NULL,
	inventory_OnhandInt int NOT NULL,
	manufacturing_DateYmd date NOT NULL,
	productsId int NOT NULL,
	storesId int NOT NULL,
	vendorIDInt int NOT NULL,
	CONSTRAINT Inventory_PK PRIMARY KEY(inventoryId),
	CONSTRAINT Inventory_FK1 FOREIGN KEY(productsId) REFERENCES ORMModel1.Products(productsId),
	CONSTRAINT Inventory_FK2 FOREIGN KEY(storesId) REFERENCES ORMModel1.Stores(storesId)
)
GO
```

![image](https://github.com/swethamurthy25/Pharmacy-Stock-Management-System/assets/112581595/eef920e8-9c95-4642-bd37-be19424cf662)

### Table Name: Customer Order Details

We have made the customerOrderDetailsNr the primary key. 

The productsId (pk) from the Products table is used as the foreign key. We have also used the NOT NULL constraint on all the fields of the table.

```sql
CREATE TABLE ORMModel1.CustomerOrderDetails
(
	customerOrderDetailsNr int IDENTITY (1, 1) NOT NULL,
	orderIdInt int NOT NULL,
	quantityInt int NOT NULL,
	productsId int NOT NULL,
	CONSTRAINT CustomerOrderDetails_PK PRIMARY KEY(customerOrderDetailsNr),
	CONSTRAINT Inventory_FK FOREIGN KEY(productsId) REFERENCES ORMModel1.Products(productsId)
)
GO
```

![image](https://github.com/swethamurthy25/Pharmacy-Stock-Management-System/assets/112581595/9e5479a5-f940-4f2e-8e77-f2cb3512ed37)


### Table Name: Customer Order 

We have made the customerOrderNr the primary key. 

The storesId (pk) from the Stores table is used as the foreign key. We have also used the NOT NULL constraint on all the fields of the table.

```sql
CREATE TABLE ORMModel1.CustomerOrder
(
	customerOrderNr int IDENTITY (1, 1) NOT NULL,
	customerOrderDetailsNr int,
	order_DateYmd date NOT NULL,
	order_IdInt int NOT NULL,
	storesId int NOT NULL,
	total_cheque_Amount decimal NOT NULL,
	tax_Amount decimal NOT NULL,
	CONSTRAINT CustomerOrder_PK PRIMARY KEY(customerOrderNr),
	CONSTRAINT CustomerOrder_FK FOREIGN KEY(storesId) REFERENCES ORMModel1.Stores(storesId)
)
GO
```

![image](https://github.com/swethamurthy25/Pharmacy-Stock-Management-System/assets/112581595/f95c2b8f-2adf-46fa-8a84-0f76cff7d73f)


### Table Name: Price

We have made the priceNr the primary key. 

The productsId (pk) from the Products table is used as the foreign key. We have also used the NOT NULL constraint on all the fields of the table.

![image](https://github.com/swethamurthy25/Pharmacy-Stock-Management-System/assets/112581595/8adce717-2bfe-4af6-a342-1ea02fcc7da6)


_______________________________________________________________________________________________________________________________


## DML Commands (Inserting Data into Tables)

### Customer Table:

```sql
SET IDENTITY_INSERT [ORMModel1].[Customer] ON
INSERT INTO [ORMModel1].[Customer]
(
customerId, countryName, customerName, customerOrderNr, emailAddress, membershipDateYmd,membershipID,stateCode, address, age,genderTitle, zipcodeCode)
VALUES (1,'India', 'Swetha','10','swe@gmail.com','1993-03-21',123,'Tamilnadu','123,sri nagar',20,'female',12345),
	   (2,'USA', 'Divya','11','divya@gmail.com','1994-02-12',345,'arizona','1717 south dorseylane',21,'female',56781),
	   (3,'Bangladesh', 'Abhishek','24','abi@gmail.com','2000-11-02',431,'dhaka','1100 East University Drive',23,'male',65189),
	   (4,'Pakistan', 'Tom','28','tom@gmail.com','2000-06-09',1000,'kabul','100 West Street',22,'male',43123),
	   (5,'London', 'Jerry','29','jerr@gmail.com','2005-08-12',234,'Tower Bridge','10 Downing Street ',20,'male',60009),
       (6,' Australia', 'Jimmy','35','jimmy@gmail.com','2001-07-21',21,'queensland','1100 East University Drive,21,'male',69871);
```

![image](https://github.com/swethamurthy25/Pharmacy-Stock-Management-System/assets/112581595/8513b946-b7d5-4a23-8530-8bc74af5a52d)

![image](https://github.com/swethamurthy25/Pharmacy-Stock-Management-System/assets/112581595/7615d933-ea2f-4e53-9095-f07620f90e32)

### Stores Table:

```sql
SET IDENTITY_INSERT [ORMModel1].[Stores] ON
INSERT INTO [ORMModel1].[Stores](
storesId,store_Name , address,cityName,contactNumberInt,countryName ,stateCode ,zipcodeCode)
VALUES (101,'store1','1717 south doresy lane','tempe',234567899,'UnitedStates','AZ',85281),
	   (102,'store2','100 new street','dallas',234567899,'UnitedStates','DL',89965),
	   (103,'store3','1718 north doresy lane','houston',234567899,'UnitedStates','HU',87651),
	   (104,'store4','1710 apache blvd','california',234567899,'UnitedStates','CA',77654),
       (105,'store5','1700 west drive','florida',234567899,'UnitedStates','FL',90876);

```










