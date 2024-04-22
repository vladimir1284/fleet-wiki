# CostCategory Enum and Cost Model Documentation

This document provides an overview of the `CostCategory` enum and the `Cost` model within the Prisma schema.

## Enum: CostCategory

The `CostCategory` enum categorizes costs into three main groups: Fixed Costs, Variable Costs, and Additional Costs. Each category represents a different aspect of the costs associated with a vehicle.

### Fixed Costs

- `Purchase`: The cost of purchasing the vehicle.
- `Depreciation`: The depreciation of the vehicle over time.
- `Financing`: The cost of financing the vehicle.
- `Insurance`: The cost of insurance for the vehicle.
- `Taxes`: Taxes related to the vehicle.
- `PreventativeMaintenance`: Costs associated with preventative maintenance of the vehicle.
- `Storage`: Costs for storing the vehicle.
- `PermitsAndLicenses`: Costs for permits and licenses required for the vehicle.

### Variable Costs

- `Fuel`: The cost of fuel for the vehicle.
- `Repairs`: Costs for repairs and maintenance.
- `Cleaning`: Costs for cleaning the vehicle.
- `TollsAndHighways`: Costs for tolls and highway usage.
- `RoadsideAssistance`: Costs for roadside assistance.
- `MarketingAndAdvertising`: Costs for marketing and advertising the vehicle.
- `AdministrativeExpenses`: Administrative expenses related to the vehicle.
- `Commissions`: Commissions paid for the vehicle.

### Additional Costs

- `AdditionalEquipment`: Costs for additional equipment.
- `RentalInsurance`: Costs for rental insurance.
- `Deductible`: Deductible amounts for insurance.
- `CleaningFee`: Fees for cleaning services.
- `AdditionalMileage`: Additional mileage costs.

## Model: Cost

### Fields

- `id`: An integer that serves as the unique identifier for each `Cost` record. It is auto-incremented.
- `value`: A float that stores the value of the cost.
- `concept`: A string that stores the concept or description of the cost.
- `category`: An array of `CostCategory` enums that categorizes the cost.
- `date`: A DateTime field that stores the date of the cost.
- `vehicle`: A relation field that links to the `Vehicle` model. This field represents the vehicle associated with the cost.
- `vehicleId`: An integer that stores the ID of the associated vehicle.

### Relations

- `vehicle`: This model has a one-to-one relation with the `Vehicle` model. Each `Cost` is associated with one `Vehicle`, and each `Vehicle` can have multiple `Cost` records.