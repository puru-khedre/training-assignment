# Activity 1

1. Creating order

   ```xml
   <entity-engine-xml>
      <OrderHeader orderId="HWMDEMO1000" orderTypeId="SALES_ORDER" statusId="ORDER_CREATED" createdBy="mark-tailor" orderDate="2024-02-03 00:00:00.0" entryDate="2024-02-04 00:00:00.0" />
   </entity-engine-xml>
   ```

   ![alt text](<../images/Screenshot from 2024-02-05 19-00-25.png>)

2. Creating order status

   ```xml
   <entity-engine-xml>
      <OrderStatus orderStatusId="HWMDEMO1000CREATED" orderId="HWMDEMO1000" statusId="ORDER_CREATED" statusUserLogin="mark-tailor" />
   </entity-engine-xml>
   ```

    ![alt text](<../images/Screenshot from 2024-02-05 19-10-25.png>)

3. Adding order items

   ```xml
   <entity-engine-xml>
      <OrderItem orderId="HWMDEMO1000" orderItemSeqId="1" productId="PURU_VARIANT_PROD1" statusId="ITEM_CREATED" quantity="23"/>
      <OrderStatus orderStatusId="HWMDEMO10001CREATED" orderId="HWMDEMO1000" orderItemSeqId="1" statusId="ITEM_CREATED" />
      <OrderItem orderId="HWMDEMO1000" orderItemSeqId="2" productId="PURU_VARIANT_PROD2" statusId="ITEM_CREATED" quantity="3"/>
      <OrderStatus orderStatusId="HWMDEMO10002CREATED" orderId="HWMDEMO1000" orderItemSeqId="2" statusId="ITEM_CREATED" />
    </entity-engine-xml>
   ```

    ![alt text](<../images/Screenshot from 2024-02-05 19-14-52.png>)

4. Adding billing and shipping location

   ```xml
   <entity-engine-xml>
      <OrderContactMech orderId="HWMDEMO1000" contactMechId="10022" contactMechPurposeTypeId="BILLING_LOCATION"/>
      <OrderContactMech orderId="HWMDEMO1000" contactMechId="10022" contactMechPurposeTypeId="SHIPPING_LOCATION"/>
   </entity-engine-xml>
   ```

5. Adding order roles for bill and ship to customer

   ```xml
   <entity-engine-xml>
        <OrderRole orderId="HWMDEMO1000" roleTypeId="SHIP_TO_CUSTOMER" partyId="MarkCustomer"/>
        <OrderRole orderId="HWMDEMO1000" roleTypeId="BILL_TO_CUSTOMER" partyId="MarkCustomer"/>
   </entity-engine-xml>
   ```

6. Adding other contact mechanism

   ```xml
   <entity-engine-xml>
        <OrderContactMech orderId="HWMDEMO1000" contactMechId="10024" contactMechPurposeTypeId="PHONE_BILLING"/>
        <OrderContactMech orderId="HWMDEMO1000" contactMechId="10024" contactMechPurposeTypeId="PHONE_SHIPPING"/>
        <OrderContactMech orderId="HWMDEMO1000" contactMechId="10023" contactMechPurposeTypeId="PRIMARY_EMAIL"/>
   </entity-engine-xml>
   ```

   ![alt text](<../images/Screenshot from 2024-02-05 19-33-31.png>)

7. Creating ship groups and association with order items

   ```xml
   <entity-engine-xml>
      <OrderItemShipGroup orderId="HWMDEMO1000" shipGroupSeqId="1" shipmentMethodTypeId="GROUND" carrierPartyId="UPS" />
      <OrderItemShipGroupAssoc orderId="HWMDEMO1000" orderItemSeqId="1" shipGroupSeqId="1" quantity="23"/>
      <OrderItemShipGroupAssoc orderId="HWMDEMO1000" orderItemSeqId="2" shipGroupSeqId="1" quantity="3"/>
   </entity-engine-xml>
   ```

   ![alt text](<../images/Screenshot from 2024-02-05 19-23-02.png>)

8. Adding payment method

   ```xml
   <entity-engine-xml>
      <OrderPaymentPreference orderPaymentPreferenceId="PKPAYPREF1000" orderId="HWMDEMO1000" paymentMethodTypeId="CREDIT_CARD" paymentMethodId="10010" statusId="PAYMENT_AUTHORIZED" />
   </entity-engine-xml>
   ```

    ![alt text](<../images/Screenshot from 2024-02-05 19-24-36.png>)
