# RentalPlan, Contract, StageUpdate, and Note Models Documentation

This document provides an overview of the `RentalPlan`, `Contract`, `StageUpdate`, and `Note` models within the Prisma schema, including their relationships and fields.

## Enum: Periodicity

The `Periodicity` enum defines the frequency at which a rental plan can be applied.

- `WEEKLY`: The rental plan is applied on a weekly basis.
- `BIWEEKLY`: The rental plan is applied on a biweekly basis.
- `MONTHLY`: The rental plan is applied on a monthly basis.

## Model: RentalPlan

### Fields

- `id`: An integer that serves as the unique identifier for each `RentalPlan` record. It is auto-incremented.
- `amount`: An integer representing the amount of the rental plan.
- `name`: A string representing the name of the rental plan.
- `periodicity`: A `Periodicity` enum indicating the frequency of the rental plan.
- `contracts`: A relation field that links to the `Contract` model. This field represents the contracts associated with the rental plan.

### Relations

- `contracts`: This model has a one-to-many relation with the `Contract` model. Each `RentalPlan` can be associated with multiple `Contract` records.

## Model: Contract

### Fields

- `id`: An integer that serves as the unique identifier for each `Contract` record. It is auto-incremented.
- `client`: A relation field that links to the `Client` model. This field represents the client associated with the contract.
- `clientId`: An integer that stores the ID of the associated client.
- `rentalPlan`: A relation field that links to the `RentalPlan` model. This field represents the rental plan associated with the contract.
- `rentalPlanId`: An integer that stores the ID of the associated rental plan.
- `vehicle`: A relation field that links to the `Vehicle` model. This field represents the vehicle associated with the contract.
- `vehicleId`: An integer that stores the ID of the associated vehicle.
- `stage`: A relation field that links to the `StageUpdate` model. This field represents the current stage of the contract.
- `stageId`: An integer that stores the ID of the associated stage.
- `creationDate`: A DateTime field that stores the date the contract was created. It defaults to the current date and time.
- `activeDate`: An optional DateTime field that stores the date the contract became active.
- `endDate`: An optional DateTime field that stores the date the contract ended.
- `tolls`: A relation field that links to the `TollDue` model. This field represents the tolls due for the contract.
- `notes`: A relation field that links to the `Note` model. This field represents the notes associated with the contract.

### Relations

- `client`, `rentalPlan`, `vehicle`, `stage`, `tolls`, `notes`: These fields represent relations to other models, indicating the associated entities for the contract.

## Model: StageUpdate

### Fields

- `id`: An integer that serves as the unique identifier for each `StageUpdate` record. It is auto-incremented.
- `date`: A DateTime field that stores the date of the stage update.
- `reason`: An optional string field that stores the reason for the stage update.
- `comments`: An optional string field that stores comments related to the stage update.
- `previousStage`: A relation field that links to another `StageUpdate` model. This field represents the previous stage of the contract.
- `previousStageId`: An optional integer that stores the ID of the previous stage.
- `stage`: A `Stage` enum indicating the current stage of the contract.

### Relations

- `previousStage`: This model has a one-to-one relation with itself. Each `StageUpdate` can have one previous `StageUpdate`.
- `contracts`: This model has a one-to-many relation with the `Contract` model. Each `StageUpdate` can be associated with multiple `Contract` records.

## Model: Note

### Fields

- `id`: An integer that serves as the unique identifier for each `Note` record. It is auto-incremented.
- `contract`: A relation field that links to the `Contract` model. This field represents the contract associated with the note.
- `contractId`: An integer that stores the ID of the associated contract.
- `user`: A relation field that links to the `User` model. This field represents the user who created the note.
- `userId`: A string that stores the ID of the associated user.
- `Subject`: A string representing the subject of the note.
- `Body`: A string representing the body of the note.
- `createdDate`: A DateTime field that stores the date the note was created.
- `reminder`: An optional DateTime field that stores the date of the reminder for the note.
- `file`: An optional string field that stores the file path of an associated file with the note.

### Relations

- `contract`, `user`: These fields represent relations to other models, indicating the associated entities for the note.