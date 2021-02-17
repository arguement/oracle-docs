# Oracle commands
---

## Over - Over Which

This command is similar to group by but it allows for for other columns to be added
it can be used with the `partition by` to get groups or used with `order by` to get an accumulation 

### Example
```sql

select sa.*,max(unitprice) over(partition by customerid) from sales sa;

```


```sql

select sa.*,max(unitprice) over(order by customerid) from sales sa;

```

```sql

select sa.*,ROW_NUMBER() over(partition by customerid order by customerid) as co from sales sa;


```


## Cursor
---

These are values that vca be used to loop though. they come with specialised exceptions.

<https://www.oracletutorial.com/plsql-tutorial/plsql-cursor-for-loop/>
<https://www.oracletutorial.com/plsql-tutorial/plsql-cursor-for-loop/>/>

### Example
```sql

set serveroutput on;
declare

    cursor tester is
    select * from sales;

begin


    for i in tester loop
    
        SYS.dbms_output.put_line(i.customerid);
    
    end loop;

end;

```

**Cursor with parameters**
```sql

set serveroutput on;
declare

cursor tester(x number) is
select * from sales where customerid = x;

begin


    for i in tester(100) loop
    
        SYS.dbms_output.put_line(i.customerid);
    
    end loop;

end;

```


## Collections
---

These are essenitally arrays 

<https://oracle-base.com/articles/8i/collections-8i>

```sql

declare
    TYPE temp_table is TABLE of NUMBERS;
    my_val temp_table;
begin
end;
```


## Set operations

Using `multiset` operator you can use set operations in plsql


<https://oracle-base.com/articles/8i/collections-8i>

```sql

SET SERVEROUTPUT ON
DECLARE
  TYPE t_tab IS TABLE OF NUMBER;
  l_tab1 t_tab := t_tab(1,2,3,4,5,6);
  l_tab2 t_tab := t_tab(5,6,7,8,9,10);
BEGIN
  l_tab1 := l_tab1 MULTISET UNION DISTINCT l_tab2;
  
  FOR i IN l_tab1.first .. l_tab1.last LOOP
    DBMS_OUTPUT.put_line(l_tab1(i));
  END LOOP;
END;

```


