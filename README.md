GreenplumPython is a Python library that enables the user to interact with database in a Pythonic way.

GreenplumPython provides a [pandas](https://pandas.pydata.org/)-like DataFrame API that
1. looks familiar and intuitive to Python users
2. is powerful to do complex analytics, such as statistical analysis, with UDFs and UDAs
3. encapsulates common best practices and avoids common pitfalls in Greenplum, compared to writing SQL directly

## Installation

To install the latest development version, do

```bash
pip3 install --user git+https://github.com/greenplum-db/GreenplumPython
```

To install the latest released version, do

```bash
pip3 install --user greenplum-python
```

**Note:** The `--user` option in an active virtual environment will install to the local user python location.
Since a user location doesn't make sense for a virtual environment, to install the **GreenplumPython** library,
just remove `--user` from the above commands.

## Simple Demo Code
```python
import greenplumpython as gp
db = gp.database("postgresql://ivan:ivan@localhost/ivan")

cols1 = ["category_name", "category_id"]
rows1 = [ ('Smart Phone', 1), ('Laptop', 2), ('DataFramet', 3) ]

cols2 = ["product_name", "category_id","price"]
rows2 = [ ('iPhone', 1, 1019), ('Samsung Galaxy', 1, 959), ('HP Elite',2,1503),
        ('Lenovo Thinkpad',2,1429), ('iPad',3,589), ('Kindle Fire',3,150) ]

# Create a DataFrame in GreenplumPython
categories = gp.DataFrame.from_rows(rows=rows1, column_names=cols1, db=db)
categories.save_as("categories", cols1, temp=False)

products = gp.DataFrame.from_rows(rows=rows2, column_names=cols2, db=db)
products.save_as("products", column_names=cols2, temp=False)
```

```python
import greenplumpython as gp
db = gp.database("postgresql://ivan:ivan@localhost/ivan")

products = db.create_dataframe(table_name="products")
print(products)
```
