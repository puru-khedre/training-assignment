# Type entities in Moqui/OFBiz

## Some of the Type entities in OFBiz

| TABLE_NAME                     | REMAINS IN MOQUI |
| ------------------------------ | ---------------- |
| BENEFIT_TYPE                   | YES              |
| CARRIER_SHIPMENT_BOX_TYPE      | YES              |
| COMMUNICATION_EVENT_TYPE       | YES              |
| ENUMERATION_TYPE               | YES              |
| FIN_ACCOUNT_TYPE               | YES              |
| ROLE_TYPE                      | YES              |
| SHIPMENT_BOX_TYPE              | YES              |
| SYSTEM_MESSAGE_TYPE            | YES              |
| STATUS_TYPE                    | YES              |
| CARRIER_SHIPMENT_METH_BOX_TYPE | No               |
| CONTACT_MECH_PURPOSE_TYPE      | No               |
| CONTACT_MECH_TYPE              | No               |
| FACILITY_TYPE                  | No               |
| GEO_ASSOC_TYPE                 | No               |
| GEO_TYPE                       | No               |
| GOOD_IDENTIFICATION_TYPE       | No               |
| INVENTORY_ITEM_TYPE            | No               |
| ORDER_ADJUSTMENT_TYPE          | No               |
| ORDER_ITEM_TYPE                | No               |
| ORDER_TYPE                     | No               |
| PARTY_IDENTIFICATION_TYPE      | No               |
| PARTY_TYPE                     | No               |
| PROD_CATALOG_CATEGORY_TYPE     | No               |
| PRODUCT_ASSOC_TYPE             | No               |
| PRODUCT_CATEGORY_TYPE          | No               |
| PRODUCT_FEATURE_APPL_TYPE      | No               |
| PRODUCT_FEATURE_TYPE           | No               |
| PRODUCT_TYPE                   | No               |
| RETURN_ADJUSTMENT_TYPE         | No               |
| RETURN_HEADER_TYPE             | No               |
| RETURN_TYPE                    | No               |
| SHIPMENT_CONTACT_MECH_TYPE     | No               |
| SHIPMENT_METHOD_TYPE           | No               |
| SHIPMENT_TYPE                  | No               |
| UOM_TYPE                       | No               |

## Some Type entities in Moqui

| TABLE_NAME                |
| ------------------------- |
| ENUMERATION_TYPE          |
| ROLE_TYPE                 |
| FACILITY_LOCATION_TYPE    |
| PARTY_SETTING_TYPE        |
| SHIPMENT_BOX_TYPE         |
| SHIPPING_GATEWAY_BOX_TYPE |
| STATUS_TYPE               |
| UOM_DIMENSION_TYPE        |
| BENEFIT_TYPE              |
| CARRIER_SHIPMENT_BOX_TYPE |
| COMMUNICATION_EVENT_TYPE  |
| FINANCIAL_ACCOUNT_TYPE    |

## How type tables are handles with help of enumerations in Moqui

Here let's take an example of `FACILITY_TYPE` entity in OFBiz

| FACILITY_TYPE_ID    | PARENT_TYPE_ID      | DESCRIPTION                                       |
| ------------------- | ------------------- | ------------------------------------------------- |
| BACKORDER           | VIRTUAL_FACILITY    | Backorder                                         |
| BUILDING            |                     | Building                                          |
| CALL_CENTER         |                     | Call Center                                       |
| CONFIGURATION       | VIRTUAL_FACILITY    | Facility for setting up product level threshold   |
| DISTRIBUTION_CENTER |                     | Distribution Center                               |
| FLOOR               |                     | Floor                                             |
| GENERAL_OPERATIONS  | VIRTUAL_FACILITY    | Facility for general operations downloaded orders |
| NA                  | VIRTUAL_FACILITY    | Not Available                                     |
| OFFICE              |                     | Office                                            |
| OUTLET_STORE        | PHYSICAL_STORE      | Outlet Store                                      |
| OUTLET_WAREHOUSE    | DISTRIBUTION_CENTER | Outlet Warehouse                                  |
| PHYSICAL_STORE      |                     | Physical Store                                    |
| PLANT               |                     | Plant                                             |
| PRE_ORDER           | VIRTUAL_FACILITY    | Pre order                                         |
| RETAIL_STORE        | PHYSICAL_STORE      | Retail Store                                      |
| ROOM                |                     | Room                                              |
| SEND_SALE_QUEUE     | VIRTUAL_FACILITY    | Send Sale Queue Facility                          |
| VIRTUAL_FACILITY    |                     | Virtual Facility                                  |
| WAREHOUSE           | DISTRIBUTION_CENTER | Warehouse                                         |

**Steps to convert OFBiz type table to enumerations in Moqui:**

1. Create an entry of `FacilityType` in `EnumerationType` table of Moqui
2. Add all the values of `FACILITY_TYPE_ID` column in `Enumeration` table of Moqui
3. In each record, the value of `ENUM_TYPE_ID` should be `FacilityType`

**After conversion these is actual values in `Enumeration` table of moqui, specially to manage facility types:**

| ENUM_ID         | ENUM_TYPE_ID | DESCRIPTION     |
| --------------- | ------------ | --------------- |
| FcTpBlock       | FacilityType | Block           |
| FcTpBlockGroup  | FacilityType | Block Group     |
| FcTpBuilding    | FacilityType | Building        |
| FcTpCallCenter  | FacilityType | Call Center     |
| FcTpDataCenter  | FacilityType | Data Center     |
| FcTpDock        | FacilityType | Dock            |
| FcTpFloor       | FacilityType | Floor           |
| FcTpLand        | FacilityType | Land            |
| FcTpLine        | FacilityType | Production Line |
| FcTpOffice      | FacilityType | Office          |
| FcTpPlant       | FacilityType | Plant           |
| FcTpRetailStore | FacilityType | Retail Store    |
| FcTpRoom        | FacilityType | Room            |
| FcTpWarehouse   | FacilityType | Warehouse       |

**Key points:**

- The column `ENUM_ID` in `Enumeration` table of moqui contains different type values
- The column `ENUM_TYPE_ID` in `Enumeration` table shows that the enum is of which type
- In our case, we create a new enum type `FacilityType` so that we can distinguish that these enum values are used for representing different facility type
- Also, the `ENUM_TYPE_ID` acts as the purpose of corresponding enum values
- A `DESCRIPTION` column is for displaying the description of enum values
- Now there is `FACILITY_TYPE_ENUM_ID` column in `Facility` table in Moqui instead of `FACILITY_TYPE_ID` in OFBiz which is used to store the enum value of that facility type
- In OFBiz, the facility entity has column `FACILITY_TYPE_ID` which is a foreign key to `FACILITY_TYPE` table
- In Moqui, the facility entity has column `FACILITY_TYPE_ENUM_ID` which is a foreign key to `Enumeration` table
- Same way we can remove the type of entities and manage them by leveraging the enumerations
