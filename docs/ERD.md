# Entity relationship diagram

![Sales and inventory ER diagram](ERD-new.png)

This diagram follows the foreign keys in [workDB.sql](../workDB.sql). Crow's foot symbols show how many child rows a parent row can have. The column names preserve the spelling used by the SQL script.

```mermaid
erDiagram
    Companies ||--o{ Branches : owns
    Companies ||--o{ Customers : serves
    Companies ||--o{ SuppLiers : works_with
    Companies ||--o{ Items : catalogs
    Branches ||--o{ Warehouses : contains
    Warehouses ||--o{ InventoryTransactions : records
    Warehouses ||--o{ PurchaseOrders : receives
    Warehouses ||--o{ SalesOrders : fulfills
    Customers ||--o{ SalesOrders : places
    SuppLiers ||--o{ PurchaseOrders : supplies
    Items ||--o{ InventoryTransactions : moves
    Items ||--o{ PurchaseOrderDetails : purchased_as
    Items ||--o{ SalesOrderDetails : sold_as
    PurchaseOrders ||--o{ PurchaseOrderDetails : contains
    SalesOrders ||--o{ SalesOrderDetails : contains

    Companies {
        int CompanieId PK
        varchar CompanieName
        varchar City
    }
    Branches {
        int BrancheId PK
        int CompanyId FK
        varchar BrancheName
        varchar City
    }
    Warehouses {
        int WarehouseId PK
        int BrancheID FK
        varchar WarehouseName
    }
    Customers {
        int CustomerId PK
        int CompanyID FK
        varchar CustomersName
    }
    SuppLiers {
        int SuppLierId PK
        int CompanyID FK
        varchar SuppLierName
    }
    Items {
        int ItemId PK
        int CompanyID FK
        varchar ItemName
        decimal PurchasePrice
        decimal SalePrice
    }
    InventoryTransactions {
        int TransactionID PK
        int ItemID FK
        int WarehouseID FK
        varchar TransactionType
        int Quantity
    }
    PurchaseOrders {
        int PurchaseOrderID PK
        int SupplierID FK
        int WarehouseID FK
        decimal TotalAmount
    }
    PurchaseOrderDetails {
        int PurchaseOrderDetailID PK
        int PurchaseOrderID FK
        int ItemID FK
        int Quantity
    }
    SalesOrders {
        int SalesOrderID PK
        int CustomerID FK
        int WarehouseID FK
        decimal TotalAmount
    }
    SalesOrderDetails {
        int SalesOrderDetailID PK
        int SalesOrderID FK
        int ItemID FK
        int Quantity
    }
```

The diagram is a concise schema overview. Optional contact fields, dates, checks, views, stored procedures, and triggers remain documented in the SQL script.
