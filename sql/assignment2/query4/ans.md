**Query:** Fetch the following columns for created orders. These should be sales orders.

- ORDER_ID
- TOTAL_AMOUNT
- PAYMENT_METHOD
- SHOPIFY_ORDER_NAME

NOTE:

1. The total amount represents the total amount of the order.
2. The payment method is the method by which payment was made, like Cash, mastercard, visa, paypal, etc.

**Query cost**: 5591.60

```sql
select
	oh.ORDER_ID ORDER_ID,
	oh.GRAND_TOTAL TOTAL_AMOUNT,
	pmt.DESCRIPTION PAYMENT_METHOD,
	oi.ORDER_IDENTIFICATION_TYPE_ID,
	oi.ID_VALUE
from order_header oh
join order_identification oi
	on oi.ORDER_ID = oh.ORDER_ID
	and oi.ORDER_IDENTIFICATION_TYPE_ID = "SHOPIFY_ORD_NAME"
	and oh.ORDER_TYPE_ID = 'SALES_ORDER'
	and oh.STATUS_ID = "ORDER_CREATED"
join order_payment_preference opp, payment_method_type pmt
where
	opp.ORDER_ID = oh.ORDER_ID
	and opp.PAYMENT_METHOD_TYPE_ID = pmt.PAYMENT_METHOD_TYPE_ID
;
```
