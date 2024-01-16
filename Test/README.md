# Approve Order

### **NetsuiteItemLineId Attribute:**&#x20;

The NetsuiteItemLineId is generated and associated with OMS order items during a specific synchronization step after the sales order has been created in Netsuite. This synchronization step is crucial for mapping and aligning the order line items in OMS with their corresponding line item IDs in Netsuite. Verification of the presence of the NetsuiteItemLineId order item attribute is necessary. If all items of an order possess the NetsuiteItemLineId, the NETSUITE\_ORDER\_EXPORTED order attribute will be created.

## **Implementation Flow:**

The approval process for eligible orders will be implemented by NiFi. This workflow is divided into creating order attributes in the OMS database and then approving the eligible orders.&#x20;



For creating order attributes, an SQL with required checks is executed and a CSV file is kept for the OMS job to read, which creates the order attribute. The name of the job is createUpdateOrderAttribute. The file is read from the directory -

```
hotwax/ApproveOrderAttributes 
```

For approving orders, a CSV file containing eligible order IDs is stored on SFTP. This file is generated based on the presence of required order attributes. The OMS job consumes this file to approve orders. The file is read from the directory -

```
hotwax/ApproveOrders
```

### NiFi Flow -

The NiFi setup employs the same set of processors for both flows – one for creating order attributes and the other for approving orders. The sequence for these processors is as follows:

* The **ExecuteSQLRecord** processor is used to execute distinct SQL queries, generating CSV files based on the defined Avro schema for creating order attributes.
* The subsequent processor, **RouteOnAttribute**, checks whether the flow file contains any records.
* The filename is then updated to the required format using the **UpdateAttribute** processor.
* The final step involves transferring the file to the SFTP location using the **PutSFTP** processor.
* The stored files will be accessed via HC to create order attributes.
