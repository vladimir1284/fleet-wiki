
# Custom Inspection Forms

The **CustomForm** system empowers users with the ability to create personalized forms tailored to specific needs within a multi-tenant environment. This section delves into the intricacies of three interconnected models: **CustomForm**, **CustomField**, and **CustomFieldResponse**. These models collectively facilitate the dynamic creation, customization, and comprehensive tracking of forms, custom fields, and user responses. Discover how this structured system provides flexibility and versatility for effective form management and user engagement within the broader context of tenant-specific requirements.

<iframe width="100%" height="315" src='https://dbdiagram.io/e/65c5169fac844320aec1e173/65c516b6ac844320aec1e399'> </iframe>

## CustomForm Model

The **CustomForm** model facilitates the creation of personalized forms that are linked to tenant users. 
Each form boasts a distinctive name, a creation timestamp, and the ability to incorporate a variety of custom fields represented by the **CustomField** model. 
Furthermore, a relationship is established to manage the association with a tenant user, allowing for a flexible and customizable design for form management within the system.

## CustomField Model

The **CustomField** model defines the custom fields that can be integrated into a personalized form. 
Each field possesses a descriptive name, a type defining the nature of the data it can contain, and the option to be marked as mandatory. 
It is connected to a form through a relationship with the **CustomForm** model and can have user-provided responses associated with it, managed through the relationship with the **CustomFieldResponse** model. 
This design enables a versatile and comprehensive structure for managing custom fields in forms.

## CustomFieldResponse Model

The **CustomFieldResponse** model records user responses to custom fields in forms. 
Each response is linked to a [TenantUser](../user/#tenantuser-model), the associated custom field, and has content associated with it. 
Additionally, the creation timestamp of the response is recorded. 
This design allows for the comprehensive tracking and management of user responses within the context of custom fields in forms.

