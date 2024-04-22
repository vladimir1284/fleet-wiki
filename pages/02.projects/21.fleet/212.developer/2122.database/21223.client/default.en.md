# Client Model

Represents a client associated with a tenant.

## Fields

- `id`: A unique identifier for each `Client`. It's an auto-incrementing integer.
- `name`: The name of the client.
- `email`: The email address of the client. It's unique across all clients.
- `phoneNumber`: The phone number of the client. It's unique across all clients and must adhere to a specific format.
- `avatar`: An optional field for storing the URL of the client's avatar image.
- `tenantId`: The identifier of the tenant the client belongs to. It's a foreign key referencing the `Tenant` model.
- `tenant`: A relation to the `Tenant` model, indicating which tenant the client is associated with.
- `contracts`: A one-to-many relationship with the `Contract` model, indicating the contracts associated with this client.

## Relationships

- `tenant`: A relation to the `Tenant` model, indicating which tenant the client is associated with.
- `contracts`: A one-to-many relationship with the `Contract` model, indicating the contracts associated with this client.

## Special Annotations

- The `phoneNumber` field uses a custom validation annotation to ensure the phone number is in a valid format.

---

