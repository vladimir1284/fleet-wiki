# Part, Category, Location, and Vendor Models Documentation

This document provides an overview of the `Part`, `Category`, `Location`, and `Vendor` models within the Prisma schema, including their relationships and fields.

## Model: Part

### Fields

- `id`: A unique identifier for each part, generated using `cuid()`.
- `name`: The name of the part.
- `number`: The part number.
- `criticalQty`: The critical quantity of the part.
- `upc`: The Universal Product Code (UPC) of the part.
- `description`: A detailed description of the part.
- `extendedPartData`: Additional data about the part in JSON format.
- `image`: An optional image URL for the part.
- `createdAt`, `updatedAt`, `deletedAt`: Timestamps for creation, last update, and deletion of the part.
- `categories`, `locations`, `vendors`: Relations to other models indicating the categories, locations, and vendors associated with the part.
- `createdBy`, `updatedBy`, `deletedBy`: IDs of the users who created, updated, or deleted the part.
- `tenantId`, `tenant`: Multi-tenant identification fields.

### Relations

- `creationAuthor`, `updateAuthor`, `deletionAuthor`: Relations to the `TenantUser` model, indicating the users who created, updated, or deleted the part.
- `tenant`: A relation to the `Tenant` model, indicating the tenant associated with the part.

## Model: Category

### Fields

- `id`: A unique identifier for each category, generated using `cuid()`.
- `name`: The name of the category, which must be unique.
- `createdAt`, `updatedAt`, `deletedAt`: Timestamps for creation, last update, and deletion of the category.
- `parts`: Relations to the `Part` model, indicating the parts associated with the category.
- `tenantId`, `tenant`: Multi-tenant identification fields.

### Relations

- `tenant`: A relation to the `Tenant` model, indicating the tenant associated with the category.

## Model: Location

### Fields

- `id`: A unique identifier for each location, generated using `cuid()`.
- `name`: The name of the location, which must be unique.
- `createdAt`, `updatedAt`, `deletedAt`: Timestamps for creation, last update, and deletion of the location.
- `parts`: Relations to the `Part` model, indicating the parts associated with the location.
- `tenantId`, `tenant`: Multi-tenant identification fields.

### Relations

- `tenant`: A relation to the `Tenant` model, indicating the tenant associated with the location.

## Model: Vendor

### Fields

- `id`: A unique identifier for each vendor, generated using `cuid()`.
- `name`: The name of the vendor, which must be unique.
- `createdAt`, `updatedAt`, `deletedAt`: Timestamps for creation, last update, and deletion of the vendor.
- `parts`: Relations to the `Part` model, indicating the parts associated with the vendor.
- `tenantId`, `tenant`: Multi-tenant identification fields.

### Relations

- `tenant`: A relation to the `Tenant` model, indicating the tenant associated with the vendor.

## Model: CategoriesOnParts

### Fields

- `partId`, `categoryId`: Identifiers for the part and category, forming a composite primary key.

### Relations

- `part`: A relation to the `Part` model, indicating the part associated with the category.
- `category`: A relation to the `Category` model, indicating the category associated with the part.

## Model: LocationsOnParts

### Fields

- `partId`, `locationId`: Identifiers for the part and location, forming a composite primary key.
- `quantity`, `unit`: Quantity and unit of the part at the location.

### Relations

- `part`: A relation to the `Part` model, indicating the part associated with the location.
- `location`: A relation to the `Location` model, indicating the location associated with the part.

## Model: VendorOnParts

### Fields

- `partId`, `vendorId`: Identifiers for the part and vendor, forming a composite primary key.
- `cost`: The cost of the part from the vendor.

### Relations

- `part`: A relation to the `Part` model, indicating the part associated with the vendor.
- `vendor`: A relation to the `Vendor` model, indicating the vendor associated with the part.