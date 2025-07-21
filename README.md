# Celebal_Week7_Assignment
Automates daily truncate-load of CSV files into PostgreSQL from a data lake. Files are processed based on naming patterns to add date/dateKey columns when required. Includes Docker support for portability and optional Docker Compose for PostgreSQL integration.

--Let's suppose you have 3 different types of file 1) CUST_MSTR_20191112.csv 2) master_child_export-20191112.csv 3) H_ECOM_ORDER.csv All these files will be in the data lake container You have to fetch all three types of files into their respective folders. Note: There could be multiple files on all 3 types for different dates for example CUST_MSTR_20191112.csv and CUST_MSTR_20191113.csv 1) For the "CUST_MSTR" starting name of the file You have to create an additional column for a date that will fetch the data value from the filename and put it into an additional column Date format: 2019-11-12 and load it into the "CUST_MSTR" table 2) For the "master_child_export" starting name of the file You have to create two additional columns date and date key which will fetch the data from the filename and put it into the additional columns. Date format: 2019-11-12 DateKey format: 20191112 and load it into the "master_child" table 3) for the "H_ECOM_ORDER" type of file you have to load it into the database as it is. and load it into "H_ECOM_Orders" table Note: This process will work on truncate load on a daily basis--
# Daily CSV Loader into Database

This project loads CSV files from a data lake directory into respective PostgreSQL database tables using a truncate-and-load logic.

## 📁 File Types & Rules

| File Pattern              | Table Name       | Notes                                                            |
|---------------------------|------------------|------------------------------------------------------------------|
| CUST_MSTR_YYYYMMDD.csv     | CUST_MSTR         | Extracts date and adds `file_date` column (YYYY-MM-DD)          |
| master_child_export-YYYYMMDD.csv | master_child      | Adds `file_date` (YYYY-MM-DD) and `file_date_key` (YYYYMMDD)     |
| H_ECOM_ORDER.csv          | H_ECOM_Orders     | Loaded as-is, no transformation                                  |

## 🔧 Configuration

Edit `config.py` to configure:
- Database connection
- Local data lake path

```python
DATABASE_CONFIG = {
    'host': 'localhost',
    'port': 5432,
    'database': 'your_database',
    'user': 'your_user',
    'password': 'your_password'
}
DATA_DIRECTORY = '/your/data/lake/path'

--Let's suppose you have 3 different types of file 1) CUST_MSTR_20191112.csv 2) master_child_export-20191112.csv 3) H_ECOM_ORDER.csv All these files will be in the data lake container You have to fetch all three types of files into their respective folders. Note: There could be multiple files on all 3 types for different dates for example CUST_MSTR_20191112.csv and CUST_MSTR_20191113.csv 1) For the "CUST_MSTR" starting name of the file You have to create an additional column for a date that will fetch the data value from the filename and put it into an additional column Date format: 2019-11-12 and load it into the "CUST_MSTR" table 2) For the "master_child_export" starting name of the file You have to create two additional columns date and date key which will fetch the data from the filename and put it into the additional columns. Date format: 2019-11-12 DateKey format: 20191112 and load it into the "master_child" table 3) for the "H_ECOM_ORDER" type of file you have to load it into the database as it is. and load it into "H_ECOM_Orders" table Note: This process will work on truncate load on a daily basis--
# 🚀 Daily CSV File Loader to PostgreSQL

This project loads and processes daily CSV files from a data lake folder. Each file type has specific transformation logic and is loaded into its corresponding PostgreSQL table using truncate-load.

## 📁 File Patterns & Processing

| File Pattern                   | Action                                                                 |
|-------------------------------|------------------------------------------------------------------------|
| CUST_MSTR_YYYYMMDD.csv         | Add `file_date` (YYYY-MM-DD), load into `CUST_MSTR`                   |
| master_child_export-YYYYMMDD.csv | Add `file_date` + `file_date_key`, load into `master_child`         |
| H_ECOM_ORDER.csv              | Load as-is into `H_ECOM_Orders`                                       |

## 🛠️ Setup Instructions

### 🔧 Step 1: Configure

Edit `config.py` to set:
- PostgreSQL credentials
- Data lake path
- Optional processed directory

### 📦 Step 2: Install Dependencies

```bash
pip install -r requirements.txt

--Let's suppose you have 3 different types of file 1) CUST_MSTR_20191112.csv 2) master_child_export-20191112.csv 3) H_ECOM_ORDER.csv All these files will be in the data lake container You have to fetch all three types of files into their respective folders. Note: There could be multiple files on all 3 types for different dates for example CUST_MSTR_20191112.csv and CUST_MSTR_20191113.csv 1) For the "CUST_MSTR" starting name of the file You have to create an additional column for a date that will fetch the data value from the filename and put it into an additional column Date format: 2019-11-12 and load it into the "CUST_MSTR" table 2) For the "master_child_export" starting name of the file You have to create two additional columns date and date key which will fetch the data from the filename and put it into the additional columns. Date format: 2019-11-12 DateKey format: 20191112 and load it into the "master_child" table 3) for the "H_ECOM_ORDER" type of file you have to load it into the database as it is. and load it into "H_ECOM_Orders" table Note: This process will work on truncate load on a daily basis--
# 🚀 Daily CSV Loader to PostgreSQL

This project reads and processes daily CSV files from a data lake folder. Each file type is processed based on its name pattern and loaded into a specific table using truncate-load.

## 🧾 File Handling Rules

| File Name Pattern            | Transforms                                           | Destination Table    |
|-----------------------------|------------------------------------------------------|----------------------|
| CUST_MSTR_YYYYMMDD.csv      | Adds `file_date` (YYYY-MM-DD)                        | CUST_MSTR            |
| master_child_export-YYYYMMDD.csv | Adds `file_date` + `file_date_key`                | master_child         |
| H_ECOM_ORDER.csv            | Loaded as-is                                        | H_ECOM_Orders        |

## 🛠️ How to Use

1. **Update DB Credentials**  
   Edit `config.py` with your PostgreSQL host/user/password.

2. **Install Python Dependencies**
   ```bash
   pip install -r requirements.txt
