# Client Model

Represents a client associated with a tenant.

Fields:

- `id`: Unique identifier for the client.
- `name`: Name of the client.
- `email`: Email address of the client.
- `phoneNumber`: Phone number of the client, must be unique.
- `avatar`: URL to the client's profile picture.
- `tenantId`: Associated tenant ID.

Relationship:

- `tenant`: One-to-one relationship with the `Tenant` model, indicating the tenant of the client.

---

