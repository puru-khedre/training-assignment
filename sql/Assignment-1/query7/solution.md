**Query:**

Payment captured but not shipped order items:

- Identify orders where payment has been captured, but the items have not been shipped yet or shipment has not yet been created/initiated

**Query cost:** 22724

**Solution:**

```sql
select
    oi.order_id
from
    order_item oi
    join order_payment_preference opp on oi.order_id = opp.order_id
where
    oi.status_id not in (
        'ITEM_CANCELLED',
        'ITEM_REJECTED',
        'ITEM_COMPLETED'
    )
    and opp.status_id = 'PAYMENT_SETTLED';
```

![alt text](image.png)
