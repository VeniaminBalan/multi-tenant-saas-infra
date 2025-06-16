# ✅ Multi-Tenancy Decisions

## 1. Tenant Identification

- Tenants are identified via the **URL path**:
  - Example: `todo.domain.com/{orgId}`, `app2.domain.com/{orgId}`
- `orgId` is parsed from the URL and used to route and secure requests per tenant.

---

## 2. Ingress & Routing

- Using **K3s** with **Traefik** as the ingress controller.
- Routing paths like:
  - `todo.domain.com/{orgId}` → React frontend
  - `todo-api.domain.com/api/{orgId}/...` → .NET Web API
- TLS termination is handled via wildcard or SAN certificates.

---

## 3. Identity Provider (Keycloak)

- Centralized **Keycloak** instance at `identity.domain.com`.
- Keycloak **Organizations** feature is used to model tenants.
- Organization memberships are included in JWT tokens via mappers.
- Backend validates:
  - Token signature & expiration
  - `orgId` in request matches `organizations` claim
  - User role (if needed)

---

## 4. Centralized Admin Panel

- Admin UI built with **.NET 9 Razor Pages**, hosted at `admin.domain.com`.
- Functions:
  - Create/manage organizations
  - Add users to orgs
  - Assign apps to orgs
  - Provision external apps via webhooks
- Data is stored in a centralized **PostgreSQL** database.

---

## 5. Backend Application Design

- Each backend app is multi-tenant aware:
  - Routes follow `/api/{orgId}/...`
  - Validates `orgId` against token
  - Loads tenant-specific DB config or connection string
- Support for shared or per-tenant databases.

---

## 6. Frontend Application Design

- Frontend apps accessed via `app.domain.com/{orgId}`.
- Bootstraps:
  - Parses `orgId` from URL
  - Logs in via Keycloak (PKCE)
  - Sends authenticated requests with token + `orgId` in path

---

## 7. Token & Claims Design

- Keycloak tokens contain:
  - `organizations` claim with membership info
  - Role info per organization
- Backend:
  - Decodes and verifies org membership
  - Checks scoped role-based access

---

## 8. Tenant Mapping & Provisioning

- Central Admin DB contains:
  - `Organizations` table: org ID, name, keycloak org ID
  - `Users`, `Applications`, `OrgAppLinks`
- Admin Panel provisions:
  - Org in Keycloak
  - Org-user memberships
  - Sends webhooks to apps to create org-specific resources

---

## 9. Security

- Strict backend validation:
  - Token signature
  - Org membership & roles
  - URL `orgId` must match token
- Ingress routes scoped to valid app + org paths

---

## 10. Future Improvements

- Use Redis to cache org config and permissions
- Automate provisioning with Keycloak Events
- Monitor per-org metrics & logs
- Add billing and rate-limiting features per organization

