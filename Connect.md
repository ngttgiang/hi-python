# Connect to Oracle using ODBC in Windows

## Confifure in local device
1. To install Oracle Client on the device 
2. Add the connection string on Tnsnames.ora file
3. To configure a user DSN (Data Service Names)

* From **Start Menu** open 'odbc' either 64 or 32 bit depend on the device's properties. (Can be checked by right-clicking on **My Computer**)
* Choose to add new DSN using Oracle driver
* Naming the DSN up to user's convenience

## In Python

1. Install/ load ```pyodbc``` package
2. (Optional) In order to mask the password, can install and load ```getpass``` package

```{python code}
import pyodbc
import getpass

def connect2Oracle(DSN_name):
  username = getpass.getpass('Username')
  password = getpass.getpass('Password')
  con_str='DSN='+DSN_name+';UID='+username+';PWD='+password
  
  connection = pyodbc.connect(con_str)
  cursor = connection.cursor()
  
  return connection, cursor
```

3. Execute SQL agaist Oracle db from Python

```
import pandas as pd

connection, cursor = connect2Oracle('test_DSN')
sql = "Select col1, col2 from table"

# get result into a pandas dataframe 
result = pd.read_sql(sql, connection)

#or just fetch the result
cursor.execute(sql)
cursor.fetchall()

```