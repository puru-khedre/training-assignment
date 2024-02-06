# Activity 2

      Order Id: HWMDEMO1001
      Order Status: Approved
      Order Items: any two products from catalog.
      Order Items Status: Approved
      Customer Name: Mark Tailor
      Shipping Address:
      HotWax Media Inc.
      136 S MAIN ST #A200
      Salt Lake City, UT,USA
      Zip: 84101
      Phone: 877.736.4080
      Email Address: mark.tailor@hotwaxmedia.com
      Shipping Method: UPS Ground
      Billing Method: Credit Card - Discover
      Billing Address:
      HotWax Media Inc.
      136 S MAIN ST #A200
      Salt Lake City, UT, USA
      Zip: 84101
      Phone: 877.736.4080

## Solution

### Creting order

```xml
<OrderHeader orderId="HWMDEMO1001" orderTypeId="SALES_ORDER" statusId="ORDER_APPROVED" createdBy="mark-tailor" orderDate="2024-02-03 00:00:00.0" entryDate="2024-02-04 00:00:00.0" />
```

![alt text](<../images/Screenshot from 2024-02-06 10-43-48.png>)

### Adding order status

```xml
<OrderStatus orderStatusId="HWMDEMO1001APPR" orderId="HWMDEMO1001" statusId="ORDER_APPROVED" statusUserLogin="mark-tailor" />
```

![alt text](<../images/Screenshot from 2024-02-06 10-54-22.png>)

### Adding order item 1

```xml
<OrderItem orderId="HWMDEMO1001" orderItemSeqId="1" productId="PURU_VARIANT_PROD1" statusId="ITEM_APPROVED" quantity="19" />
<OrderStatus orderStatusId="HWMDEMO10011APPROVED" orderId="HWMDEMO1001" orderItemSeqId="1" statusId="ITEM_APPROVED" />
```

![alt text](<../images/Screenshot from 2024-02-06 10-54-56.png>)

### Adding order item 2

```xml
<OrderItem orderId="HWMDEMO1001" orderItemSeqId="2" productId="PURU_VARIANT_PROD2" statusId="ITEM_APPROVED" quantity="6" />
<OrderStatus orderStatusId="HWMDEMO10012APPROVED" orderId="HWMDEMO1001" orderItemSeqId="2" statusId="ITEM_APPROVED" />
```

![alt text](<../images/Screenshot from 2024-02-06 10-55-26.png>)

### Creating ship groups and association with order items

```xml
<OrderItemShipGroup orderId="HWMDEMO1001" shipGroupSeqId="1" shipmentMethodTypeId="GROUND" carrierPartyId="UPS" />
<OrderItemShipGroupAssoc orderId="HWMDEMO1001" orderItemSeqId="1" shipGroupSeqId="1" quantity="19" />
<OrderItemShipGroupAssoc orderId="HWMDEMO1001" orderItemSeqId="2" shipGroupSeqId="1" quantity="6" />
```

![alt text](<../images/Screenshot from 2024-02-06 10-56-21.png>)

### Adding orderRole for bill and ship to customer

```xml
<OrderRole orderId="HWMDEMO1001" roleTypeId="SHIP_TO_CUSTOMER" partyId="MarkCustomer" />
<OrderRole orderId="HWMDEMO1001" roleTypeId="BILL_TO_CUSTOMER" partyId="MarkCustomer" />
```

![alt text](<../images/Screenshot from 2024-02-06 10-56-30.png>)

### Adding billing and shipping locations

```xml
<OrderContactMech orderId="HWMDEMO1001" contactMechId="10022" contactMechPurposeTypeId="BILLING_LOCATION" />
<OrderContactMech orderId="HWMDEMO1001" contactMechId="10022" contactMechPurposeTypeId="SHIPPING_LOCATION" />
```

### Adding contact number for billing and shipping

```xml
<OrderContactMech orderId="HWMDEMO1001" contactMechId="10024" contactMechPurposeTypeId="PHONE_BILLING" />
<OrderContactMech orderId="HWMDEMO1001" contactMechId="10024" contactMechPurposeTypeId="PHONE_SHIPPING" />
```

![alt text](<../images/Screenshot from 2024-02-06 10-57-35.png>)

### Creting payment method

```xml
<PaymentMethod fromDate="2024-02-01 19:05:50.167" partyId="MarkCustomer" paymentMethodId="10011" paymentMethodTypeId="CREDIT_CARD"/>
```

### Creating an credit card of type Discover

```xml
<CreditCard paymentMethodId="10011" cardType="CCT_DISCOVER" cardNumber="4111111111111112" firstNameOnCard="Mark" lastNameOnCard="Tailor" expireDate="06/2030" />
```

### Adding payment method

```xml
<OrderPaymentPreference orderPaymentPreferenceId="HWPAYPREF1001" orderId="HWMDEMO1001" paymentMethodTypeId="CREDIT_CARD" paymentMethodId="10011" statusId="PAYMENT_AUTHORIZED" />
```

![alt text](<../images/Screenshot from 2024-02-06 10-58-11.png>)
