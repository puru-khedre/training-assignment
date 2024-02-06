# Activity 3

    Order Id: HWMDEMO1001
    Order Status: Cancelled
    Order Items: any two products from catalog.
    Order Items Status: Cancelled
    Customer Name: Mark Tailor
    Shipping Address:
    HotWax Media Inc.
    136 S MAIN ST #A200
    Salt Lake City, UT, USA
    Zip: 84101
    Phone: 877.736.4080
    Email Address: mark.tailor@hotwaxmedia.com
    Shipping Method: FEDEX Ground
    Billing Method: COD
    Billing Address:
    HotWax Media Inc.
    136 S MAIN ST #A200
    Salt Lake City, UT, USA
    Zip: 84101
    Phone: 877.736.4080

## Solution

### Cancelling an order

```xml
<OrderHeader orderId="HWMDEMO1001" statusId="ORDER_CANCELLED" />
```

### Adding cancelled status to order status

```xml
<OrderStatus orderStatusId="HWMDEMO1001CANC" orderId="HWMDEMO1001" statusId="ORDER_CANCELLED" statusUserLogin="mark-tailor" />
```

![alt text](<../images/Screenshot from 2024-02-06 11-56-03.png>)

### Cancelling order item 1

```xml
<OrderItem orderId="HWMDEMO1001" orderItemSeqId="1" statusId="ITEM_CANCELLED" />
<OrderStatus orderStatusId="HWMDEMO10011CANC" orderId="HWMDEMO1001" orderItemSeqId="1" statusId="ITEM_CANCELLED" />
```

### Cancelling order item 2

```xml
<OrderItem orderId="HWMDEMO1001" orderItemSeqId="2" statusId="ITEM_CANCELLED" />
<OrderStatus orderStatusId="HWMDEMO10012CANC" orderId="HWMDEMO1001" orderItemSeqId="2" statusId="ITEM_CANCELLED" />
```

![alt text](<../images/Screenshot from 2024-02-06 11-57-33.png>)

### Adding email address contact mech

```xml
<OrderContactMech orderId="HWMDEMO1001" contactMechId="10023" contactMechPurposeTypeId="PRIMARY_EMAIL" />
```

### Updating shipping method of order ship group

```xml
<OrderItemShipGroup orderId="HWMDEMO1001" shipGroupSeqId="1" carrierPartyId="FEDEX" />
```

![alt text](<../images/Screenshot from 2024-02-06 12-00-09.png>)

### Creting payment method COD type

```xml
<PaymentMethod fromDate="2024-02-01 19:05:50.167" partyId="MarkCustomer" paymentMethodId="10012" paymentMethodTypeId="EXT_COD"/>
```


### Adding payment method

```xml
<OrderPaymentPreference orderPaymentPreferenceId="HWPAYPREF1001" orderId="HWMDEMO1001" paymentMethodTypeId="EXT_COD" paymentMethodId="10012" />
```
