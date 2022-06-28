# ICT502-Back-End-project

CREATE TABLE  "CUSTOMER" 
   (	"CUSTOMER_ID" NUMBER(10,0) NOT NULL ENABLE, 
	"CUSTOMER_NAME" VARCHAR2(100) NOT NULL ENABLE, 
	"CUSTOMER_ADDRESS" VARCHAR2(100), 
	"CUSTOMER_PHONE" NUMBER(10,0), 
	"CUSTOMER_EMAIL" VARCHAR2(100), 
	"CUSTOMER_TYPE" VARCHAR2(100), 
	"CUSTOMER_TABLE" NUMBER(10,0), 
	"VACCINATION_STATUS" VARCHAR2(100), 
	"DATE" DATE, 
	"TIME" TIMESTAMP (6), 
	 PRIMARY KEY ("CUSTOMER_ID") ENABLE
   ) ;
   
 CREATE TABLE  "PAYMENT" 
   (	"PAYMENT_ID" NUMBER(10,0) NOT NULL ENABLE, 
	"PAYMENT_TIME" TIMESTAMP (6), 
	"PAYMENT_DATE" DATE, 
	"PAYMENT_TYPE" VARCHAR2(100), 
	"TOTAL" FLOAT(126), 
	 PRIMARY KEY ("PAYMENT_ID") ENABLE
   ) ;

CREATE TABLE  "STAFF" 
   (	"STAFF_ID" NUMBER(10,0) NOT NULL ENABLE, 
	"STAFF_NAME" VARCHAR2(100), 
	"STAFF_GENDER" VARCHAR2(100), 
	"DATE_OF_BIRTH" DATE, 
	"HIRE_DATE" DATE, 
	"SALARY" NUMBER(10,0), 
	"SHIFT" VARCHAR2(100), 
	"MANAGER_ID" NUMBER(10,0), 
	 PRIMARY KEY ("STAFF_ID") ENABLE
   ) ;ALTER TABLE  "STAFF" ADD CONSTRAINT "STAFF_ID_FK" FOREIGN KEY ("STAFF_ID")
	  REFERENCES  "STAFF" ("STAFF_ID") ENABLE;
    
CREATE TABLE  "ORDER" 
   (	"ORDER_ID" NUMBER(10,0) NOT NULL ENABLE, 
	"ORDER_DATE" DATE, 
	"ORDER_TIME" TIMESTAMP (6), 
	 PRIMARY KEY ("ORDER_ID") ENABLE
   ) ;ALTER TABLE  "ORDER" ADD CONSTRAINT "ORDER_ID_FK1" FOREIGN KEY ("ORDER_ID")
	  REFERENCES  "CUSTOMER" ("CUSTOMER_ID") ENABLE;ALTER TABLE  "ORDER" ADD CONSTRAINT "ORDER_ID_FK2" FOREIGN KEY ("ORDER_ID")
	  REFERENCES  "PAYMENT" ("PAYMENT_ID") ENABLE;ALTER TABLE  "ORDER" ADD CONSTRAINT "ORDER_ID_FK3" FOREIGN KEY ("ORDER_ID")
	  REFERENCES  "STAFF" ("STAFF_ID") ENABLE;

CREATE TABLE  "PRODUCT" 
   (	"PRODUCT_ID" NUMBER(10,0) NOT NULL ENABLE, 
	"PRODUCT_NAME" VARCHAR2(100), 
	"PRODUCT_TYPE" VARCHAR2(100), 
	"PRICE" NUMBER(10,0), 
	 PRIMARY KEY ("PRODUCT_ID") ENABLE
   ) ;

CREATE TABLE  "ORDER_LINE" 
   (	"QUANTITY" NUMBER(10,0) NOT NULL ENABLE, 
	"ORDER_ID" NUMBER(10,0) NOT NULL ENABLE, 
	"PRODUCT_ID" NUMBER(10,0) NOT NULL ENABLE, 
	 CONSTRAINT "ORDER_ID_PRODUCT_ID_PK" PRIMARY KEY ("ORDER_ID", "PRODUCT_ID") ENABLE
   ) ;ALTER TABLE  "ORDER_LINE" ADD CONSTRAINT "ORDER_ID_PRODUCT_ID_FK" FOREIGN KEY ("ORDER_ID", "PRODUCT_ID")
	  REFERENCES  "ORDER_LINE" ("ORDER_ID", "PRODUCT_ID") ENABLE;

CREATE TABLE  "SUPPLIER" 
   (	"SUPPLIER_ID" NUMBER(10,0) NOT NULL ENABLE, 
	"CONTACT_NUM" NUMBER(10,0), 
	"SUPPLIER_NAME" VARCHAR2(100), 
	"SUPPLIER_ADDRESS" VARCHAR2(100), 
	"SUPPLIER_EMAIL" VARCHAR2(100), 
	 PRIMARY KEY ("SUPPLIER_ID") ENABLE
   ) ;

CREATE TABLE  "INGREDIENTS" 
   (	"INGREDIENTS_ID" NUMBER(10,0) NOT NULL ENABLE, 
	"INGREDIENTS_NAME" VARCHAR2(100), 
	"QUANTITY" NUMBER(10,0), 
	"EXPIRATION_DATE" DATE, 
	"SUPPLY_DATE" DATE, 
	"SUPPLY_TIME" TIMESTAMP (6), 
	 PRIMARY KEY ("INGREDIENTS_ID") ENABLE
   ) ;ALTER TABLE  "INGREDIENTS" ADD CONSTRAINT "INGREDIENTS_ID_FK" FOREIGN KEY ("INGREDIENTS_ID")
	  REFERENCES  "SUPPLIER" ("SUPPLIER_ID") ENABLE;

CREATE TABLE  "INGREDIENTS_LINE" 
   (	"QUANTITY" NUMBER(10,0), 
	"INGREDIENTS_ID" NUMBER(10,0) NOT NULL ENABLE, 
	"SUPPLIER_ID" NUMBER(10,0) NOT NULL ENABLE, 
	 CONSTRAINT "INGREDIENTS_ID_SUPPLIER_ID_PK" PRIMARY KEY ("INGREDIENTS_ID", "SUPPLIER_ID") ENABLE
   ) ;ALTER TABLE  "INGREDIENTS_LINE" ADD CONSTRAINT "INGREDIENTS_ID_SUPPLIER_ID_FK" FOREIGN KEY ("INGREDIENTS_ID", "SUPPLIER_ID")
	  REFERENCES  "INGREDIENTS_LINE" ("INGREDIENTS_ID", "SUPPLIER_ID") ENABLE;
