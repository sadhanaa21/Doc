# Behaviour

The service generates the Transfer Order Receipts Feed based on the following scenarios:

1. **All Items Received:**
   * If a shipment has multiple items, and all are received before the next feed generation, the feed file will include the shipment and all its item shipment receipt details.
2. **Partial Item Receipt:**
   * If a shipment has 3 items, for example, and only 1 is received before the next feed generation, the feed file will still contain the order and all its items. The 1 received item will have its shipment receipt details, while the other 2 items will contain empty shipment details.
3. **History Records:**
   * History records are created in the ShipmentItemHistory entity for shipment receipts, and these records are already included in the feed.
4. **Multiple Receipts for an Item:**
   * If a shipment item has multiple receipts, the feed will create records for all receipts. In the feed, the `totalReceivedQuantity` in the `shipmentItems` list will reflect the overall quantity, while individual receipt details will be included in `shipmentReceipts` inside the `shipmentItems` list.
