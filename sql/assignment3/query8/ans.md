**Query:** Find all the orders whose two or more items are completed but the orders are still in the approved status.

**Query cost**: 16127.03

```sql
select
	oi.ORDER_ID,
	oh.STATUS_ID ORDER_STATUS,
	count(oh.ORDER_ID) ITEMS_COUNT
from order_header oh
join order_item oi
	on oi.ORDER_ID = oh.ORDER_ID
	and oh.STATUS_ID = "ORDER_APPROVED"
	and oi.STATUS_ID = "ITEM_COMPLETED"
group by oh.ORDER_ID
having count(oh.ORDER_ID)>=2
;
```
