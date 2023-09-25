# sqlite_database_operations
Introduction to the world of databases, starting with SQLite. Integrate data processing with Python, utilize Pandas for exploratory data analysis, and conduct database operations using SQLite.

### Datasets selected
The two datasets I selected are from New York Presbyterian Hospital and Mount Sinai Hospital.

### Account of Exploratory Data Analysis Process
First I loaded the NY Presbyerian Hospital dataset as nypdf. I cleansed the data by checking for missing values. Then, I removed white space from the column names and removed any duplicates. I first grouped by the revenue code and average gross charge for each code. Then, I calculated the mean, median, mode, variange, standard deviation, 25th percentile, and 75th percentile of all the gross charges. Then, I found the range of the gross charges. I also performed multiple imputation. The imputed data contained gross charges, discounted cash price, minimum negotiated charge, and maximum negotiated charge. Afterwards, I grouped it with the revenue code. Later, I combined it all into a statistics table using the ".describe" code. I repeated these steps with the Mount Sinai hospital, but changed the labels based on corresponding column name for the dataset. 

### SQLite Database Setup
1. Import create_engine and sqlite3 by using:
   ```from sqlalchemy import create_engine```
   ```import sqlite3```
2. Create a local database using:
   ```conn = sqlite3.connect('health.db')```
   ```c = conn.cursor()```
3. Create table and include type of data:
   ```c.execute("""
      CREATE TABLE NYP_healthcare
      (
          'revcode text',
          'description text',
          'grosscharges float',
          'discountedcashprice float',
          'minimumnegotiatedcharge float',
          'maximumnegotiatedcharge float'
         );

      """)

      conn.commit()```
4. Insert data into tabla:
   ```sql_query = """
      INSERT INTO NYP_healthcare (
             revcode,
             description,
             grosscharges,
             discountedcashprice,
             minimumnegotiatedcharge,
             maximumnegotiatedcharge
         )
         VALUES (
         '0260',
         'HC IV INFUSION HYDRATION INITIAL 31 MIN-1HR',
         648.00,
         648.00,
         253.05,
         838.20
         );
      """

     print(sql_query)```
5. Commit it into the database using:
   ```conn.commit()```
6. Checking if rows have been populated in table:
   ```query = """

      SELECT *
      from NYP_healthcare;

      """

      c.execute(query)
      print(c.fetchall())```
7. Create engine to connect to the sqlite database:
   ```engine = create_engine('sqlite:///health.db')```
8. Display values created:
   ```NYP_healthcare = pd.read_sql("select * from NYP_healthcare;", conn)```
   ```NYP_healthcare```
