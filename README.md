# Pharmacy-Stock-Management-System

Course: Advanced Database Management System (ADBMS)

## Summary

Any contemporary, data-driven business produces significant data through its various operations. Due to differences in business operations, systems, and procedures, it is essential that the data be appropriately consolidated, cleaned to reduce noise, and converted to allow for meaningful analytics. To achieve this, a data modeling process must be performed to systematically arrange the data and store it in a format that can be used for a variety of applications. When building a new database or reengineering an existing one, data models act as a road map. To create relationships and make sense of the data, many tools including tables, graphs, nesting, and more were used. One sort of data modeling that makes use of constraints to create relationships between different entities is object-relational mapping. While NoSQL uses buckets and hierarchical documents for the same purpose, Relational Schema uses keys to map data. The focus of this project is to put these strategies into practice while maintaining a unified theme. The Pharmacy Stock Management database will be developed by using ORM, Relational Schema, and NoSQL approach. 

## Introduction

Any business requires inventory management, stock visibility, and dedicated systems that help analyze and make key business decisions. In this project, we have taken the example of a pharmacy store chain operating in several franchises. The inventory management database is designed to capture store details, manufacturer details, product details, on-hand inventory, daily transactions, and sales. The tables are designed so that they can be used to analyze and create dashboards for critical KPIs such as total sales per store, the product with the highest sales, average amount per cheque, tracking different lot codes of the same product, shelf-life analysis, and replenishment levels. Customer, Manufacturer, Products (Medicine), Stores, Inventory, Price, Customer Order (Master), and Order details are the primary tables and entities involved in this project. Each store or pharmacy will purchase the appropriate amount of goods (medication) from the authorized manufacturer and stock them in an inventory with all its information. When a customer visits a pharmacy to buy drugs, the medications are then sold to that customer. Therefore, all the entities stated above are quite interconnected with one another. The overall sales for any given store can be obtained using the Customer Order (Master) entity, and specific order information can be obtained using the Order details table. This aids in minimizing the complexity level of each query. The entities and tables used in this project allow us to utilize a variety of joints to extract the proper information. For instance, by joining the price table and the inventory table, we can analyze the current on-hand cost of the whole pharmacy. It is therefore created in a way that makes easy analysis, replenishment, and important business decisions possible.

## Context

Since drugs are essential to the healthcare sector, technology has been crucial to the expansion of the pharmaceutical industry in recent years. Medication administration requires extreme caution because it can potentially reduce suffering and speed up recovery from illnesses. By automating the inventory management process thereby improving visibility and traceability, the Pharmacy Stocks Management System will help to guarantee that the pharmacy has an adequate supply of drugs and supplies to meet patients' demands. It is crucial for pharmacies to make sure they have enough drug stock to meet the needs of the patients. Pharmacies use manual inventories to monitor their stock levels, but they are time-consuming and subject to human errors. Inventory management is the heart of every supply chain industry, especially pharmaceuticals. Each pharmaceutical entity requires granular inventory visibility and traceability so that proper replenishment levels can be established. The traceability component helps track shelf life and address any inventory discrepancies to ensure the highest quality of service to the customers while maintaining quality standards. By using this system, pharmacies can keep track of their inventory and replenish any medications that are running out of stock.

## Recognized Entities

### Customer: 
The customer entity represents the end users of the system, who visit the pharmacy for drug purchases.

* CustomerId (int) - Unique identifier (Primary Key)

* CustomerName (varchar) - Refers to the name of the customer

* Age (int) - Refers to the age of the customer

* Gender (varchar) - Refers to the sexual characteristics of a customer. It can be male or female.

* Address (varchar) - Contains the address of the customer

* City (varchar) - represents the city the customer is residing in.

* State (varchar) - represents the state the customer is residing in.

* Country (varchar) - represents the country the customer is residing in.

* Zip Code (int) - represents the zip code of the city or state.

* MembershipId (int) - Represents the membership id number. This can also be null if the customer does not have a membership or a rewards account.

* MembershipDate (date) - Represents the date when the membership was activated. This will eventually become null when the membership id is null.
  
* EmailAddress (varchar) - Contains the email id of the customer.


### Manufacturers: 

The Manufacturer/Vendor is the one who sells their products a.k.a medicines to the stores.

* VendorID (int) - Unique Identifier (Primary Key)

* VendorName (varchar) - Represents the name of the manufacturer

* VendorLicense (int) - Refers to the license number of the manufacturer

* VendorAddress (varchar) - Contains the address of the manufacturer or their company

* City (varchar) - represents the city where the manufacturing company is located

* State (varchar) - represents the state where the manufacturing company is located

* Country (varchar) - represents the country where the manufacturing company is located

* Zip Code (int) - represents the zip code of the city or state.

* EmailAddress (varchar) - Contains the email id of the manufacturer/company.

* ContactNumber (int) - Mobile Number or the office number of the company

* AccountBegindate (date) - Represent the date from when the store started getting the products from this manufacturer.

### Products (Medicine):

This entity represents each SKU (Stock Keeping Unit) that is housed within each pharmacy and the system.

* Prod_Id (int) - Unique Identifier (Primary Key)

* Prod_Name (varchar) - Name of the Medicine/Product

* VendorID (int) - unique identifier of the vendor/manufacturer from whom it is purchased. This acts as a foreign key here.

* Shelf_Life (int) - Lifetime of each product. This can be represented by the number of days.

* Unit(varchar)-the actual value pertaining to that Unit (possible values 'ea','ounces', 'grams')

* Unit_Size (int) - the measurement used for that particular SKU - ea, ounces, pounds, etc.

### Stores : 

This entity represents the stores or pharmacy which sells the products to the customer.

* Store_Id (int) - Unique Identifier (Primary Key)

* Store_Name (varchar) - Name of the store or pharmacy

* Address (varchar) - Address of the pharmacy where it is located.

* City (varchar) - represents the city where the store is located

* State (varchar) - represents the state where the store is located

* Country (varchar) - represents the country where the store is located

* Zip Code (int) - represents the zip code of the city or state.

* ContactNumber (int) - Mobile Number or the office number of the store

### Inventory: 

This entity refers to the warehouse where the products are stocked for future usage.

* Inventory_Id (int) - Unique Identifier (Primary Key)

* Store_Id (int) - Unique Identifier of the store. This acts as a Foreign Key here.

* Prod_Id (int) -Unique Identifier of the product. This acts as a Foreign Key here.

* Vendor_Id (int) - Unique Identifier of the manufacturer. This acts as a Foreign Key here.

* Inventory_Onhand (int) - Total count of each available product  

* Manufacturing_Date (date) - Manufacturing date of each product/medicine

* Expiry_Date (date) – The expiry date of each product/medicine

### Price: 

The price entity holds information on each product's price in addition to the manufacturer from which it was purchased.

* Prod_Id (int) -Unique Identifier of product. This refers to the product/medicine and this acts as a foreign key here.

* VendorID (int) - Unique Identifier of the manufacturer. This refers to the manufacturer from whom the above-mentioned medicine was bought. This acts as a foreign key here.
  
* Unit_Price (float) - Individual cost of each product.

### Customer Order (Master): 

With the help of this entity, the total cost of a customer's purchase of a product or medicine has been calculated.

* Order_Id (int) - Refers to the order number/order id (Primary Key)

* Order_Date (date) - Date when the order was placed.
  
* Total_Cheque_Amount (float) - the total cost of the purchase
  
* Tax_Amount (float) - tax amount for the total bill
  
* CustomerId (int) - Unique Identifier of the customer table. This refers to the name of the customer who placed the order. This acts as a foreign key here.
  
* Store_Id (int) - Unique Identifier of store table. This refers to the store/pharmacy information from where the product was purchased. This acts as a foreign key here.

### Customer Order Details: 

This entity contains details about the products purchased and their quantity.

* Order_Id - (int)- Unique identifier of order table. This refers to the order and acts as a foreign key here.

* Product_Id - (int) - Unique Identifier of the product table. This refers to the product and acts as a foreign key here.

* Quantity (int) - the number of products purchased


## At least 5 queries the SQL database will answer:

* How much is the total sales for each store in the current calendar year?

  We can do the inner join on tables customer orders and stores to get the result.

* Which item/product has the highest volume of sales?

  We can do the inner join on tables Customer order details and Product to get the result. 

* Which store has the maximum sale value? 

  We can combine tables of Customer Orders and Store details to get the maximum value. 

* Display the order id which has the minimum quantity?

  We can combine tables of Customer Orders Details and Customers to get the minimum value.

* Display the store name with the number of stocks available?

  We can combine tables of inventory and stores to get the result.
  

## ORM Diagram 

![image](https://github.com/swethamurthy25/Pharmacy-Stock-Management-System/assets/112581595/0a0bdd64-e34b-4dc9-8c51-312afb45cc71)


## Relational Schema

![image](https://github.com/swethamurthy25/Pharmacy-Stock-Management-System/assets/112581595/014ea0ea-eea9-4284-8563-f8491a69fc5c)




