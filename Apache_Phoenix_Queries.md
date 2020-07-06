`!outputformat vertical` - List select query columns vertically

`!outputformat table` - List select query columns in tabular format

`!tables` - list all tables

`!describe {table name}` - detailed description of the table

`DROP TABLE IF EXISTS my_table;` - drops the table named my_table

`SELECT * FROM my_table LIMIT 1000;` - selects all columns from my_table limiting the result set to 1000 records

`DELETE FROM my_table WHERE ID= 321;` - deletes a record from my_table where the primary Id is equal to 321

`CREATE INDEX idx_last_updated_date ON sales.opportunity(last_updated_date DESC)` - Creates a secondary index on a table or view.  The index is kept in sync with the table as data changes.  At query time, the optimizer will use the index if it contains all columns referenced in the query to produce an efficient execution plan.

`!quit` - quites SQLLine client
