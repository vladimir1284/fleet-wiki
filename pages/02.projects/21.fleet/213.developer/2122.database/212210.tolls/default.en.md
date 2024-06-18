# TollDue Model Documentation

This document provides an overview of the `TollDue` model within the Prisma schema, including its fields, relations, and the associated `TollDueStage` enum.

## Enum: TollDueStage

The `TollDueStage` enum defines the payment status of a toll due.

- `PAID`: Indicates that the toll has been paid.
- `UNPAID`: Indicates that the toll has not been paid yet.

## Model: TollDue

### Fields

- `id`: An integer that serves as the unique identifier for each `TollDue` record. It is auto-incremented.
- `amount`: An integer representing the amount of the toll due.
- `plate`: A relation field that links to the `VehiclePlate` model. This field represents the vehicle plate associated with the toll due.
- `plateId`: An integer that stores the ID of the associated vehicle plate.
- `contract`: A relation field that links to the `Contract` model. This field represents the contract associated with the toll due.
- `contractId`: An integer that stores the ID of the associated contract.
- `stage`: A `TollDueStage` enum indicating the payment status of the toll due.
- `invoice`: An optional string field that stores the invoice associated with the toll due.
- `invoiceNumber`: An optional string field that stores the invoice number associated with the toll due.
- `createDate`: A DateTime field that stores the date the toll due was created.
- `note`: An optional string field that stores any notes or comments related to the toll due.

### Relations

- `plate`: This model has a one-to-one relation with the `VehiclePlate` model. Each `TollDue` is associated with one `VehiclePlate`, and each `VehiclePlate` can have one `TollDue`.
- `contract`: This model has a one-to-one relation with the `Contract` model. Each `TollDue` is associated with one `Contract`, and each `Contract` can have one `TollDue`.