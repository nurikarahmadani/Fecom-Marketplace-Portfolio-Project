# Fecom-Marketplace-Portfolio-Project

## Database Preparation
```sql
CREATE DATABASE fecom_marketplace_db


CREATE TABLE geolocations(
	Geo_Postal_Code VARCHAR(100) PRIMARY KEY,
	Geo_Lat VARCHAR(100),
	Geo_Lon VARCHAR(100),
	Geolocation_City VARCHAR(100),
	Geo_Country VARCHAR(100)
)

CREATE TABLE customer_list(
	Customer_Trx_ID VARCHAR(100) PRIMARY KEY,
	Subscriber_ID VARCHAR(100),
	Subscribe_Date DATE,
	First_Order_Date DATE,
	Customer_Postal_Code VARCHAR (100),
	Customer_City VARCHAR(100),
	Customer_Country VARCHAR(100),
	Customer_Country_Code VARCHAR(100),
	Age INT,
	Gender VARCHAR(100),
	CONSTRAINT FK_Postal_Code FOREIGN KEY (Customer_Postal_Code) REFERENCES geolocations(Geo_Postal_Code)
)

CREATE TABLE seller_list(
	Seller_ID VARCHAR(100) PRIMARY KEY,
	Seller_Name VARCHAR(100),
	Seller_Postal_Code VARCHAR(100),
	Seller_City VARCHAR(100),
	Country_Code VARCHAR(100),
	Seller_Country VARCHAR(100),
	CONSTRAINT Seller_FK_Postal_Code FOREIGN KEY (Seller_Postal_Code) REFERENCES geolocations(Geo_Postal_Code)
)

CREATE TABLE products(
	Product_ID VARCHAR(100) PRIMARY KEY,
	Product_Category_Name VARCHAR(100),
	Product_Weight_Gr DECIMAL,
	Product_Length_Cm DECIMAL,
	Product_Height_Cm DECIMAL,
	Product_Width_Cm DECIMAL
)

CREATE TABLE orders(
	Order_ID VARCHAR(100) PRIMARY KEY,
	Customer_Trx_ID VARCHAR(100),
	Order_Status VARCHAR(100),
	Order_Purchase_Timestamp DATETIME,
	Order_Approved_At DATETIME,
	Order_Delivered_Carrier_Date DATETIME,
	Order_Delivered_Customer_Date DATETIME,
	Order_Estimated_Delivery_Date DATE
	CONSTRAINT orders_FK_Customer_Trx_ID FOREIGN KEY(Customer_Trx_ID) REFERENCES customer_list(Customer_Trx_ID)
)

CREATE TABLE order_items(
	Order_ID VARCHAR(100),
	Order_Item_ID VARCHAR(100) PRIMARY KEY,
	Product_ID VARCHAR(100),
	Seller_ID VARCHAR(100),
	Shipping_Limit_Date DATETIME,
	Price DECIMAL,
	Freight_Value DECIMAL,
	CONSTRAINT orderitems_FK_Order_ID FOREIGN KEY(Order_ID) REFERENCES orders(Order_ID),
	CONSTRAINT orderitems_FK_Product_ID FOREIGN KEY(Product_ID) REFERENCES products(Product_ID),
	CONSTRAINT orderitems_FK_Seller_ID FOREIGN KEY(Seller_ID) REFERENCES seller_list(Seller_ID)
)

CREATE TABLE order_reviews(
	Review_ID VARCHAR(100),
	Order_ID VARCHAR(100),
	Review_Score INT,
	Review_Comment_Title_En VARCHAR(100),
	Review_Comment_Message_En VARCHAR(100),
	Review_Creation_Date DATETIME,
	Review_Answer_Timestamp DATETIME,
	CONSTRAINT orderreviews_FK_Order_ID FOREIGN KEY (Order_ID) REFERENCES orders(Order_ID)
)

CREATE TABLE order_payments(
	Order_ID VARCHAR(100),
	Payment_Sequential INT,
	Payment_Type VARCHAR(100),
	Payment_Installments INT,
	Payment_Value DECIMAL
	CONSTRAINT orderpayments_FK_Order_ID FOREIGN KEY (Order_ID) REFERENCES orders(Order_ID)
)
```
