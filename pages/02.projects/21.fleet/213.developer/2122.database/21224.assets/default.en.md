---
title: Vehicles
---

# Vehicle models

The `Vehicle` model represents a vehicle within the system, typically associated with a tenant and possibly with specific clients or users. It includes information about the vehicle's details, such as make, model, year, and registration number, as well as a reference to the tenant it belongs to.

## Fields

- `id`: A unique identifier for each `Vehicle`. It's an auto-incrementing integer.
- `make`: The make of the vehicle.
- `model`: The model of the vehicle.
- `year`: The year the vehicle was manufactured.
- `registrationNumber`: The registration number of the vehicle. It's unique across all vehicles.
- `tenantId`: The identifier of the tenant the vehicle belongs to. It's a foreign key referencing the `Tenant` model.
- `tenant`: A relation to the `Tenant` model, indicating which tenant the vehicle is associated with.
- `clients`: A many-to-many relationship with the `Client` model, indicating the clients associated with this vehicle.
- `inspections`: A one-to-many relationship with the `Inspection` model, indicating the inspections conducted on this vehicle.

## Relationships

- `tenant`: A relation to the `Tenant` model, indicating which tenant the vehicle is associated with.
- `clients`: A many-to-many relationship with the `Client` model, indicating the clients associated with this vehicle.
- `inspections`: A one-to-many relationship with the `Inspection` model, indicating the inspections conducted on this vehicle.

## Special Annotations

- The `registrationNumber` field uses a custom validation annotation to ensure the registration number is in a valid format.



# VehiclePlate Documentation

The `VehiclePlate` model represents a vehicle's license plate information within the system, typically associated with a specific vehicle. It includes information about the plate number, its type (e.g., front, rear), and possibly the state or region it's registered in.

## Fields

- `id`: A unique identifier for each `VehiclePlate`. It's an auto-incrementing integer.
- `plateNumber`: The license plate number of the vehicle. It's unique across all vehicle plates.
- `type`: The type of the license plate, such as "Front", "Rear", or "Custom".
- `region`: The region or state the license plate is registered in. This field is optional.
- `vehicleId`: The identifier of the vehicle the plate is associated with. It's a foreign key referencing the `Vehicle` model.
- `vehicle`: A relation to the `Vehicle` model, indicating which vehicle the plate is associated with.

## Relationships

- `vehicle`: A relation to the `Vehicle` model, indicating which vehicle the plate is associated with.

## Special Annotations

- The `plateNumber` field uses a custom validation annotation to ensure the plate number is in a valid format.
- The `type` field uses an enum to restrict the values to predefined types.



# Vehicle Picture Documentation

This document provides an overview of the `VehiclePicture` model within the Prisma schema.

## Model: VehiclePicture

### Fields

- `id`: An integer that serves as the unique identifier for each `VehiclePicture` record. It is auto-incremented.
- `image`: A string that stores the image URL or path of the vehicle picture.
- `vehicle`: A relation field that links to the `Vehicle` model. This field represents the vehicle associated with the picture.
- `vehicleId`: An integer that stores the ID of the associated vehicle. This field is used to establish the relation with the `Vehicle` model.
- `pinned`: A boolean field that indicates whether the picture is pinned or not. By default, this field is set to `false`.

### Relations

- `vehicle`: This model has a one-to-one relation with the `Vehicle` model. Each `VehiclePicture` is associated with one `Vehicle`, and each `Vehicle` can have one `VehiclePicture`.



# Document and DocumentTag Models Documentation

This document provides an overview of the `Document` and `DocumentTag` models within the Prisma schema.

## Model: Document

### Fields

- `id`: An integer that serves as the unique identifier for each `Document` record. It is auto-incremented.
- `file`: A string that stores the file path or URL of the document.
- `name`: A string that stores the name of the document.
- `note`: A string that stores additional notes or descriptions about the document.
- `document_type`: A string that specifies the type of the document.
- `expiration_date`: A nullable DateTime field that stores the expiration date of the document.
- `remainder_days`: A nullable integer field that stores the number of days remaining until the document expires.
- `isActive`: A boolean field that indicates whether the document is active. By default, this field is set to `true`.
- `createdAt`: A DateTime field that stores the creation date and time of the document. By default, it is set to the current date and time.
- `vehicle`: A relation field that links to the `Vehicle` model. This field represents the vehicle associated with the document.
- `vehicleId`: An integer that stores the ID of the associated vehicle. This field is used to establish the relation with the `Vehicle` model.
- `tags`: A relation field that links to the `DocumentTag` model. This field represents the tags associated with the document.
- `extraFields`: A nullable JSON field that can store additional, flexible data related to the document.

### Relations

- `vehicle`: This model has a one-to-one relation with the `Vehicle` model. Each `Document` is associated with one `Vehicle`, and each `Vehicle` can have one `Document`.
- `tags`: This model has a one-to-many relation with the `DocumentTag` model. Each `Document` can have multiple `DocumentTag` records associated with it.

## Model: DocumentTag

### Fields

- `id`: An integer that serves as the unique identifier for each `DocumentTag` record. It is auto-incremented.
- `name`: A string that stores the name of the tag.
- `document`: A relation field that links to the `Document` model. This field represents the document associated with the tag.
- `documentId`: An integer that stores the ID of the associated document. This field is used to establish the relation with the `Document` model.

### Relations

- `document`: This model has a many-to-one relation with the `Document` model. Each `DocumentTag` is associated with one `Document`, and each `Document` can have multiple `DocumentTag` records associated with it.