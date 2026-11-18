# Tracker

## Product Requirements Document (PRD)

**Document status:** Final\
**Version:** 1.0\
**Platform:** Responsive web application (desktop and mobile browsers)\
**Currency:** Philippine Peso (PHP)\
**Timezone:** Asia/Manila\
**Primary user:** Single business owner / administrator

> **Illustration note:** Any images added to this document are visual
> references only. They illustrate possible layouts and workflows and
> are not authoritative specifications. Functional requirements, field
> definitions, and business rules in this document take precedence.

------------------------------------------------------------------------

## 1. Product Overview

The Store & Digital Transaction Tracker is a responsive web application
for managing a small retail business that provides e-wallet services,
mobile load, and physical store products.

The application centralizes transaction recording, automatic service-fee
calculation, inventory management, point-of-sale (POS) checkout,
reporting, and business performance monitoring.

### 1.1 Business areas

-   **E-wallet services:** GCash and Maya cash-in / cash-out
    transactions.
-   **Mobile load services:** TNT, Smart, DITO, Globe, and TM.
-   **Store inventory:** School supplies, frozen foods, and rice.
-   **POS:** Sales of physical store products with automatic inventory
    deduction.

### 1.2 Product goals

1.  Record e-wallet and mobile load transactions accurately.
2.  Calculate service fees automatically using configurable fee rules.
3.  Track inventory quantities, cost prices, selling prices, and
    expiration dates.
4.  Process store sales through an integrated POS.
5.  Keep transaction volume, sales revenue, service-fee income, and
    profit financially distinct.
6.  Provide daily and monthly summaries that help the owner understand
    business performance.
7.  Work reliably on desktop, tablet, and mobile browsers.

### 1.3 Out of scope for the initial release

-   Multiple user accounts and employee permissions.
-   Native iOS or Android applications.
-   Direct GCash, Maya, or telecom-provider API integration.
-   Automated fund transfers or automated load purchases.
-   Supplier management and purchase-order workflows.
-   Loyalty, rewards, or customer-membership programs.
-   Full operating-expense management (unless added in a later phase).

The initial release records transactions entered by the owner. It does
not itself transfer money or purchase load from provider systems.

------------------------------------------------------------------------

## 2. Users and Access

### 2.1 Primary user

The system has one owner/admin account.

The owner can: - View the dashboard. - Create and update transactions. -
Configure fee rules. - Manage products and inventory. - Process POS
sales. - View and export reports. - Manage business settings.

### 2.2 Authentication

-   Secure login and logout.
-   Passwords must be stored using a modern password-hashing algorithm.
-   Financial and inventory actions must require an authenticated
    session.
-   The initial version does not require role-based access control.

------------------------------------------------------------------------

## 3. Navigation and Modules

The application contains the following modules:

1.  Dashboard
2.  E-Wallet Management
3.  Mobile Load Management
4.  Store Inventory
5.  POS / Store Sales
6.  Reports
7.  Settings

### Suggested navigation

-   Dashboard
-   E-Wallet
-   Mobile Load
-   Inventory
-   Point of Sale
-   Sales History
-   Reports
-   Settings

------------------------------------------------------------------------

## 4. Dashboard

The dashboard provides a consolidated view of business activity.

### 4.1 Summary cards

Display the following metrics for the selected date range:

  -----------------------------------------------------------------------
  Metric                              Definition
  ----------------------------------- -----------------------------------
  E-Wallet Transaction Volume         Total amount processed through
                                      eligible GCash and Maya
                                      transactions

  E-Wallet Fees Today                 Eligible e-wallet service fees
                                      earned today

  E-Wallet Fees This Month            Eligible e-wallet service fees
                                      earned in the current month

  Mobile Load Sales Volume            Total amount of successful load
                                      transactions

  Mobile Load Fees                    Service-fee income from successful
                                      load transactions

  Store Sales                         Revenue from completed POS sales,
                                      net of discounts and applicable
                                      refunds

  Store Gross Profit                  Store sales revenue minus cost of
                                      goods sold

  Total Gross Earnings                E-wallet fees + load fees + store
                                      gross profit
  -----------------------------------------------------------------------

**Important:** E-wallet principal amounts and mobile load principal
amounts are transaction volume, not business income or profit. They must
not be included in gross earnings.

### 4.2 Charts and widgets

-   Daily sales and service-fee overview.
-   Monthly revenue / gross-earnings trend.
-   E-wallet cash-in versus cash-out.
-   GCash versus Maya transaction comparison.
-   Mobile load performance by network.
-   Best-selling store products.
-   Low-stock alerts.
-   Expiration alerts.
-   Recent transactions.
-   Daily cash-flow overview.

### 4.3 Date filters

-   Today
-   Yesterday
-   This week
-   This month
-   Last month
-   Custom date range

All dashboard cards and charts must use the same selected date range
unless a card is explicitly labeled with a fixed period such as "Today"
or "This Month."

> **Illustration placeholder --- Dashboard:** Insert a dashboard mockup
> or screenshot here. The image is illustrative; the metric definitions
> above are authoritative.

![Illustrative dashboard layout](images/dashboard-illustration.png)

------------------------------------------------------------------------

## 5. E-Wallet Management

### 5.1 Supported providers

-   GCash
-   Maya

### 5.2 Summary cards

-   Total transaction amount today.
-   Total service fees today.
-   Total service fees this month.
-   Total cash-in amount.
-   Total cash-out amount.

### 5.3 Transaction fields

  Field                     Description
  ------------------------- ---------------------------------------------------
  Transaction Date          Date the transaction occurred
  Transaction Time          Time the transaction occurred
  Transaction Type          Cash-in or cash-out
  Provider                  GCash or Maya
  Amount                    Principal amount processed
  Service Fee               Automatically calculated fee
  Customer Payment Method   Cash, GCash, or Maya
  Reference Number          Provider or transaction reference, when available
  Status                    Sent, Claimed, Pending, Failed, or Cancelled
  Notes                     Optional transaction remarks

**Provider and payment method are separate fields.** For example, a
GCash cash-in transaction may be paid by the customer in cash. The
provider is GCash; the customer payment method is Cash.

### 5.4 Transaction workflow

1.  Owner opens E-Wallet.
2.  Selects Cash-in or Cash-out.
3.  Selects GCash or Maya.
4.  Enters the transaction amount.
5.  Selects how the customer paid.
6.  System calculates the fee using the active fee rule.
7.  System displays a transaction preview.
8.  Owner confirms and saves the transaction.
9.  Dashboard and reports update based on the saved status.

### 5.5 Fee configuration

Fee rules must be configurable by: - Provider. - Transaction type. -
Minimum and maximum amount. - Fixed fee. - Percentage fee. - Effective
start date and optional end date. - Active/inactive status.

The fee engine must support: - Fixed fees. - Percentage-based fees. -
Amount brackets / tiered fees. - Minimum and maximum fee limits where
configured. - Authorized manual fee override.

Example calculation:

`Service Fee = Fixed Fee + (Transaction Amount × Percentage Rate)`

The exact fee schedule must be configured by the owner. Example values
used in mockups or tests are illustrative only.

### 5.6 Status and financial treatment

-   **Sent:** Eligible for fee and volume reporting when the transaction
    is considered successfully processed.
-   **Claimed:** Eligible for fee and volume reporting.
-   **Pending:** Excluded from completed transaction totals.
-   **Failed:** Excluded from completed transaction totals.
-   **Cancelled:** Excluded from completed transaction totals.

A status update must modify the original transaction record. It must not
create a second financial transaction or double-count the amount or fee.

------------------------------------------------------------------------

## 6. Mobile Load Management

### 6.1 Supported networks

-   TNT
-   Smart
-   DITO
-   Globe
-   TM

### 6.2 Summary cards

-   Total load amount today.
-   Total load service fees today.
-   Total load service fees this month.
-   Successful transaction count.
-   Failed transaction count.

### 6.3 Transaction fields

  Field              Description
  ------------------ -----------------------------------------------
  Transaction Date   Date of transaction
  Transaction Time   Time of transaction
  Network            TNT, Smart, DITO, Globe, or TM
  Mobile Number      Customer number receiving the load
  Load Amount        Principal load amount
  Service Fee        Automatically calculated service fee / margin
  Status             Successful, Pending, Failed, or Cancelled
  Reference Number   Optional provider reference
  Notes              Optional remarks

### 6.4 Transaction workflow

1.  Owner selects the network.
2.  Enters the customer's mobile number.
3.  Enters the load amount.
4.  System calculates the service fee using the active network fee rule.
5.  Owner reviews the transaction.
6.  Owner confirms and saves it.
7.  The transaction appears in history and eligible dashboard totals.

### 6.5 Fee rules

Fee rules must be configurable per network and support: - Fixed fee. -
Percentage fee. - Amount-based brackets. - Effective dates. -
Active/inactive status. - Manual override with audit history.

Only successful transactions contribute to completed load volume and
load-fee earnings. Pending, failed, and cancelled transactions are
excluded.

------------------------------------------------------------------------

## 7. Store Inventory

### 7.1 Product categories

Initial categories: - School Supplies - Frozen Foods - Rice

The owner can add, edit, or deactivate categories.

### 7.2 Product fields

  -----------------------------------------------------------------------
  Field                               Description
  ----------------------------------- -----------------------------------
  Product Name                        Item display name

  SKU                                 Optional unique product code

  Category                            Product category

  Unit                                Piece, pack, kilo, sack, box, or
                                      configured unit

  Selling Price                       Current POS selling price

  Default Cost Price                  Optional convenience value for
                                      stock receiving

  Current Stock                       Calculated available quantity

  Low-Stock Threshold                 Quantity at which an alert is
                                      raised

  Expiration Tracking                 Whether the product requires
                                      expiration tracking

  Status                              Active or inactive
  -----------------------------------------------------------------------

### 7.3 Inventory batches

Stock received at different times may have different costs or expiration
dates. The system must therefore track stock in batches.

Each batch should contain: - Product. - Date received. - Quantity
received. - Remaining quantity. - Actual unit cost. - Expiration date,
when applicable. - Supplier / source note, optional.

The batch's actual unit cost is authoritative for cost-of-goods-sold
calculations. A product-level default cost price may assist data entry
but must not overwrite historical batch costs.

### 7.4 Stock-in workflow

1.  Select an existing product or create a product.
2.  Enter quantity received.
3.  Enter actual unit cost.
4.  Enter expiration date when applicable.
5.  Confirm stock-in.
6.  System creates an inventory batch and stock movement.
7.  Current stock is recalculated.

### 7.5 Stock-out and adjustments

Stock may decrease through: - Completed POS sales. - Owner-entered stock
adjustments.

Every manual adjustment must include: - Product. - Quantity changed. -
Reason. - Date and time. - Reference or note, optional.

Manual stock adjustments must be recorded as inventory movements. The
system must not silently overwrite the stock quantity.

### 7.6 Stock costing and batch allocation

Use FIFO (First In, First Out) as the default cost-allocation method.
Where expiration dates exist, the system should also support
expiry-aware handling so stock nearing expiration is not overlooked.

When a POS sale consumes stock from multiple batches, the system must
record the quantity and cost allocated from each batch. A sale item may
therefore be associated with multiple inventory batches through a
batch-allocation table.

### 7.7 Inventory calculations

-   `Current Stock = Total Stock In - Total Stock Out + Adjustments`
-   `Unit Gross Margin = Selling Price - Allocated Unit Cost`
-   `Inventory Cost Value = Sum(Remaining Batch Quantity × Batch Unit Cost)`

### 7.8 Inventory alerts

-   Low stock: current stock is at or below the configured threshold.
-   Expiring soon: configurable warning window, such as 7 or 30 days.
-   Expired: expiration date is earlier than the current business date.

Expiration date is optional for products that do not require it.

> **Illustration placeholder --- Inventory:** Insert a product-list,
> stock-batch, or expiration-alert mockup here. The image is
> illustrative only.

![Illustrative inventory layout](images/inventory-illustration.png)

------------------------------------------------------------------------

## 8. Point of Sale (POS)

The POS module handles physical store-product sales and integrates
directly with inventory.

### 8.1 POS screen requirements

-   Product search.
-   Category filters.
-   Product grid or list.
-   Product name, price, and available stock.
-   Cart with quantity controls.
-   Remove item action.
-   Subtotal.
-   Optional discount.
-   Total amount.
-   Payment method.
-   Amount tendered and change for cash payments.
-   Checkout action.
-   Receipt generation.

### 8.2 Supported payment methods

-   Cash
-   GCash
-   Maya

Payment method must be recorded independently from the e-wallet service
provider fields used in the E-Wallet module.

### 8.3 Checkout workflow

1.  Owner searches for or selects products.
2.  Adds products to the cart.
3.  Adjusts quantities.
4.  System validates available stock.
5.  System calculates subtotal, discount, and total.
6.  Owner selects the payment method.
7.  For cash, owner enters the amount tendered and the system calculates
    change.
8.  Owner confirms checkout.
9.  System creates the sale and sale-item records.
10. System allocates sold quantities to inventory batches using FIFO.
11. System records inventory movements and payment.
12. System generates a unique receipt number.
13. Dashboard and reports update.

### 8.4 Sale record fields

-   Receipt number.
-   Sale date and time.
-   Items sold.
-   Quantity per item.
-   Unit selling price snapshot.
-   Unit cost snapshot / batch allocations.
-   Subtotal.
-   Discount.
-   Total.
-   Payment method.
-   Amount tendered.
-   Change.
-   Status: Completed, Voided, or Refunded.

### 8.5 POS business rules

-   Prevent checkout when stock is insufficient.
-   Deduct inventory only after successful checkout.
-   Generate a unique receipt number for every sale.
-   Support multiple products in one sale.
-   Preserve historical selling-price and cost snapshots.
-   Do not change old sale prices when a product's current selling price
    changes.
-   Voiding a sale must reverse its inventory movements and financial
    reporting impact.
-   A refund must record the refunded amount and affected sale items.
-   Return stock only when the goods are physically returned and
    considered resalable.
-   Checkout, payment creation, batch allocation, and stock deduction
    must run within one database transaction.
-   Use an idempotency key or equivalent protection to prevent duplicate
    checkout submissions.

### 8.6 Profit calculation

`Store Gross Profit = Net Store Sales Revenue - Cost of Goods Sold`

Discounts reduce recognized sales revenue. Cost of goods sold must use
the actual batch costs allocated to the sold quantities.

> **Illustration placeholder --- POS:** Insert a POS/cart/receipt mockup
> here. The image is illustrative only.

![Illustrative POS layout](images/pos-illustration.png)

------------------------------------------------------------------------

## 9. Reports

The reports module provides date-filtered business records and
summaries.

### 9.1 Required reports

-   Daily business summary.
-   Monthly business summary.
-   E-wallet transaction report.
-   E-wallet service-fee report.
-   Mobile load transaction report.
-   Mobile load service-fee report.
-   Store sales report.
-   Store gross-profit report.
-   Product sales report.
-   Inventory valuation report.
-   Stock movement report.
-   Low-stock report.
-   Expiration and expired-stock report.

### 9.2 Report features

-   Date-range filtering.
-   Provider / network filtering.
-   Transaction status filtering.
-   Product and category filtering where applicable.
-   Search, sorting, and pagination.
-   Export to CSV, Excel, and PDF.
-   Print-friendly report layouts.

------------------------------------------------------------------------

## 10. Settings

The settings module includes:

### Business settings

-   Business name.
-   Business address.
-   Contact information.
-   Currency (PHP).
-   Timezone (Asia/Manila).

### Fee settings

-   E-wallet fee rules.
-   Mobile load fee rules.
-   Effective dates.
-   Manual fee override permissions for the owner.

### Inventory settings

-   Default low-stock threshold.
-   Expiration warning window.
-   Cost-allocation method (FIFO initially).
-   Product units.
-   Product categories.

### POS settings

-   Receipt format.
-   Receipt numbering.
-   Default payment methods.
-   Discount configuration, if enabled.

### Account and maintenance

-   Change password.
-   Database backup / restore procedures.
-   Audit-log access.

------------------------------------------------------------------------

## 11. Financial Definitions and Business Logic

This section is authoritative for dashboard totals and reports.

### 11.1 Financial terminology

  -----------------------------------------------------------------------
  Term                                Meaning
  ----------------------------------- -----------------------------------
  Transaction Volume                  Principal amount processed through
                                      a service

  Service-Fee Income                  Fee earned for providing e-wallet
                                      or load services

  Store Sales Revenue                 Revenue from physical products sold

  Cost of Goods Sold (COGS)           Actual inventory cost allocated to
                                      sold products

  Store Gross Profit                  Store sales revenue minus COGS

  Total Gross Earnings                E-wallet fees + load fees + store
                                      gross profit

  Net Profit                          Total gross earnings minus
                                      operating expenses

  Cash Flow                           Actual cash received and paid out
  -----------------------------------------------------------------------

### 11.2 Core formulas

**E-wallet** - E-wallet transaction volume = sum of eligible transaction
amounts. - E-wallet fee income = sum of eligible transaction fees.

**Mobile load** - Load transaction volume = sum of successful load
amounts. - Load fee income = sum of successful load fees.

**Store** - Store sales revenue = completed POS sales, net of discounts
and applicable refunds. - COGS = sum of actual batch costs allocated to
sold quantities. - Store gross profit = store sales revenue - COGS.

**Business** - Total gross earnings = e-wallet fee income + load fee
income + store gross profit. - Net profit = total gross earnings -
operating expenses.

Operating-expense tracking is outside the initial MVP unless explicitly
added. If expenses are not recorded, the application must not label
gross earnings as net profit.

### 11.3 Eligibility rules

  -----------------------------------------------------------------------
  Transaction type                    Included in completed totals
  ----------------------------------- -----------------------------------
  E-wallet Sent                       Yes, when successfully processed

  E-wallet Claimed                    Yes

  E-wallet Pending                    No

  E-wallet Failed                     No

  E-wallet Cancelled                  No

  Mobile load Successful              Yes

  Mobile load Pending                 No

  Mobile load Failed                  No

  Mobile load Cancelled               No

  POS Completed                       Yes

  POS Voided                          No; reverse original impact

  POS Refunded                        Reverse the applicable refunded
                                      amount and returned-stock cost
                                      treatment
  -----------------------------------------------------------------------

Status transitions must not double-count a transaction. Reports should
derive totals from the current authoritative transaction state and
associated reversal/refund records.

### 11.4 Fee calculation integrity

-   Fee rules must be evaluated on the backend.
-   Each transaction must preserve the fee amount actually applied.
-   Store the fee-rule reference and/or a calculation snapshot.
-   Updating a fee rule must not recalculate historical transactions.
-   Manual overrides must be recorded in the audit log with the previous
    and new values.
-   Define deterministic behavior for overlapping or missing fee
    brackets.

### 11.5 Rounding and monetary precision

-   Store money using `NUMERIC(12,2)` or an equivalent fixed-precision
    decimal type.
-   Do not use binary floating-point types for persisted financial
    amounts.
-   Define one consistent currency-rounding policy in the backend.
-   Frontend totals are previews only; backend-calculated values are
    authoritative.

------------------------------------------------------------------------

## 12. Database Design

Recommended database: PostgreSQL.

### 12.1 Core tables

  -----------------------------------------------------------------------
  Table                               Purpose
  ----------------------------------- -----------------------------------
  `users`                             Single owner/admin account

  `business_settings`                 Business profile and system
                                      preferences

  `providers`                         GCash, Maya, TNT, Smart, DITO,
                                      Globe, TM

  `fee_rules`                         Effective-dated fixed, percentage,
                                      or tiered fee configurations

  `ewallet_transactions`              E-wallet cash-in and cash-out
                                      records

  `load_transactions`                 Mobile load transaction records

  `payment_methods`                   Cash, GCash, Maya payment-method
                                      definitions

  `product_categories`                Inventory categories

  `products`                          Product master data and current
                                      selling price

  `inventory_batches`                 Received stock, batch cost,
                                      remaining quantity, expiration

  `inventory_movements`               Auditable stock-in, stock-out,
                                      adjustment, and reversal records

  `sales`                             POS sale headers

  `sale_items`                        Product, quantity, and price
                                      snapshots for each sale line

  `sale_item_batch_allocations`       Links sale items to one or more
                                      consumed inventory batches

  `payments`                          Payment records associated with
                                      sales

  `refunds`                           Refund headers and amounts

  `refund_items`                      Refunded quantities and affected
                                      sale items

  `audit_logs`                        Important financial, inventory, and
                                      configuration changes

  `expenses`                          Optional future module for
                                      operating expenses
  -----------------------------------------------------------------------

### 12.2 Key relationships

-   A provider has many fee rules.
-   A provider has many e-wallet or load transactions, depending on
    provider type.
-   A product belongs to a category.
-   A product has many inventory batches.
-   A product has many inventory movements.
-   A sale has many sale items.
-   A sale item may consume stock from multiple inventory batches
    through `sale_item_batch_allocations`.
-   A sale has one or more payment records if split payments are
    supported; otherwise enforce one payment per sale in the MVP.
-   A refund belongs to a sale and may contain multiple refund items.
-   An audit log records the user and affected entity.

### 12.3 Important schema rules

-   Use foreign keys for provider, payment method, category, product,
    sale, and batch relationships.
-   Keep e-wallet provider and customer payment method as separate
    fields / relationships.
-   Store monetary values as fixed-precision decimals.
-   Preserve historical transaction fees and applied fee-rule snapshots.
-   Preserve sale-time product price and cost information.
-   Use batch allocations to support FIFO costing across multiple
    batches.
-   Record stock changes as inventory movements.
-   Do not hard-delete completed financial transactions.
-   Use void, cancellation, reversal, and refund records with audit
    history.
-   Use database transactions for checkout and all related stock/payment
    writes.
-   Add indexes for transaction date, status, provider, network,
    product, receipt number, and foreign keys.

------------------------------------------------------------------------

## 13. API Scope

Suggested REST API endpoints:

### Authentication

-   `POST /api/auth/login`
-   `POST /api/auth/logout`
-   `GET /api/auth/me`

### Dashboard

-   `GET /api/dashboard/summary`
-   `GET /api/dashboard/analytics`

### E-wallet

-   `GET /api/ewallet/transactions`
-   `POST /api/ewallet/transactions`
-   `PATCH /api/ewallet/transactions/:id`
-   `POST /api/ewallet/fee-preview`

### Mobile load

-   `GET /api/load/transactions`
-   `POST /api/load/transactions`
-   `PATCH /api/load/transactions/:id`
-   `POST /api/load/fee-preview`

### Fee configuration

-   `GET /api/settings/fees`
-   `POST /api/settings/fees`
-   `PATCH /api/settings/fees/:id`

### Inventory

-   `GET /api/products`
-   `POST /api/products`
-   `PATCH /api/products/:id`
-   `POST /api/inventory/stock-in`
-   `POST /api/inventory/adjustments`
-   `GET /api/inventory/movements`
-   `GET /api/inventory/alerts`

### POS and sales

-   `POST /api/sales/checkout`
-   `GET /api/sales`
-   `GET /api/sales/:id`
-   `POST /api/sales/:id/void`
-   `POST /api/sales/:id/refunds`

### Reports

-   `GET /api/reports/daily`
-   `GET /api/reports/monthly`
-   `GET /api/reports/ewallet`
-   `GET /api/reports/load`
-   `GET /api/reports/sales`
-   `GET /api/reports/inventory`

All list endpoints should support pagination, sorting, and relevant
filters. The backend must validate all inputs and calculate
authoritative financial values.

------------------------------------------------------------------------

## 14. Recommended Technical Architecture

The following is a suggested implementation stack and may be adjusted to
the existing project architecture.

### Frontend

-   React
-   TypeScript
-   Tailwind CSS
-   Mantine or shadcn/ui
-   Zustand for client-side state where needed
-   TanStack Query for server state and caching
-   Recharts for dashboard charts
-   Zod for client-side schemas and form validation

### Backend

-   PHP or Node.js (NestJS / Express), selected according to the
    existing project and deployment environment.
-   REST API with modular domain services.
-   Server-side validation and authorization.
-   Centralized fee-calculation service.
-   Transactional POS / inventory service.

### Database

-   PostgreSQL
-   Prisma if using a compatible Node.js backend, or an appropriate PHP
    ORM / query layer if using PHP.

### Suggested backend modules

-   Authentication
-   Dashboard analytics
-   E-wallet transactions
-   Mobile load transactions
-   Fee engine
-   Inventory and batch costing
-   POS and sales
-   Refunds and voids
-   Reports and exports
-   Business settings
-   Audit logging

------------------------------------------------------------------------

## 15. User Interface and Visual Direction

### 15.1 Design direction

Use a clean, technical, mobile-first interface with a baby-blue theme.

Suggested palette:

  Token        Color
  ------------ -----------
  Primary      `#60A5FA`
  Secondary    `#BFDBFE`
  Background   `#F8FAFC`
  Surface      `#FFFFFF`
  Main text    `#0F172A`
  Border       `#E2E8F0`

Use Inter or Geist typography, clear data hierarchy, readable tables,
restrained shadows, and consistent spacing.

### 15.2 Desktop layout

-   Sidebar navigation.
-   Top header with page title and date controls.
-   Summary cards.
-   Main content area for charts, tables, and forms.
-   Contextual actions for adding transactions or products.

### 15.3 Mobile layout

-   Responsive navigation, such as a collapsible menu or bottom
    navigation.
-   Touch-friendly buttons and form controls.
-   Summary cards that stack or scroll horizontally.
-   Tables that adapt into readable card rows or horizontally scroll
    when necessary.
-   POS optimized for small screens.
-   Forms that fit the viewport without requiring excessive zooming.

### 15.4 Illustration guidance

Images and mockups in the PRD are examples of visual direction only.
They must not be treated as exact UI requirements. The implementation
team may refine spacing, component arrangement, and responsive behavior
while preserving the required data, workflows, and business rules.

------------------------------------------------------------------------

## 16. Non-Functional Requirements

### Performance

-   Dashboard should load within approximately 3 seconds under normal
    operating conditions.
-   Use pagination for large transaction and inventory lists.
-   Use indexed database queries and avoid unnecessary full-table scans.

### Security

-   HTTPS in production.
-   Secure password hashing.
-   Server-side input validation.
-   Parameterized queries / ORM protections against SQL injection.
-   Secure session handling.
-   Authorization checks on all protected endpoints.
-   Do not expose sensitive configuration or credentials in frontend
    code.

### Data integrity

-   Use database transactions for POS checkout, refunds, and stock
    changes.
-   Prevent duplicate checkout submissions.
-   Preserve financial and inventory audit history.
-   Keep fee calculations consistent between preview and final save.
-   Use migrations and validated schema changes.

### Reliability and maintenance

-   Scheduled database backups.
-   Documented restore procedure.
-   Application and error logging.
-   Audit logs for important changes.
-   Consistent timezone handling using Asia/Manila.
-   Automated tests for financial calculations and inventory workflows.

### Accessibility and usability

-   Clear labels and validation messages.
-   Keyboard-accessible forms and navigation.
-   Sufficient contrast.
-   Responsive layouts for desktop and mobile browsers.

------------------------------------------------------------------------

## 17. Development Scope and Milestones

### Phase 1 --- Foundation

-   Initialize frontend and backend.
-   Configure database and migrations.
-   Implement owner authentication.
-   Implement responsive application shell.
-   Implement business settings and shared UI components.

**Deliverable:** Authenticated application foundation.

### Phase 2 --- E-wallet and Mobile Load

-   Configure providers.
-   Implement transaction creation and history.
-   Implement automatic fee engine.
-   Implement fee-rule configuration.
-   Implement status handling and filters.
-   Add transaction validation and audit logging.

**Deliverable:** Working e-wallet and load modules.

### Phase 3 --- Inventory

-   Implement categories and product management.
-   Implement stock receiving and batch tracking.
-   Implement cost and selling-price handling.
-   Implement FIFO batch allocation support.
-   Implement inventory movements.
-   Implement low-stock and expiration alerts.

**Deliverable:** Working inventory module with auditable stock history.

### Phase 4 --- POS

-   Implement product search and cart.
-   Implement checkout and payment recording.
-   Implement batch-based stock deduction.
-   Implement receipt generation.
-   Implement sales history, voids, and refunds.

**Deliverable:** POS integrated with inventory and sales records.

### Phase 5 --- Dashboard and Reports

-   Implement dashboard summary calculations.
-   Implement charts and date filters.
-   Implement module-specific reports.
-   Implement CSV, Excel, and PDF exports.

**Deliverable:** Business dashboard and reporting suite.

### Phase 6 --- Testing and Deployment

-   Test fee calculations and status transitions.
-   Test POS stock deduction and rollback.
-   Test FIFO allocation and refunds.
-   Test dashboard/report reconciliation.
-   Test mobile and desktop responsiveness.
-   Perform security checks.
-   Configure backups and production deployment.

**Deliverable:** Production-ready initial release.

------------------------------------------------------------------------

## 18. Acceptance Criteria

The initial release is accepted when:

1.  The owner can securely log in and access all modules.
2.  E-wallet transactions can be recorded for GCash and Maya.
3.  Mobile load transactions can be recorded for all five supported
    networks.
4.  Fee rules calculate fees automatically and preserve historical
    applied values.
5.  Pending, failed, and cancelled transactions are excluded from
    completed totals.
6.  Inventory supports categories, cost price, selling price, batches,
    and optional expiration dates.
7.  Stock movements are recorded and current stock reconciles with
    movement history.
8.  POS supports multi-item checkout and the three supported payment
    methods.
9.  Successful POS checkout deducts inventory exactly once.
10. Insufficient stock prevents checkout.
11. Voids and refunds correctly reverse applicable financial and
    inventory effects.
12. FIFO batch allocations produce correct COGS.
13. Dashboard totals distinguish transaction volume, fee income, store
    sales, and gross profit.
14. Reports support date filters and required exports.
15. The application is usable on desktop and mobile browsers.
16. Financial records are not silently deleted or recalculated when
    settings change.

------------------------------------------------------------------------

## 19. Key Risks and Implementation Notes

  -----------------------------------------------------------------------
  Risk                                Mitigation
  ----------------------------------- -----------------------------------
  Fee rules change over time          Effective-dated rules and
                                      transaction-level fee snapshots

  Principal amounts are mistaken for  Separate volume, fee income, sales
  profit                              revenue, and profit metrics

  Duplicate POS checkout              Idempotency key and database
                                      transaction

  Inventory quantities drift          Movement ledger and batch-level
                                      reconciliation

  Different purchase costs            Batch costing and FIFO allocation

  Partial refunds                     Refund-item records linked to
                                      original sale items

  Expired products are sold           Expiration alerts and
                                      stock-selection controls

  Provider API assumptions            Clearly define initial release as
                                      manual transaction recording
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 20. Final Product Definition

The initial product is a single-owner, responsive web application for
tracking GCash and Maya services, mobile load transactions, retail
inventory, and physical store sales through an integrated POS.

Its core requirements are automatic configurable service-fee
calculation, batch-based inventory costing, reliable POS stock
deduction, accurate financial reporting, and a baby-blue responsive
interface.

The system must preserve a clear distinction between transaction volume
and actual business earnings. E-wallet and mobile load principal amounts
are not profit; only service fees and physical-store gross profit
contribute to total gross earnings.
