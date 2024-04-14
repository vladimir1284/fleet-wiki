# Custom Inspection Forms

The **CustomForm** system empowers users with the ability to create personalized forms tailored to specific needs within a multi-tenant environment. This section delves into the intricacies of three interconnected models: **CustomForm**, **CustomField**, and **CustomFieldResponse**. These models collectively facilitate the dynamic creation, customization, and comprehensive tracking of forms, custom fields, and user responses. Discover how this structured system provides flexibility and versatility for effective form management and user engagement within the broader context of tenant-specific requirements.

<iframe width="100%" height="315" src='https://dbdiagram.io/e/65fdc6ecae072629cebcc19a/65fdc72fae072629cebcc5da'> </iframe>

## CustomForm Model

The **CustomForm** model makes it easy to create custom forms that are tied to tenant users. Each form has a distinctive name, a creation timestamp, and the ability to embed a variety of custom fields represented by the **CustomField** model. Additionally, a relationship is established to manage the association with a tenant user, allowing for a flexible and customizable design for forms management within the system.

## Card Model

The **Card** model represents a card that can contain multiple custom fields and is associated with a custom form through the relationship established with the **CustomForm** model. Each card has a unique name and can contain a list of fields represented by the **CustomField** model, providing an organizational structure for the data within the form.

## FormFieldType Enum

The **FormFieldType** enum lists the different types of fields that can be used in custom forms, including text fields, numbers, and checkboxes. This enumeration provides a predefined list of field types that can be used to configure custom fields on forms.

## CustomField Model

The **CustomField** model represents a custom field within a custom form. Each field has a distinguished name, a type defined by the **FormFieldType** enum, and can be marked as required. Additionally, you can have associated check options represented by the **CheckOption** model and associated responses represented by the **CustomFieldResponse** model. A relationship is established with a card through the **Card** model to organize the fields within the form.

## CheckOption Model

The **CheckOption** model represents the options available for check fields on a custom form. Each option can have a name and is associated with a custom field through the relationship established with the **CustomField** model. Additionally, it can have associated responses represented by the **CustomFieldResponse** model.

## CustomFieldResponse Model

The **CustomFieldResponse** model represents the response to a custom field on a form. Each response can contain content, notes, and a creation timestamp. It is associated with a tenant user through the **[TenantUser](../user/#tenantuser-model)** model and to the corresponding custom field through the **CustomField** model. Additionally, it can be associated with a verification option and/or an inspection, providing a detailed record of the responses provided by users.

## Inspection Model

The **Inspection** model represents an inspection performed against a custom form. Each inspection has a creation timestamp and is associated with a tenant user, a vehicle, and a custom form through relationships established with the **[TenantUser](../user/#tenantuser-model)**, **Vehicle**, and **CustomForm** models respectively. . Additionally, it may contain associated responses represented by the **CustomFieldResponse** model.
