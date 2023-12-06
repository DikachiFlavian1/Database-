 Projects you will find in this repository comprises of my data base knowledge ranging from creation of tables, inserting values into columns, Normalization, querying tables and if necessary updating columns and tables . 
 
Project Name:__Finance&Product Tracker__
--
__Aim__
The project was aimed at creating a database named finance & product tracker to help solve some challenging issues being experienced by the company

1.__To provide insights into the total number of customers that patronizes the comapny.__

2.__To keep a tract record of company available products and quantity with prices.__

3.__to keep record of daily&weekly  sales and product quantity left whereby marking recommendations for needed product.__ 

3.__To analysize customer choiced product and relationship with age.__

4.__and also to reduce data redundacy while.__ 

__Process__

I started the project by creating a database and followed up by creating a tables and cloumns according to the given specification 
__TABLE NAMES__

**USERS**
CREATE TABLE Users (
    UserID SERIAL  PRIMARY KEY,
    FirstName VARCHAR(255) NOT NULL,
    LastName VARCHAR(255) NOT NULL,
    Age INT,
    Sex CHAR(1), -- Assuming 'M' for male, 'F' for female, or other appropriate values
    UserName VARCHAR(255) NOT NULL);
    
  **PRODUCTS**
CREATE TABLE Products (
    ProductID SERIAL PRIMARY KEY,
    ProductName VARCHAR(255) NOT NULL,
    Price DECIMAL(10, 2) NOT NULL,
    Quantity INT NOT NULL
    -- Other product-related fields
);select * from Users

**TRANSACTIONS**
CREATE TABLE Transactions (
    TransactionID SERIAL PRIMARY KEY,
    UserID INT,
    ProductID INT,
    Quantity INT NOT NULL,
    TransactionDate DATE NOT NULL,
    FOREIGN KEY (UserID) REFERENCES Users(UserID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
    -- Other transaction-related fields
);
**REPORTS**
CREATE TABLE Reports (
    ReportID SERIAL PRIMARY KEY,
    UserID INT,
    StartDate DATE NOT NULL,
    EndDate DATE NOT NULL,
    TotalIncome DECIMAL(10, 2),
    TotalExpenses DECIMAL(10, 2),
    FOREIGN KEY (UserID) REFERENCES Users(UserID)
    -- Other report-related fields
);

__INSERTING VALUES INTO TABLES__

INSERT INTO Users (FirstName, LastName, Age, Sex, UserName)
SELECT
    'Kachi' || (i + 1),
    'Flavian' || (i + 1),
    (18 + (i % 20)),  -- Random age between 18 and 37
    CASE WHEN i % 2 = 0 THEN 'M' ELSE 'F' END,  -- Alternating gender
    'Kachi' || 'Flavian' || (i + 1) 
FROM generate_series(1, 300) i;

INSERT INTO Products (ProductName, Price, Quantity)
SELECT
    'IdealMats' || (i + 1),
    CAST(RANDOM() * 100 + 1 AS NUMERIC(10, 2)),  
    (i % 10 + 1) * 10  
FROM generate_series(1, 850) i;
select * from Products

-- Insert values into Transactions table
INSERT INTO Transactions (UserID, ProductID, Quantity, TransactionDate)
SELECT
    (i % 300) + 1,  -- Assigning random users to transactions
    (i % 30) + 1,   -- Assigning random products to transactions
    (i % 5 + 1) * 2,  -- Quantity ranging from 2 to 10
    CURRENT_DATE - (i % 30)  -- Random transaction dates within the last 30 days
FROM generate_series(1, 1000) i;
select * from Transactions


-- Insert values into Reports table
INSERT INTO Reports (UserID, StartDate, EndDate, TotalIncome, TotalExpenses)
SELECT
    (i % 300) + 1,  -- Assigning random users to reports
    CURRENT_DATE - (i % 30) - 30,  -- Random start date within the last 30 days
    CURRENT_DATE - (i % 30),  -- Random end date within the last 30 days
    CAST(RANDOM() * 1000 + 1 AS NUMERIC (10, 2)),  -- Random total income between 1 and 1000
    CAST(RANDOM() * 500 + 1 AS NUMERIC (10, 2))  -- Random total expenses between 1 and 500
FROM generate_series(1, 850) i;

check the tables files above to see the resultof the table and values creation 
__IF YOU READ TO THIS PATH , ITS IMPORTANT THAT YOOU NOTE THAT THIS WAS A PROJECT I ASSIGNED MY SELF AND THE VALUES AND NAMES ARE FICTIONAL BUT  THE PROJECT GOAL REMAINS__

