# DATA CLEANING


```python
# get sales data
import pandas as pd
sales_data = pd.read_csv('sales_data.csv')
sales_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SaleID</th>
      <th>Product_ID</th>
      <th>Quantity</th>
      <th>Price</th>
      <th>SaleDate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>101</td>
      <td>2</td>
      <td>19.99</td>
      <td>2024-11-01</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>102</td>
      <td>1</td>
      <td>29.99</td>
      <td>2024-11-02</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>103</td>
      <td>3</td>
      <td>NaN</td>
      <td>2024-11-03</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>101</td>
      <td>5</td>
      <td>19.99</td>
      <td>2024-11-04</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>104</td>
      <td>2</td>
      <td>39.99</td>
      <td>2024-11-05</td>
    </tr>
  </tbody>
</table>
</div>




```python
# get inventory data
inventory_data = pd.read_excel('product_inventory.xlsx')
inventory_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ProductID</th>
      <th>ProductName</th>
      <th>Stock</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>101</td>
      <td>Widget A</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>102</td>
      <td>Gadget B</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>103</td>
      <td>Thingamajig C</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>104</td>
      <td>Doohickey D</td>
      <td>8</td>
    </tr>
    <tr>
      <th>4</th>
      <td>105</td>
      <td>Contraption E</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
# find number of missing values in sales data
sales_data.isna().sum()
```




    SaleID        0
    Product_ID    0
    Quantity      0
    Price         1
    SaleDate      0
    dtype: int64




```python
# fill the missing value with the mean value of that column
sales_data['Price'].fillna(sales_data['Price'].mean(), inplace=True)
sales_data
```

    C:\Users\cyndi\AppData\Local\Temp\ipykernel_43796\2523382436.py:2: FutureWarning: A value is trying to be set on a copy of a DataFrame or Series through chained assignment using an inplace method.
    The behavior will change in pandas 3.0. This inplace method will never work because the intermediate object on which we are setting values always behaves as a copy.
    
    For example, when doing 'df[col].method(value, inplace=True)', try using 'df.method({col: value}, inplace=True)' or df[col] = df[col].method(value) instead, to perform the operation inplace on the original object.
    
    
      sales_data['Price'].fillna(sales_data['Price'].mean(), inplace=True)
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SaleID</th>
      <th>Product_ID</th>
      <th>Quantity</th>
      <th>Price</th>
      <th>SaleDate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>101</td>
      <td>2</td>
      <td>19.99</td>
      <td>2024-11-01</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>102</td>
      <td>1</td>
      <td>29.99</td>
      <td>2024-11-02</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>103</td>
      <td>3</td>
      <td>27.49</td>
      <td>2024-11-03</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>101</td>
      <td>5</td>
      <td>19.99</td>
      <td>2024-11-04</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>104</td>
      <td>2</td>
      <td>39.99</td>
      <td>2024-11-05</td>
    </tr>
  </tbody>
</table>
</div>




```python
# find number of missing values in inventory data
inventory_data.isna().sum()
```




    ProductID      0
    ProductName    0
    Stock          0
    dtype: int64




```python
# Verify cleaning steps
print("\nCleaned Sales Data:")
print(sales_data.head())
print("\nCleaned Inventory Data:")
print(inventory_data.head())
    
```

    
    Cleaned Sales Data:
       SaleID  Product_ID  Quantity  Price    SaleDate
    0       1         101         2  19.99  2024-11-01
    1       2         102         1  29.99  2024-11-02
    2       3         103         3  27.49  2024-11-03
    3       4         101         5  19.99  2024-11-04
    4       5         104         2  39.99  2024-11-05
    
    Cleaned Inventory Data:
       ProductID    ProductName  Stock
    0        101       Widget A     10
    1        102       Gadget B      5
    2        103  Thingamajig C      7
    3        104    Doohickey D      8
    4        105  Contraption E      3
    


```python
# rename column ProductID AS Product_ID
inventory_data.rename(columns = {"ProductID":"Product_ID"}, inplace = True)
```


```python
inventory_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Product_ID</th>
      <th>ProductName</th>
      <th>Stock</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>101</td>
      <td>Widget A</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>102</td>
      <td>Gadget B</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>103</td>
      <td>Thingamajig C</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>104</td>
      <td>Doohickey D</td>
      <td>8</td>
    </tr>
    <tr>
      <th>4</th>
      <td>105</td>
      <td>Contraption E</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
# as these two dataset has the same column name Product_ID now, we can merge them together by left join
merged_data = pd.merge(sales_data, inventory_data, on='Product_ID', how='left') 
```


```python
merged_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SaleID</th>
      <th>Product_ID</th>
      <th>Quantity</th>
      <th>Price</th>
      <th>SaleDate</th>
      <th>ProductName</th>
      <th>Stock</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>101</td>
      <td>2</td>
      <td>19.99</td>
      <td>2024-11-01</td>
      <td>Widget A</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>102</td>
      <td>1</td>
      <td>29.99</td>
      <td>2024-11-02</td>
      <td>Gadget B</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>103</td>
      <td>3</td>
      <td>27.49</td>
      <td>2024-11-03</td>
      <td>Thingamajig C</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>101</td>
      <td>5</td>
      <td>19.99</td>
      <td>2024-11-04</td>
      <td>Widget A</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>104</td>
      <td>2</td>
      <td>39.99</td>
      <td>2024-11-05</td>
      <td>Doohickey D</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
!jupyter nbconvert --to markdown data_cleaning.ipynb
```


