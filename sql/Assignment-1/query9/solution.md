**Query:**

Find orders where multiple items are grouped and shipped together in a single shipment:

**Query cost:** 71340

**Solution:**

```sql
select
    oisga.ORDER_ID,
    oisga.SHIP_GROUP_SEQ_ID,
    count(*) ITEM_COUNT
from
    order_item_ship_group_assoc oisga
join order_item oi
    on
    oi.ORDER_ID = oisga.ORDER_ID
    and oi.ORDER_ITEM_SEQ_ID = oisga.ORDER_ITEM_SEQ_ID
    and oi.STATUS_ID = "ITEM_COMPLETED"
group by
    oisga.ORDER_ID,
    oisga.SHIP_GROUP_SEQ_ID
having
    count(*)>1
;
```

![alt text](image.png)
