# EnterBridge Procurement Case Study

## Overview

This application was developed as a solution for the EnterBridge Procurement Case Study.

The application integrates with the EnterBridge Product and Pricing API to provide a lightweight procurement management experience for a building supplies company. Users can browse products, review pricing trends, create orders, and reorder previously submitted purchases.

The solution was intentionally scoped to provide a functional end-to-end workflow within the suggested time constraints while leaving room for future enhancements.

---

## Technology Stack

* ASP.NET MVC 4
* .NET Framework
* SQL Server LocalDB
* Entity Framework
* Bootstrap
* Chart.js
* Newtonsoft.Json

---

## Features Implemented

### Product Catalog

* Retrieves products from the EnterBridge REST API
* Supports paginated product browsing
* Displays product information including:

  * Name
  * Category
  * Description
  * SKU

### Price History & Trends

* Retrieves historical pricing data from the API
* Displays pricing history in a tabular format
* Displays pricing trends using Chart.js
* Shows:

  * Current Price
  * Starting Price
  * Percentage Change

### Order Management

* Create orders using products from the catalog
* Capture and store the current product price at the time of order creation
* Store orders locally in SQL Server
* Track the user who submitted the order
* Maintain order status

### Reorder Functionality

* Recreate a previous order with a single click
* Supports frequently purchased products and repeat ordering workflows

---

## Database

The application stores orders locally and does not persist product or pricing data from the API.

### Tables

#### Orders

* OrderId
* SubmittedBy
* OrderDate
* Status

#### OrderItems

* OrderItemId
* OrderId
* ProductId
* ProductName
* UnitPrice
* Quantity

A foreign key relationship exists between Orders and OrderItems.

---

## Running Locally

### Prerequisites

* Visual Studio 2017 or later
* SQL Server LocalDB (or SQL Server Express)
* .NET Framework installed

### Database Setup

1. Create a local SQL Server database.
2. Execute the provided database creation scripts located in the repository.
3. Update the connection string in:

```
Web.config
```

to point to your local SQL Server instance.

### Restore Packages

Open the solution in Visual Studio and restore NuGet packages if prompted.

Packages used include:

* EntityFramework
* Newtonsoft.Json

### Run the Application

1. Open the solution in Visual Studio.
2. Build the solution.
3. Press F5.

The application will launch locally using IIS Express.

Example:

```
http://localhost:xxxx/
```

---

## Key Design Decisions

### Product Data Source

Products and pricing information are retrieved directly from the EnterBridge API rather than being stored locally.

This keeps the application aligned with the requirement that product and pricing information is centrally managed through the external API.

### Price Snapshotting

Order items store the price at the time the order is created.

This ensures historical orders remain accurate even when product pricing changes in the future.

### Lightweight Procurement Workflow

To address the foreman review requirement, orders include a status field that can support:

* Pending
* Approved
* Rejected

This establishes a foundation for an approval workflow without introducing unnecessary complexity.

### Reorder Capability

The requirement that users frequently purchase the same products was interpreted as a need for repeat ordering.

A Reorder feature was implemented to allow users to quickly recreate previously submitted orders.

---

## Scope Decisions

### Implemented

* Product browsing
* Price history visualization
* Order creation
* Local order storage
* Reorder functionality

### Intentionally Not Implemented

* Authentication / authorization
* Role-based permissions
* Notifications
* Email workflows
* Product caching
* Automated tests
* Deployment pipeline
* User tracking by name or loging

These items were intentionally deferred to maximize delivery of core business functionality within the recommended time allocation.

---

## Future Enhancements

Given additional time, I would consider:

* Product and pricing synchronization/caching
* Approval workflow UI for foreman review
* Order editing after submission
* Search and filtering improvements
* Product favorites
* Notifications and email alerts
* Automated tests
* API resiliency and retry handling
* Role-based security

---

## Assumptions

* Users are identified by name only.
* Product and pricing data remain authoritative in the external API.
* Orders are owned and stored by the local application.
* Pricing displayed during order creation represents the latest available price returned by the API.
