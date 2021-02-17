# Spooling


* **colsep** - is the separator character used to split your columns. For a .csv file, this is a simple comma.

* **headsep** - is the separator character for the header row (if you require one). In this example we’re not outputting the header row, so we’ll leave this off.

* **pagesize** - is the number of lines “per page.” This is a slightly archaic setting that is intended for printing without having too many lines per page. With a value of 0, we don’t use pages since we’re outputting to a file. If you elect to show the header row, set pagesize to a very large number (larger than the expected number of record results in the query), so your header row will only show up one time rather than once “per page.”

* **trimspool** - set to on simply removes trailing whitespace.

* **linesize** - the # value should be the total number of output columns in your resulting query.

* **numwidth** - the column width (number of character spaces) used when outputting numeric values.

```sql
set colsep ,
set headsep off
set pagesize 0
set trimspool on
set feedback off;
set linesize 200


spool 'jason.csv'

select * from employee;

spool off


spool 'jordan.csv'

select * from sales;

spool off


```