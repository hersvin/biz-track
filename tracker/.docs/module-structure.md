# Source Module Architecture

## Project Structure

This document defines the recommended feature-based structure for the
Store & Digital Transaction Tracker. All business features live under
`src/modules/`.

Each module follows the same convention:

-   `assets/` --- module-specific images, icons, and static assets.
-   `components/` --- reusable UI components owned by the module.
-   `services/` --- API calls and module-specific service functions.
-   `<module>.context.tsx` --- optional React Context for module-level
    dependency or shared state.
-   `<module>.store.ts` --- Zustand store for client-side state.
-   `<module>.tsx` --- main module page / entry component.

``` text
src/
├── modules/
│   ├── dashboard/
│   │   ├── assets/
│   │   ├── components/
│   │   │   ├── SummaryCards/
│   │   │   ├── RevenueChart/
│   │   │   ├── TransactionOverview/
│   │   │   ├── RecentTransactions/
│   │   │   ├── LowStockAlerts/
│   │   │   └── ExpirationAlerts/
│   │   ├── services/
│   │   │   └── dashboard.service.ts
│   │   ├── dashboard.context.tsx
│   │   ├── dashboard.store.ts
│   │   └── dashboard.tsx
│   │
│   ├── ewallet/
│   │   ├── assets/
│   │   ├── components/
│   │   │   ├── EwalletSummary/
│   │   │   ├── EwalletTable/
│   │   │   ├── EwalletForm/
│   │   │   ├── EwalletFilters/
│   │   │   ├── EwalletDetails/
│   │   │   └── FeePreview/
│   │   ├── services/
│   │   │   └── ewallet.service.ts
│   │   ├── ewallet.context.tsx
│   │   ├── ewallet.store.ts
│   │   └── ewallet.tsx
│   │
│   ├── mobile-load/
│   │   ├── assets/
│   │   ├── components/
│   │   │   ├── LoadSummary/
│   │   │   ├── LoadTransactionTable/
│   │   │   ├── LoadTransactionForm/
│   │   │   ├── LoadFilters/
│   │   │   ├── NetworkSelector/
│   │   │   └── FeePreview/
│   │   ├── services/
│   │   │   └── mobile-load.service.ts
│   │   ├── mobile-load.context.tsx
│   │   ├── mobile-load.store.ts
│   │   └── mobile-load.tsx
│   │
│   ├── inventory/
│   │   ├── assets/
│   │   ├── components/
│   │   │   ├── InventorySummary/
│   │   │   ├── ProductTable/
│   │   │   ├── ProductForm/
│   │   │   ├── ProductDetails/
│   │   │   ├── CategoryManager/
│   │   │   ├── StockInForm/
│   │   │   ├── StockAdjustmentForm/
│   │   │   ├── InventoryBatchTable/
│   │   │   ├── StockMovementTable/
│   │   │   ├── LowStockList/
│   │   │   └── ExpirationList/
│   │   ├── services/
│   │   │   └── inventory.service.ts
│   │   ├── inventory.context.tsx
│   │   ├── inventory.store.ts
│   │   └── inventory.tsx
│   │
│   ├── pos/
│   │   ├── assets/
│   │   ├── components/
│   │   │   ├── ProductCatalog/
│   │   │   ├── ProductSearch/
│   │   │   ├── CategoryFilter/
│   │   │   ├── ShoppingCart/
│   │   │   ├── CartItem/
│   │   │   ├── CheckoutPanel/
│   │   │   ├── PaymentSelector/
│   │   │   ├── CashPaymentForm/
│   │   │   ├── Receipt/
│   │   │   └── CheckoutConfirmation/
│   │   ├── services/
│   │   │   └── pos.service.ts
│   │   ├── pos.context.tsx
│   │   ├── pos.store.ts
│   │   └── pos.tsx
│   │
│   ├── sales/
│   │   ├── assets/
│   │   ├── components/
│   │   │   ├── SalesSummary/
│   │   │   ├── SalesTable/
│   │   │   ├── SaleDetails/
│   │   │   ├── ReceiptViewer/
│   │   │   ├── VoidSaleDialog/
│   │   │   ├── RefundForm/
│   │   │   └── SalesFilters/
│   │   ├── services/
│   │   │   └── sales.service.ts
│   │   ├── sales.context.tsx
│   │   ├── sales.store.ts
│   │   └── sales.tsx
│   │
│   ├── reports/
│   │   ├── assets/
│   │   ├── components/
│   │   │   ├── ReportFilters/
│   │   │   ├── BusinessSummaryReport/
│   │   │   ├── EwalletReport/
│   │   │   ├── MobileLoadReport/
│   │   │   ├── SalesReport/
│   │   │   ├── ProfitReport/
│   │   │   ├── InventoryReport/
│   │   │   └── ExportActions/
│   │   ├── services/
│   │   │   └── reports.service.ts
│   │   ├── reports.context.tsx
│   │   ├── reports.store.ts
│   │   └── reports.tsx
│   │
│   └── settings/
│       ├── assets/
│       ├── components/
│       │   ├── BusinessProfileForm/
│       │   ├── FeeRuleManager/
│       │   ├── FeeRuleForm/
│       │   ├── InventorySettings/
│       │   ├── PosSettings/
│       │   ├── AccountSettings/
│       │   └── BackupSettings/
│       ├── services/
│       │   └── settings.service.ts
│       ├── settings.context.tsx
│       ├── settings.store.ts
│       └── settings.tsx
│
├── components/
│   ├── ui/
│   ├── layout/
│   ├── data-display/
│   └── feedback/
│
├── hooks/
├── lib/
├── services/
│   ├── api-client.ts
│   └── query-client.ts
├── routes/
├── types/
├── utils/
├── App.tsx
└── main.tsx
```

## Module Responsibilities

  -----------------------------------------------------------------------
  Module                              Responsibility
  ----------------------------------- -----------------------------------
  `dashboard`                         Business overview, summary metrics,
                                      charts, alerts, and recent activity

  `ewallet`                           GCash and Maya cash-in / cash-out
                                      transaction management

  `mobile-load`                       TNT, Smart, DITO, Globe, and TM
                                      load transaction management

  `inventory`                         Products, categories, stock
                                      receiving, batches, stock
                                      adjustments, and expiration
                                      tracking

  `pos`                               Product selection, cart management,
                                      checkout, payment capture, and
                                      receipt generation

  `sales`                             Sales history, sale details, voids,
                                      refunds, and receipt reprints

  `reports`                           Date-filtered financial,
                                      transaction, sales, and inventory
                                      reports

  `settings`                          Business profile, fee rules,
                                      inventory preferences, POS
                                      preferences, and account settings
  -----------------------------------------------------------------------

## Shared Source Directories

These directories contain code shared by multiple modules. Keep
feature-specific code inside its owning module.

  -----------------------------------------------------------------------
  Directory                           Responsibility
  ----------------------------------- -----------------------------------
  `components/ui/`                    Generic buttons, inputs, dialogs,
                                      dropdowns, and other design-system
                                      primitives

  `components/layout/`                Application shell, sidebar, header,
                                      navigation, and page containers

  `components/data-display/`          Shared tables, metric cards, empty
                                      states, and chart wrappers

  `components/feedback/`              Toasts, alerts, loading indicators,
                                      and error states

  `hooks/`                            Shared React hooks

  `lib/`                              Library configuration and setup

  `services/`                         Shared API client and query-client
                                      configuration

  `routes/`                           Route definitions and route guards

  `types/`                            Shared application-level TypeScript
                                      types

  `utils/`                            Shared formatting, date, currency,
                                      and validation utilities
  -----------------------------------------------------------------------

## Module File Responsibilities

Example: `src/modules/ewallet/`

``` text
ewallet/
├── assets/
├── components/
│   ├── EwalletForm/
│   │   ├── EwalletForm.tsx
│   │   ├── ewallet-form.schema.ts
│   │   └── index.ts
│   └── EwalletTable/
│       ├── EwalletTable.tsx
│       └── index.ts
├── services/
│   └── ewallet.service.ts
├── ewallet.context.tsx
├── ewallet.store.ts
└── ewallet.tsx
```

-   `ewallet.tsx`: Composes the module page from its components.
-   `ewallet.store.ts`: Holds client-side UI state, such as selected
    filters, active dialogs, or temporary form state.
-   `ewallet.context.tsx`: Optional provider for module-scoped
    dependencies or state that genuinely needs React Context.
-   `services/ewallet.service.ts`: Contains typed API functions. Use
    TanStack Query hooks to call these functions and manage server
    state.
-   `components/`: Contains UI components used by this module.

## Architecture Guidelines

1.  **Keep modules independent.** A module should own its components,
    service functions, types, and state.
2.  **Avoid unnecessary Context and Zustand duplication.** Use TanStack
    Query for server state, Zustand for client-side shared UI state, and
    React Context only when a provider is useful.
3.  **Keep shared components generic.** Move a component to
    `src/components/` only when it is genuinely reusable across multiple
    modules.
4.  **Keep business logic out of page components.** Put API access in
    services and reusable calculations or domain logic in appropriate
    module-level utilities.
5.  **Use a shared API client.** Module services should use the
    configured client from `src/services/api-client.ts`.
6.  **Use consistent naming.** Use kebab-case for module directories and
    PascalCase for React component directories and files.
7.  **Do not duplicate financial calculations in the frontend.** The
    backend is authoritative for fees, totals, COGS, refunds, and
    profit.
8.  **Protect transaction integrity.** POS checkout, inventory
    deduction, and payment recording must be committed atomically by the
    backend.
9.  **Use barrel exports selectively.** Add `index.ts` files where they
    improve imports, but avoid broad exports that create circular
    dependencies.
10. **Add tests alongside the feature.** For larger modules, add
    `__tests__/` or colocated test files for critical workflows.

## Implementation Notes

-   The `sales` module is separate from `pos`: POS is responsible for
    creating a sale, while Sales manages completed-sale history and
    after-sale actions.
-   Fee-rule configuration belongs in `settings`; fee previews and
    transaction-specific fee display belong in `ewallet` and
    `mobile-load`.
-   Inventory is the source of truth for product stock and batch costs.
    POS must request checkout from the backend rather than directly
    mutating stock in the frontend.
-   Dashboard values should come from dashboard/reporting APIs, not be
    independently recomputed from whichever records happen to be loaded
    in the browser.
-   Context and store files are included as optional conventions. Do not
    create empty files just to satisfy the tree; add them when the
    module needs them.
