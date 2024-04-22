# CustomForm, Card, and Related Models Documentation

This document provides an overview of the `CustomForm`, `Card`, and related models within the Prisma schema.

## Model: CustomForm

### Fields

- `id`: An integer that serves as the unique identifier for each `CustomForm` record. It is auto-incremented.
- `name`: A string that stores the name of the custom form.
- `tenantId`: An integer that stores the ID of the associated tenant.
- `tenant`: A relation field that links to the `Tenant` model. This field represents the tenant associated with the custom form.
- `createdAt`: A DateTime field that stores the creation date and time of the custom form. By default, it is set to the current date and time.
- `isActive`: A boolean field that indicates whether the custom form is active. By default, this field is set to `true`.
- `inspections`: A relation field that links to the `Inspection` model. This field represents the inspections associated with the custom form.
- `cards`: A relation field that links to the `Card` model. This field represents the cards associated with the custom form.

### Relations

- `tenant`: This model has a one-to-one relation with the `Tenant` model. Each `CustomForm` is associated with one `Tenant`, and each `Tenant` can have multiple `CustomForm` records.
- `inspections`: This model has a one-to-many relation with the `Inspection` model. Each `CustomForm` can have multiple `Inspection` records associated with it.
- `cards`: This model has a one-to-many relation with the `Card` model. Each `CustomForm` can have multiple `Card` records associated with it.

## Model: Card

### Fields

- `id`: An integer that serves as the unique identifier for each `Card` record. It is auto-incremented.
- `name`: A string that stores the name of the card.
- `formId`: An integer that stores the ID of the associated custom form.
- `form`: A relation field that links to the `CustomForm` model. This field represents the custom form associated with the card.
- `fields`: A relation field that links to the `CustomField` model. This field represents the custom fields associated with the card.

### Relations

- `form`: This model has a one-to-one relation with the `CustomForm` model. Each `Card` is associated with one `CustomForm`, and each `CustomForm` can have multiple `Card` records.
- `fields`: This model has a one-to-many relation with the `CustomField` model. Each `Card` can have multiple `CustomField` records associated with it.

## Model: CustomField

### Fields

- `id`: An integer that serves as the unique identifier for each `CustomField` record. It is auto-incremented.
- `name`: A string that stores the name of the custom field.
- `type`: An enum field that specifies the type of the custom field. The possible values are `TEXT`, `NUMBER`, `SINGLE_CHECK`, `IMAGE`, `SIGNATURE`, `EMAIL`, `PHONE`, `DATE`, and `TIME`.
- `required`: A nullable boolean field that indicates whether the custom field is required. By default, this field is set to `true`.
- `checkOptions`: A relation field that links to the `CheckOption` model. This field represents the check options associated with the custom field.
- `responses`: A relation field that links to the `CustomFieldResponse` model. This field represents the responses associated with the custom field.
- `card`: A nullable relation field that links to the `Card` model. This field represents the card associated with the custom field.
- `cardId`: A nullable integer that stores the ID of the associated card.

### Relations

- `checkOptions`: This model has a one-to-many relation with the `CheckOption` model. Each `CustomField` can have multiple `CheckOption` records associated with it.
- `responses`: This model has a one-to-many relation with the `CustomFieldResponse` model. Each `CustomField` can have multiple `CustomFieldResponse` records associated with it.
- `card`: This model has a one-to-one relation with the `Card` model. Each `CustomField` is associated with one `Card`, and each `Card` can have multiple `CustomField` records.

## Model: CustomFieldResponse

### Fields

- `id`: An integer that serves as the unique identifier for each `CustomFieldResponse` record. It is auto-incremented.
- `content`: A nullable string field that stores the content of the response if it is text or number.
- `checked`: A nullable boolean field that indicates whether the response is checked if it is a checkbox or radio button.
- `note`: A nullable string field that stores additional notes or descriptions about the response.
- `createdAt`: A DateTime field that stores the creation date and time of the response. By default, it is set to the current date and time.
- `tenantUserId`: An integer that stores the ID of the associated tenant user.
- `user`: A relation field that links to the `TenantUser` model. This field represents the tenant user associated with the response.
- `fieldId`: An integer that stores the ID of the associated custom field.
- `field`: A relation field that links to the `CustomField` model. This field represents the custom field associated with the response.
- `checkOptionId`: A nullable integer that stores the ID of the associated check option.
- `checkOption`: A nullable relation field that links to the `CheckOption` model. This field represents the check option associated with the response.
- `inspectionId`: A nullable integer that stores the ID of the associated inspection.
- `inspection`: A nullable relation field that links to the `Inspection` model. This field represents the inspection associated with the response.

### Relations

- `user`: This model has a one-to-one relation with the `TenantUser` model. Each `CustomFieldResponse` is associated with one `TenantUser`, and each `TenantUser` can have multiple `CustomFieldResponse` records.
- `field`: This model has a one-to-one relation with the `CustomField` model. Each `CustomFieldResponse` is associated with one `CustomField`, and each `CustomField` can have multiple `CustomFieldResponse` records.
- `checkOption`: This model has a one-to-one relation with the `CheckOption` model. Each `CustomFieldResponse` is associated with one `CheckOption`, and each `CheckOption` can have multiple `CustomFieldResponse` records.
- `inspection`: This model has a one-to-one relation with the `Inspection` model. Each `CustomFieldResponse` is associated with one `Inspection`, and each `Inspection` can have multiple `CustomFieldResponse` records.

## Model: Inspection

### Fields

- `id`: An integer that serves as the unique identifier for each `Inspection` record. It is auto-incremented.
- `createdAt`: A DateTime field that stores the creation date and time of the inspection. By default, it is set to the current date and time.
- `customFormId`: An integer that stores the ID of the associated custom form.
- `customForm`: A relation field that links to the `CustomForm` model. This field represents the custom form associated with the inspection.
- `tenantId`: An integer that stores the ID of the associated tenant.
- `tenant`: A relation field that links to the `Tenant` model. This field represents the tenant associated with the inspection.
- `vehicleId`: An integer that stores the ID of the associated vehicle.
- `vehicle`: A relation field that links to the `Vehicle` model. This field represents the vehicle associated with the inspection.
- `tenantUserId`: An integer that stores the ID of the associated tenant user.
- `user`: A relation field that links to the `TenantUser` model. This field represents the tenant user associated with the inspection.
- `responses`: A relation field that links to the `CustomFieldResponse` model. This field represents the responses associated with the inspection.

### Relations

- `customForm`: This model has a one-to-one relation with the `CustomForm` model. Each `Inspection` is associated with one `CustomForm`, and each `CustomForm` can have multiple `Inspection` records.
- `tenant`: This model has a one-to-one relation with the `Tenant` model. Each `Inspection` is associated with one `Tenant`, and each `Tenant` can have multiple `Inspection` records.
- `vehicle`: This model has a one-to-one relation with the `Vehicle` model. Each `Inspection` is associated with one `Vehicle`, and each `Vehicle` can have multiple `Inspection` records.
- `user`: This model has a one-to-one relation with the `TenantUser` model. Each `Inspection` is associated with one `TenantUser`, and each `TenantUser` can have multiple `Inspection` records.
- `responses`: This model has a one-to-many relation with the `CustomFieldResponse` model. Each `Inspection` can have multiple `CustomFieldResponse` records associated with it.