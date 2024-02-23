**Query:**

Shipping Refund in the last month:

- Calculate the refunds issued specifically for shipping charges in the last month.

**Query cost:** 839

**Solution:**

```sql
select
    sum(ra.AMOUNT) TOTAL_REFUNDS
from
    return_status rs
join return_adjustment ra
    on rs.STATUS_ID = 'RETURN_COMPLETED'
    and rs.RETURN_ID = ra.RETURN_ID
    and ra.RETURN_ADJUSTMENT_TYPE_ID = 'RET_SHIPPING_ADJ'
join return_header rh
    on rs.RETURN_ID = rh.RETURN_ID
    and rs.STATUS_ID = rh.STATUS_ID
where
    datediff(
        date_sub(curdate(), interval day(curdate()) day),
        rs.STATUS_DATETIME
    ) between 0
    and 30;
```

**No data found**
