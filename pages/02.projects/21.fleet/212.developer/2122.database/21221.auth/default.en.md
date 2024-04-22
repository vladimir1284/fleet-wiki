
# VerificationToken Model

Stores verification tokens for users.

Fields:

- `identifier`: Identifier for the token.
- `token`: Unique token string.
- `expires`: Expiration datetime of the token.
---

# Session Model

Represents a user session with a unique token.

Fields:

- `id`: Unique identifier for the session.
- `sessionToken`: Unique session token.
- `userId`: Associated user ID.
- `expires`: Expiration datetime of the session.

Relationship:

- `user`: One-to-one relationship with the `User` model, indicating the user of the session.
---

# Account Model

Represents a user account associated with various providers. Each account is uniquely identified by a combination of `provider` and `providerAccountId`.

Fields:

- `id`: Unique identifier for the account.
- `userId`: Associated user ID.
- `type`: Type of the account.
- `provider`: Provider of the account (e.g., Google, Facebook).
- `providerAccountId`: Unique identifier of the account within the provider's system.
- `refresh_token`, `access_token`, `expires_at`, `token_type`, `scope`, `id_token`, `session_state`: Authentication and authorization tokens and related information.

Relationship:

- `user`: One-to-one relationship with the `User` model, indicating the owner of the account.

---