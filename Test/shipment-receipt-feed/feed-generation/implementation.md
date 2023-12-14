---
description: Shipment Receipt Feed implementation details -
---

# Implementation

**View Utilized:** ShipmentAndItemAndReceipt

The first entity-find uses conditions like `shipmentId`, `shipmentTypeId`, `shipmentStatusId`, and `sinceReceivedDate`. If a specific shipment ID is provided, the view fetches receipts exclusively for that ID.&#x20;

Similarly, it caters to specified shipment types or status IDs and considers a given date for receipt eligibility. This `sinceReceivedDate` aligns with the `datetimeReceived` field in the Shipment Receipt entity.

The service also utilizes `productStoreIds` for feed generation. If only one value is provided, the feed is tailored to that product store ID, representing a particular brand. Otherwise, if no values or multiple values are present, the default prefix 'HOTWAX' is set. This entity-find focuses on fetching shipment-level details for the eligible Shipment Receipt Feed, considering only shipment-level fields.

The second entity-find on the ShipmentAndItemAndReceipt view retrieves eligible shipment items based on the `shipmentId` obtained from the first entity-find. This entity-find specifically fetches shipment item details since the select-field includes only shipment item-level fields.

A third entity-find on the ShipmentAndItemAndReceipt view fetches eligible Shipment Receipts. Conditions on `shipmentId` and `shipmentItemsSeqId` are included to retrieve shipment item receipts for designated shipment IDs and shipment Item Seq IDs. The goal is to fetch valid Shipment Receipts for each shipment item, ensuring accurate quantity evaluation in the next entity-find. This prevents duplication of quantities sent in earlier feeds.

Lastly, a fourth entity-find calculates the total quantity, i.e., the sum of `qtyAccepted`, eligible shipment receipts. This approach ensures accurate aggregation of accepted quantities within the feed.
