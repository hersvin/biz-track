# Web Application Project Structure

## Overview

This document describes the frontend project structure for the Store &
Digital Transaction Tracker web application, built with React,
TypeScript, and Vite.

Feature-specific code lives under `src/modules/`. Shared hooks, layouts,
and application-level files remain in their respective shared
directories.
`   
## Project Structure

``` text
web/
├── public/
│   ├── favicon.svg
│   └── icons.svg
├── src/
│   ├── assets/
│   │   ├── hero.png
│   │   ├── react.svg
│   │   └── vite.svg
│   ├── hooks/
│   ├── layout/
│   ├── modules/
│   │   ├── dashboard/
│   │   │   ├── assets/
│   │   │   ├── components/
│   │   │   ├── services/
│   │   │   ├── dashboard.context.tsx
│   │   │   ├── dashboard.store.tsx
│   │   │   └── dashboard.tsx
│   │   ├── e-wallet/
│   │   │   ├── assets/
│   │   │   ├── components/
│   │   │   ├── services/
│   │   │   ├── e-wallet.context.tsx
│   │   │   ├── e-wallet.store.ts
│   │   │   └── e-wallet.tsx
│   │   ├── mobile-load/
│   │   │   ├── assets/
│   │   │   ├── components/
│   │   │   ├── services/
│   │   │   ├── mobile-load.context.tsx
│   │   │   ├── mobile-load.store.ts
│   │   │   └── mobile-load.tsx
│   │   ├── reports/
│   │   │   ├── assets/
│   │   │   ├── components/
│   │   │   ├── services/
│   │   │   ├── reports.context.tsx
│   │   │   ├── reports.store.ts
│   │   │   └── reports.tsx
│   │   ├── settings/
│   │   │   ├── assets/
│   │   │   ├── components/
│   │   │   ├── services/
│   │   │   ├── settings.context.tsx
│   │   │   ├── settings.store.ts
│   │   │   └── settings.tsx
│   │   ├── store-inventory/
│   │   │   ├── assets/
│   │   │   ├── components/
│   │   │   ├── services/
│   │   │   ├── store-inventory.context.tsx
│   │   │   ├── store-inventory.store.ts
│   │   │   └── store-inventory.tsx
│   │   └── store-sales/
│   │       ├── assets/
│   │       ├── components/
│   │       ├── services/
│   │       ├── store-sales.context.tsx
│   │       ├── store-sales.store.ts
│   │       └── store-sales.tsx
│   ├── App.css
│   ├── App.tsx
│   ├── index.css
│   └── main.tsx
├── eslint.config.js
├── index.html
├── package-lock.json
├── package.json
├── README.md
├── tsconfig.app.json
├── tsconfig.json
├── tsconfig.node.json
└── vite.config.ts
```

> The nested module folders shown here are recommended conventions.
> Create optional files and folders when the feature needs them; do not
> add empty context or store files just to match the template.

## 1. Root Directories and Files

  -----------------------------------------------------------------------
  Path                                Responsibility
  ----------------------------------- -----------------------------------
  `public/`                           Static files served directly
                                      without being imported through the
                                      application bundle

  `public/favicon.svg`                Browser tab and bookmark icon

  `public/icons.svg`                  Shared SVG symbol or icon sprite,
                                      if used

  `src/`                              Application source code

  `eslint.config.js`                  ESLint rules and lint configuration

  `index.html`                        Vite HTML entry document

  `package.json`                      Project metadata, dependencies, and
                                      scripts

  `package-lock.json`                 Locked dependency versions for
                                      reproducible installs

  `README.md`                         Setup, development, and project
                                      documentation

  `tsconfig.json`                     Root TypeScript configuration

  `tsconfig.app.json`                 TypeScript configuration for
                                      application code

  `tsconfig.node.json`                TypeScript configuration for
                                      Node-based tooling

  `vite.config.ts`                    Vite development and build
                                      configuration
  -----------------------------------------------------------------------

## 2. Source Directories

### `src/assets/`

Contains application-wide static assets: - Brand assets and shared
illustrations. - Images used by multiple modules. - Fonts and other
shared resources.

Keep feature-specific images inside the owning module's `assets/`
folder.

### `src/hooks/`

Contains reusable React hooks shared across modules.

Examples: - `use-debounce.ts` - `use-media-query.ts` - `use-mobile.ts` -
`use-pagination.ts` - `use-confirmation.ts`

A hook used by only one feature should normally remain inside that
feature's module.

### `src/layout/`

Contains the application shell and shared page layouts.

Suggested organization:

``` text
layout/
├── components/
│   ├── AppSidebar/
│   ├── AppHeader/
│   ├── AppNavigation/
│   ├── Breadcrumbs/
│   └── MobileNavigation/
├── MainLayout.tsx
└── AuthLayout.tsx
```

Responsibilities: - Main application layout. - Sidebar and header. -
Navigation and responsive navigation. - Page content container. -
Authentication layout, if required.

### `src/modules/`

Contains the application's business features. Each module owns its page,
feature components, API service functions, and module-specific state.

## 3. Module Responsibilities

  -----------------------------------------------------------------------
  Module                              Responsibility
  ----------------------------------- -----------------------------------
  `dashboard/`                        Business overview, summary cards,
                                      charts, recent transactions, and
                                      inventory alerts

  `e-wallet/`                         GCash and Maya cash-in / cash-out
                                      transaction recording, fee
                                      previews, and transaction history

  `mobile-load/`                      TNT, Smart, DITO, Globe, and TM
                                      load transactions, fee
                                      calculations, and history

  `reports/`                          Financial, e-wallet, mobile-load,
                                      sales, and inventory reports with
                                      date filters and exports

  `settings/`                         Business profile, fee rules,
                                      inventory preferences, POS
                                      preferences, and account settings

  `store-inventory/`                  Product catalog, categories, stock
                                      receiving, batches, stock
                                      adjustments, and expiration
                                      tracking

  `store-sales/`                      Store sales history, sale details,
                                      receipts, voids, and refunds
  -----------------------------------------------------------------------

### Suggested feature components

**Dashboard** - `SummaryCards/` - `RevenueChart/` -
`TransactionOverview/` - `RecentTransactions/` - `LowStockAlerts/` -
`ExpirationAlerts/`

**E-Wallet** - `EwalletSummary/` - `EwalletTable/` - `EwalletForm/` -
`EwalletFilters/` - `EwalletDetails/` - `FeePreview/`

**Mobile Load** - `LoadSummary/` - `LoadTransactionTable/` -
`LoadTransactionForm/` - `LoadFilters/` - `NetworkSelector/` -
`FeePreview/`

**Reports** - `ReportFilters/` - `BusinessSummaryReport/` -
`EwalletReport/` - `MobileLoadReport/` - `SalesReport/` -
`ProfitReport/` - `InventoryReport/` - `ExportActions/`

**Settings** - `BusinessProfileForm/` - `FeeRuleManager/` -
`FeeRuleForm/` - `InventorySettings/` - `PosSettings/` -
`AccountSettings/` - `BackupSettings/`

**Store Inventory** - `InventorySummary/` - `ProductTable/` -
`ProductForm/` - `ProductDetails/` - `CategoryManager/` -
`StockInForm/` - `StockAdjustmentForm/` - `InventoryBatchTable/` -
`StockMovementTable/` - `LowStockList/` - `ExpirationList/`

**Store Sales** - `SalesSummary/` - `SalesTable/` - `SaleDetails/` -
`ReceiptViewer/` - `VoidSaleDialog/` - `RefundForm/` - `SalesFilters/`

> **POS placement:** The supplied structure does not include a separate
> `pos/` module. If the application has a dedicated cashier / checkout
> screen, consider adding `src/modules/pos/`. Keep `store-sales/`
> focused on sales history and after-sale operations. Alternatively, if
> checkout is intentionally part of the sales feature, keep POS
> components inside `store-sales/components/pos/`.

## 4. Standard Module Convention

A module should follow this pattern:

``` text
module-name/
├── assets/
├── components/
│   ├── FeatureComponent/
│   │   ├── FeatureComponent.tsx
│   │   ├── feature-component.schema.ts
│   │   └── index.ts
│   └── AnotherComponent/
├── services/
│   └── module-name.service.ts
├── module-name.context.tsx
├── module-name.store.ts
└── module-name.tsx
```

  -----------------------------------------------------------------------
  File / Directory                    Responsibility
  ----------------------------------- -----------------------------------
  `assets/`                           Static resources used only by this
                                      module

  `components/`                       Feature-specific UI components

  `services/`                         Typed API calls and service
                                      functions

  `module-name.context.tsx`           Optional React Context provider

  `module-name.store.ts`              Optional Zustand store for
                                      client-side UI state

  `module-name.tsx`                   Main page component that composes
                                      the module
  -----------------------------------------------------------------------

### Example: E-Wallet module

``` text
e-wallet/
├── assets/
├── components/
│   ├── EwalletForm/
│   │   ├── EwalletForm.tsx
│   │   ├── ewallet-form.schema.ts
│   │   └── index.ts
│   ├── EwalletTable/
│   │   ├── EwalletTable.tsx
│   │   └── index.ts
│   └── FeePreview/
├── services/
│   └── e-wallet.service.ts
├── e-wallet.context.tsx
├── e-wallet.store.ts
└── e-wallet.tsx
```

## 5. Application Entry Files

### `src/main.tsx`

The Vite entry point. It mounts the React application and imports global
styles.

Typical responsibilities: - Import `index.css`. - Initialize the React
root. - Render `App`. - Register application-level providers when
appropriate.

### `src/App.tsx`

The application root.

Typical responsibilities: - Configure the router. - Register global
providers. - Define application-level composition. - Render the selected
route and layout.

### `src/App.css`

Contains styles specific to the root application component. Prefer
shared design tokens and global styles in `index.css` where appropriate.

### `src/index.css`

Contains global styles: - CSS reset and base styles. - Font
declarations. - Theme variables. - Global background and typography. -
Shared design tokens.

## 6. State Management Guidelines

  State type                                 Recommended solution
  ------------------------------------------ --------------------------------------
  API data, caching, refetching, mutations   TanStack Query
  Shared client-side UI state                Zustand
  Local component state                      React `useState` / `useReducer`
  Dependency or scoped provider state        React Context, when useful
  Form state and validation                  React Hook Form with Zod, if adopted

Avoid storing the same server data in both TanStack Query and Zustand.
The backend remains the source of truth for transactions, fee
calculations, inventory quantities, sales, and profit.

## 7. Service Layer Guidelines

Each module should call its own service functions, using a shared
configured API client.

Example:

``` text
src/
├── services/
│   └── api-client.ts
└── modules/
    └── e-wallet/
        └── services/
            └── e-wallet.service.ts
```

Service responsibilities may include: - Fetching transaction lists and
details. - Creating transactions. - Updating transaction statuses. -
Requesting fee previews. - Fetching report data.

Keep HTTP request logic out of page and presentation components.

## 8. Naming Conventions

-   Module directories: `kebab-case`, such as `mobile-load`.
-   Component directories and component files: `PascalCase`, such as
    `EwalletTable/EwalletTable.tsx`.
-   Hooks: `use-` prefix and `kebab-case`, such as `use-mobile.ts`.
-   Service files: `<module-name>.service.ts`.
-   Store files: `<module-name>.store.ts`.
-   Context files: `<module-name>.context.tsx`.
-   Page files: `<module-name>.tsx`.
-   Type and schema files: descriptive `kebab-case` names.

If the existing project uses `.store.tsx`, it can remain, but a
Zustand-only store generally does not need the `.tsx` extension.

## 9. Architecture Rules

1.  Keep feature-specific components, services, and state inside their
    owning module.
2.  Move code into shared directories only when it is genuinely reused
    across features.
3.  Keep page components focused on composing components and
    coordinating page-level behavior.
4.  Keep API calls inside service files.
5.  Use TanStack Query for server state rather than duplicating API data
    in Zustand.
6.  Use Context and Zustand only when there is a clear state-management
    need; do not create empty files just to match the template.
7.  Keep financial calculations authoritative on the backend.
8.  Treat inventory as the source of truth for available stock and batch
    costs.
9.  Ensure POS checkout, payment recording, and stock deduction are
    atomic backend operations.
10. Preserve audit history for financial transactions, inventory
    movements, voids, and refunds.

## 10. Recommended Implementation Order

1.  Set up the application entry point, routing, and shared providers.
2.  Build the responsive application shell and navigation.
3.  Configure the shared API client and query client.
4.  Implement authentication and settings.
5.  Implement e-wallet and mobile-load transaction modules.
6.  Implement inventory and batch tracking.
7.  Implement POS checkout and sales history.
8.  Implement dashboard analytics and reports.
9.  Add tests for fee calculations, stock movements, checkout, voids,
    and refunds.
