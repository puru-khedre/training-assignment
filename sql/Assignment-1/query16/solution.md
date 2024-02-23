**Query:**

Send sale orders shipped from the warehouse:

- Identify send sale orders that have been shipped from the warehouse.

**Query cost:** 2632

**Solution:**

```sql
select
    oh.ORDER_ID,
    oh.SALES_CHANNEL_ENUM_ID,
    f.FACILITY_TYPE_ID
from
    order_header oh
    join facility f on f.FACILITY_ID = oh.ORIGIN_FACILITY_ID
    and oh.SALES_CHANNEL_ENUM_ID = 'POS_SALES_CHANNEL'
where
    f.FACILITY_TYPE_ID = 'WAREHOUSE';
```

**No data found**
