**Query:** Find all the orders that have more than one return.

**Query cost**: 2480.60

```sql
select
	ra.ORDER_ID,
	count(distinct RETURN_ID) TOTAL_RETURNS
from return_adjustment ra
group by ra.ORDER_ID
having count(distinct RETURN_ID)>1;
```
