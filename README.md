# Multi-Tenant SaaS Infrastructure on Hetzner + K3s + Keycloak + .NET

This repository contains infrastructure and architectural decisions, code, and configuration examples for building a multi-tenant SaaS platform on Hetzner VPS using:

- K3s (Lightweight Kubernetes)
- Traefik ingress controller with wildcard subdomains
- Keycloak for authentication and tenant realm management
- Admin Panel for tenant management
- Multi-tenant backend and frontend applications


## Project Goals

- **Build a scalable and cost-effective Kubernetes infrastructure** on Hetzner VPS using K3s.
- **Implement multi-tenancy using subdomain routing**, enabling tenant isolation and easy management.
- **Deploy Keycloak** for secure and flexible tenant authentication with realm separation.
- **Develop a custom admin panel** for creating and managing tenants dynamically.
- **Demonstrate multi-tenant backend and frontend applications** that consume tenant context and integrate with Keycloak.
- **Test infrastructure scalability and resilience** through stress testing and monitoring.
- **Document best practices and architectural decisions** for multi-tenant SaaS on self-managed Kubernetes.

---

## Repo Contents

- `docs/INFRASTRUCTURE_DECISIONS.md` - Infrastructure setup and Kubernetes cluster decisions.
- `docs/MULTI_TENANCY_DECISIONS.md` - Multi-tenancy design, tenant management, and routing strategies.
- Additional folders for Helm charts, manifests, and source code (TBD).

---

## Getting Started

1. Provision Hetzner VPS servers.
2. Install K3s and set up the Kubernetes cluster.
3. Configure Traefik ingress with wildcard DNS.
4. Deploy Keycloak with tenant realms.
5. Deploy custom tenant management admin panel.
6. Deploy multi-tenant backend and frontend applications.

---
