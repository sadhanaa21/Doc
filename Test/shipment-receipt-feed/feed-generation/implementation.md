# Implementation

**View Utilized:** ShipmentAndItemAndReceipt

In the service, the ShipmentAndItemAndReceipt view is employed for fetching relevant data. Here's a breakdown of the entity-finds within the service:

1.  **Eligible Shipment Retrieval:** The initial entity-find fetches eligible shipments using specific conditions:

    * `shipmentId`: If provided in the service, the view fetches shipment receipts exclusively for that shipment ID.
    * `shipmentTypeId`: If the shipment type ID is provided, the service fetches shipment receipts corresponding to that type.
    * `shipmentStatusId`: If the shipment status ID is provided, the service fetches shipment receipts based on that status.
    * `sinceReceivedDate`: If the `sinceReceivedDate` is provided, the service retrieves eligible shipment receipts after that date.

    **Note:** `sinceReceivedDate` aligns with the `datetimeReceived` field in the ShipmentReceipt entity.

    * `productStoreIds`: The service generates the feed based on the following:
      * If only one value is provided in `productStoreIds`, the feed is generated for that specific product store ID, representing a particular brand.
      * If `productStoreIds` is not provided or if there are multiple values, the default prefix 'HOTWAX' is set using the property in the MoquiConf file.

    **Note:** This entity-find fetches shipment-level details for eligible Shipment Receipt Feed since the select field includes only shipment-level fields.
2.  **Fetching Eligible Shipment Items:** The second entity-find retrieves eligible shipment items based on the conditions:

    * `shipmentId`: To fetch details for the order ID existing in the list obtained from the first entity-find.

    **Note:** This entity-find fetches shipment item-level details since the select field includes only shipment item-level fields.
3.  **Fetching Eligible Shipment Receipts:** The third entity-find fetches eligible shipment receipts using conditions:

    * `shipmentId` and `shipmentItemsSeqId`: Included to fetch shipment item receipts for specific shipment IDs and shipment Item Seq IDs.

    Here, for each shipment item, valid Shipment Receipts are fetched. This ensures accurate quantity evaluation (sum of `qtyAccepted`) in the next entity-find using these receipt IDs.

    **Note:** It is crucial to fetch valid Shipment Receipts to prevent resending quantities already included in earlier feeds.
4. **Total Quantity Calculation:** The fourth entity-find calculates the total quantity (`sum(qtyAccepted)`) of eligible shipment receipts. This aggregation ensures an accurate representation of the cumulative accepted quantity in the feed.
