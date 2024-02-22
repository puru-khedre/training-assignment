**Query:**

Shipment by Tracking number

- View or analyze shipments based on their unique tracking numbers. Each shipment is identified and tracked using a specific tracking number.

**Query cost:** 10184

**Solution:**

```sql
select
    sprs.shipment_id,
    sprs.shipment_package_seq_id,
    sprs.shipment_route_segment_id,
    sprs.tracking_code
from
    shipment_package_route_seg sprs
where
    sprs.tracking_code is not null
;
```

![alt text](image.png)
