**Query:** Fetch all the customers created in June 2023.

**Query cost**: 41501637.52

```sql
select
	p.PARTY_ID,
	p.PARTY_TYPE_ID,
	p.CREATED_DATE,
	pr.ROLE_TYPE_ID
from party p
join party_role pr
on
	p.PARTY_TYPE_ID = "PERSON"
	and pr.ROLE_TYPE_ID = "CUSTOMER"
where
	extract(month from p.CREATED_DATE) = 7
	and extract(year from p.CREATED_DATE) = 2023
;
```
