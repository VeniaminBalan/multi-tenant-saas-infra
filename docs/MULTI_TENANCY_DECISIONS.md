# Multi-Tenancy Decisions

## Tenant Identification
- Tenants will be identified by **subdomains** (e.g., `tenant1.yourapp.com`).
- A wildcard DNS record routes all tenant subdomains to the Kubernetes ingress controller.

## Tenant Mapping Storage
- Store tenant-to-subdomain mappings in a **shared relational database table**.
- The table includes tenant ID, name, subdomain, Keycloak realm, DB connection info, and metadata.
- This allows dynamic creation, update, and removal of tenants without cluster redeploy.

## Tenant Management
- Build a **custom admin panel** (.NET MVC) to:
  - Create and manage tenants.
  - Assign subdomains.
  - Configure Keycloak realms and related tenant settings.
  - Manage database connections or resource limits per tenant.

## Authentication & Authorization
- Use **Keycloak** with separate realms per tenant for isolation.
- Expose Keycloak via an ingress at a dedicated domain (e.g., `auth.yourapp.com`).
- Backend services will verify tenant identity and permissions based on the subdomain and Keycloak realm.

## Application Design
- Backend and frontend applications resolve the tenant context from the subdomain.
- Load tenant-specific configurations (e.g., DB connection strings, feature flags).
- Ensure security by validating tenant mappings strictly on each request.

## Routing & Ingress
- Traefik uses routing rules to forward tenant requests based on subdomains.
- Supports wildcard certificates for seamless SSL termination.

---

## Future Improvements
- Cache tenant mappings in-memory or in distributed cache (e.g., Redis) for performance.
- Implement tenant provisioning automation integrated with Keycloak and database setup.
- Monitor tenant resource usage for scaling and billing.
