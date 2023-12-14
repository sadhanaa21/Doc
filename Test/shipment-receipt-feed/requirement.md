---
description: Prepare Shipments Receipt Feed from OMS -
---

# Requirement

The generated feed is in JSON format. The OMS JSON is organized shipment-wise, containing information about each shipment's items and receipt details. This feed is used to obtain shipment receipt details.

To generate the feed in Moqui, a service job is configured. It runs on a schedule, creates the feed, and stores it on the SFTP.

The following parameters are configured for the service job:

NOTE: The values of parameters used to fetch and generate the feed for eligible purchase order shipment receipts are included.







<details>

<summary>The following parameters are configured for the service job:</summary>



```markdown
 <table>
  <tr>
  <th>

  <div>Parameter Name</div></th>
  <th>

  <div>Description</div></th>
  <th>

  <div>Example Value</div></th>
  </tr>
  <tr>
  <td>shipmentId</td>
  <td>

  <div>To generate the Shipment Receipt Feed for a specific order ID</div></td>
  <td>

  <div>

  </div></td>
  </tr>
  <tr>
  <td>

  <div>productStoreIds</div></td>
  <td>

  <div>To generate the Shipment Receipt Feed for a specific brand or multiple brands</div></td>
  <td>

  <div>

  </div></td>
  </tr>
  <tr>
  <td>

  <div>shipmentTypeId</div></td>
  <td>

  <div>To fetch Shipment Receipt details for a specific shipment type ID</div></td>
  <td>

  <div>

  IN_TRANSFER,

  PURCHASE_SHIPMENT

  </div></td>
  </tr>
  <tr>
  <td>

  <div>shipmentStatusId</div></td>
  <td>

  <div>To fetch Shipment Receipt details for a specific shipment status ID</div></td>
  <td>

  <div>

  PURCH_SHIP_RECEIVED,

  <span dir="">PURCH_SHIP_CREATED</span>

  </div></td>
  </tr>
  <tr>
  <td>

  <div>sinceReceivedDate</div></td>
  <td>

  <div>To fetch the Shipment Receipt details received after a specific date</div></td>
  <td>

  <div>

  </div></td>
  </tr>
  <tr>
  <td>

  <div>

  <span dir="">systemMessageTypeId</span>

  </div></td>
  <td>

  <div>

  The System Message Type ID for generating the Shipment Receipt Feed

  \
  **NOTE:** This is the required parameter to generate the feed.

  </div></td>
  <td>

  TransferOrdersReceiptFeed

  **NOTE:**
  1. As of now, the service job has been scheduled to fetch the eligible Transfer Order Receipts to send to NetSuite.
  2. Here is the example value of systemMessageType is taken from the service job of Transfer Order Receipt Feed
  </td>
  </tr>
  <tr>
  <td>

  <span dir="">systemMessageRemoteId</span>
  </td>
  <td>

  <div>

  <span dir="">The System Message Remote ID for generating the</span>

  Shipment Receipt Feed

  \
  **NOTE:** This is the required parameter to generate the feed.

  </div></td>
  <td>

  <div>

  </div>
  <div>RemoteSFTP</div></td>
  </tr>
  </table>
```

</details>



| **Description**                                                                                                                                                          | **Example Value**                                                                                                                                                                                                                                                                                                   | **Parameter Name**    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| To generate the Shipment Receipt Feed for a specific order ID                                                                                                            |                                                                                                                                                                                                                                                                                                                     | shipmentId            |
| To generate the Shipment Receipt Feed for a specific brand or multiple brands                                                                                            |                                                                                                                                                                                                                                                                                                                     | productStoreIds       |
| To fetch Shipment Receipt details for a specific shipment type ID                                                                                                        | <p>IN_TRANSFER,</p><p>PURCHASE_SHIPMENT</p>                                                                                                                                                                                                                                                                         | shipmentTypeId        |
| To fetch Shipment Receipt details for a specific shipment status ID                                                                                                      | <p>PURCH_SHIP_RECEIVED,</p><p>PURCH_SHIP_CREATED</p>                                                                                                                                                                                                                                                                | shipmentStatusId      |
| To fetch the Shipment Receipt details received after a specific date                                                                                                     |                                                                                                                                                                                                                                                                                                                     | sinceReceivedDate     |
| <p>The System Message Type ID for generating the Shipment Receipt Feed</p><p><br><strong>NOTE:</strong> This is the required parameter to generate the feed.</p>         | <p>TransferOrdersReceiptFeed</p><p><strong>NOTE:</strong></p><ol><li>As of now, the service job has been scheduled to fetch the eligible Transfer Order Receipts to send to NetSuite.</li><li>Here is the example value of systemMessageType is taken from the service job of Transfer Order Receipt Feed</li></ol> | systemMessageTypeId   |
| <p>The System Message Remote ID for generating the</p><p>Shipment Receipt Feed</p><p><br><strong>NOTE:</strong> This is the required parameter to generate the feed.</p> | RemoteSFTP                                                                                                                                                                                                                                                                                                          | systemMessageRemoteId |
