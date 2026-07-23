---
name: Onboard a tenant on Armada Bridge
description: Create a tenant on the Bridge GPUaaS platform and establish its default resource quotas.
api: openapi/armada-orchestrator-openapi-original.yml
operations: [getTenants, createTenant, getDefaultQuotas, createDefaultQuotas, getMonetizeInfo, getSupportedCountries]
---

# Onboard a tenant on Armada Bridge

Provision a new tenant on the Bridge GPU cloud and set the quotas it starts with.

## Auth
All Orchestrator calls require `Authorization: Bearer <JWT>` (see `authentication/armada-authentication.yml`). Admin/platform role required.

## Steps
1. List existing tenants with `getTenants` (`GET /tenants`) to confirm the name is free — a duplicate returns `409 Conflict`.
2. (Optional) Check billing eligibility for the tenant's region with `getSupportedCountries` (`GET /monetize/countries`) and `getMonetizeInfo` (`POST /monetize`).
3. Create the tenant with `createTenant` (`POST /tenants`).
4. Read the platform default quotas with `getDefaultQuotas` (`GET /defaultquotas`); if none are set, create them with `createDefaultQuotas` (`POST /defaultquotas`).

## Errors
Handle `400` (malformed body), `401/403` (auth/RBAC), `409` (tenant already exists). See `errors/armada-problem-types.yml`.
