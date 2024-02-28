**Query:** Fetch the following columns for completed order items for sales orders of SM_STORE product store and that are physical items.
- ORDER_ID
- ORDER_ITEM_SEQ_ID
- PRODUCT_ID
- PRODUCT_TYPE_ID
- IS_PHYSICAL
- IS_DIGITAL
- SALES_CHANNEL_ENUM_ID
- ORDER_DATE
- ENTRY_DATE
- STATUS_ID
- STATUS_DATETIME
- ORDER_TYPE_ID
- PRODUCT_STORE_ID 

**Query cost**: 405900.29

```sql
select
	oh.ORDER_ID,
	oi.ORDER_ITEM_SEQ_ID,
	p.PRODUCT_ID,
	p.PRODUCT_TYPE_ID,
	pt.IS_PHYSICAL,
	pt.IS_DIGITAL,
	oh.SALES_CHANNEL_ENUM_ID,
	oh.ORDER_DATE,
	oh.ENTRY_DATE,
	os.STATUS_ID,
	os.STATUS_DATETIME,
	oh.ORDER_TYPE_ID,
	oh.PRODUCT_STORE_ID
from order_header oh
join order_item oi
	on oh.ORDER_TYPE_ID ='SALES_ORDER'
	and oh.PRODUCT_STORE_ID = 'SM_STORE'
	and oh.ORDER_ID = oi.ORDER_ID
join order_status os
	on os.ORDER_ID = oi.ORDER_ID
	and os.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID
	and os.STATUS_ID = "ITEM_COMPLETED"
join product p
	on p.PRODUCT_ID = oi.PRODUCT_ID
join product_type pt
	on p.PRODUCT_TYPE_ID = pt.PRODUCT_TYPE_ID
	and pt.IS_PHYSICAL = "Y";
```
