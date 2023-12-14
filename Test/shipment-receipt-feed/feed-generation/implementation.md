---
description: Shipment Receipt Feed implementation details -
---

# Implementation

**View Utilized:** ShipmentAndItemAndReceipt

In the service, the ShipmentAndItemAndReceipt view plays a central role in gathering necessary data. Let's break down the entity-finds within the service in a friendly format:

##

## **Eligible Shipment Retrieval:**&#x20;

The initial entity-find is designed to retrieve shipments based on specific conditions. If a `shipmentId` is provided, it fetches the corresponding shipment receipts. Similarly, with a given `shipmentTypeId`, the entity-find retrieves shipment receipts associated with that type. If a `shipmentStatusId` is provided, the entity-find fetches shipment receipts based on the specified status. Additionally, if a date is provided in `sinceReceivedDate`, the entity-find gathers eligible shipment receipts after that particular date.

It's essential to note that the `sinceReceivedDate` corresponds to the `datetimeReceived` field in the ShipmentReceipt entity.

The generation of the feed is influenced by the `productStoreIds`. If only one value is provided in `productStoreIds`, the resulting feed is tailored to that specific product store ID, representing a distinct brand. However, if `productStoreIds` is not provided or contains multiple values, the default prefix 'HOTWAX' is set using the MoquiConf file.

A crucial aspect is that this entity-find specifically focuses on fetching shipment-level details for the eligible Shipment Receipt Feed. This is emphasized by the inclusion of only shipment-level fields in the select criteria.

##

## **Fetching Eligible Shipment Items:**&#x20;

The second entity-find retrieves eligible shipment items based on the condition: **shipmentId:** It fetches details for the order ID existing in the list obtained from the first entity-find.

_Note: This entity-find fetches shipment item-level details since it includes only shipment item-level fields._



## **Fetching Eligible Shipment Receipts:**&#x20;

The third entity-find fetches eligible shipment receipts with conditions: **shipmentId** and **shipmentItemsSeqId:** Included to fetch shipment item receipts for specific shipment IDs and shipment item-seq IDs.

_Note: For each shipment item, valid Shipment Receipts are fetched. This ensures accurate quantity evaluation (sum of `qtyAccepted`) in the next entity-find using these receipt IDs. It's crucial to fetch valid Shipment Receipts to prevent resending quantities already included in earlier feeds._



## **Total Quantity Calculation:**&#x20;

The fourth entity-find calculates the total quantity (`sum(qtyAccepted)`) of eligible shipment receipts. This aggregation ensures an accurate representation of the cumulative accepted quantity in the feed.

This structured breakdown helps beginners understand the step-by-step process of how the service leverages the view to gather essential information.
