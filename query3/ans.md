**Query:** Fetch the order id and contact mech id for the shipping address of the orders completed in October of 2023.

**Query cost**: 87742.42

```sql
select
	oh.ORDER_ID,
	ocm.CONTACT_MECH_ID,
	CONTACT_MECH_PURPOSE_TYPE_ID,
	os.STATUS_DATETIME,
	os.STATUS_ID ORDER_ID
from order_contact_mech ocm
join order_header oh
	on oh.ORDER_ID = ocm.ORDER_ID
	and ocm.CONTACT_MECH_PURPOSE_TYPE_ID = 'SHIPPING_LOCATION'
join order_status os
	on oh.ORDER_ID = os.ORDER_ID
     and oh.STATUS_ID = "ORDER_COMPLETED"
where
	extract(MONTH from os.STATUS_DATETIME) = 10
	and extract(YEAR from os.STATUS_DATETIME) = 2023
;
```
