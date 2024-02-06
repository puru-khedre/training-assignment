# Activity 4

Order Id: HWMDEMO1001
Order Status: Completed
Order Items: any two products from catalog.
Order Items Status: Completed
Customer Name: Mark Tailor
Shipping Address:
HotWax Media Inc.
307 W 200 S
Suite 4003
Salt Lake City, UT
Zip: 84101
Phone: 888.405.2667
Email Address: <mark.tailor@hotwaxmedia.com>
Shipping Method: UPS Ground
Billing Method: Credit Card - AMEX
Billing Address:
HotWax Media Inc.
307 W 200 S
Suite 4003
Salt Lake City, UT
Zip: 84101
Phone: 888.405.2667

OrderShipment:

shipmentId: HwmDemo1000

## Solution

1. Creating order

   ```xml
    <OrderHeader orderId="HWMDEMO1002" orderTypeId="SALES_ORDER" statusId="ORDER_COMPLETED" createdBy="mark-tailor" orderDate="2024-02-03 00:00:00.0" entryDate="2024-02-04 00:00:00.0" />
   ```

2. Creating order status

   ```xml
    <OrderStatus orderStatusId="HWMDEMO1002CMPL" orderId="HWMDEMO1002" statusId="ORDER_COMPLETED" statusUserLogin="mark-tailor" />
   ```

    ![alt text](<Screenshot from 2024-02-06 14-25-49.png>)

3. Adding order items

   ```xml
    <OrderItem orderId="HWMDEMO1002" orderItemSeqId="1" productId="PURU_VARIANT_PROD1" statusId="ITEM_COMPLETED" quantity="23"/>
    <OrderStatus orderStatusId="HWMDEMO10021CMPL" orderId="HWMDEMO1002" orderItemSeqId="1" statusId="ITEM_COMPLETED" />
    <OrderItem orderId="HWMDEMO1002" orderItemSeqId="2" productId="PURU_VARIANT_PROD2" statusId="ITEM_COMPLETED" quantity="3"/>
    <OrderStatus orderStatusId="HWMDEMO10022CMPL" orderId="HWMDEMO1002" orderItemSeqId="2" statusId="ITEM_COMPLETED" />
   ```

    ![alt text](<Screenshot from 2024-02-06 14-27-34.png>)

4. Creating location for billing and shipping

    ```xml
    <ContactMech contactMechId="HWDEMOADDR1002" contactMechTypeId="POSTAL_ADDRESS" />
    <PostalAddress 
    address1="HotWax Media Inc. 307 W 200 S Suite 4003 Salt Lake City, UT" city="Salt Lake City" contactMechId="HWDEMOADDR1002" countryGeoId="USA" postalCode="84101" stateProvinceGeoId="AA" toName="Mark Tailor"/>
    ```

5. Adding billing and shipping location

   ```xml
    <OrderContactMech orderId="HWMDEMO1002" contactMechId="HWDEMOADDR1002" contactMechPurposeTypeId="BILLING_LOCATION"/>
    <OrderContactMech orderId="HWMDEMO1002" contactMechId="HWDEMOADDR1002" contactMechPurposeTypeId="SHIPPING_LOCATION"/>
   ```

   ![alt text](<Screenshot from 2024-02-06 15-02-45.png>)
   ![alt text](<Screenshot from 2024-02-06 15-02-56.png>)

6. Adding order roles for bill and ship to customer

   ```xml
    <OrderRole orderId="HWMDEMO1002" roleTypeId="SHIP_TO_CUSTOMER" partyId="MarkCustomer"/>
    <OrderRole orderId="HWMDEMO1002" roleTypeId="BILL_TO_CUSTOMER" partyId="MarkCustomer"/>
   ```

   ![alt text](<Screenshot from 2024-02-06 15-03-03.png>)

7. Creating telecom number

   ```xml
   <ContactMech contactMechId="HWDEMO1002TELE" contactMechTypeId="TELECOM_NUMBER" />
   <TelecomNumber areaCode="405" contactMechId="HWDEMO1002TELE" contactNumber="2667" countryCode="888" />
   ```

7. Adding other contact mechanism

   ```xml
    <OrderContactMech orderId="HWMDEMO1002" contactMechId="HWDEMO1002TELE" contactMechPurposeTypeId="PHONE_BILLING"/>
    <OrderContactMech orderId="HWMDEMO1002" contactMechId="HWDEMO1002TELE" contactMechPurposeTypeId="PHONE_SHIPPING"/>
    <OrderContactMech orderId="HWMDEMO1002" contactMechId="10023" contactMechPurposeTypeId="PRIMARY_EMAIL"/>
   ```

   ![alt text](<Screenshot from 2024-02-06 15-04-06.png>)

8. Creating ship groups and association with order items

   ```xml
    <OrderItemShipGroup orderId="HWMDEMO1002" shipGroupSeqId="1" shipmentMethodTypeId="GROUND" carrierPartyId="UPS" />
    <OrderItemShipGroupAssoc orderId="HWMDEMO1002" orderItemSeqId="1" shipGroupSeqId="1" quantity="23"/>
    <OrderItemShipGroupAssoc orderId="HWMDEMO1002" orderItemSeqId="2" shipGroupSeqId="1" quantity="3"/>
   ```

   ![alt text](<Screenshot from 2024-02-06 15-05-25.png>)

10. Creating payment method

    ```xml
    <PaymentMethod paymentMethodId="PAYPREF1002" paymentMethodTypeId="CREDIT_CARD" partyId="MarkCustomer" />
    <CreditCard paymentMethodId="PAYPREF1002" cardType="CCT_AMERICANEXPRESS" cardNumber="4111111111111113" firstNameOnCard="Mark" lastNameOnCard="Tailor" expireDate="06/2030" />
    ```

9. Adding payment method

   ```xml
    <OrderPaymentPreference orderPaymentPreferenceId="HWDEMO1002PAYPREF" orderId="HWMDEMO1002" paymentMethodTypeId="CREDIT_CARD" paymentMethodId="PAYPREF1002" statusId="PAYMENT_AUTHORIZED" />
   ```

    ![alt text](<Screenshot from 2024-02-06 15-06-40.png>)
