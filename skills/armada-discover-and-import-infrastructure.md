---
name: Discover and import edge infrastructure
description: Run topology discovery on an Armada site and import the discovered compute/storage hardware into Bridge.
api: openapi/armada-orchestrator-openapi-original.yml
operations: [getDiscoveryType, discoverTopology, getDeviceDiscoveryStatus, getTopology, getAllImportInfra, importInfraPost, getAllComputeImportInfra, getAllStorageImportInfra]
---

# Discover and import edge infrastructure

Bring a new edge/data-center site's hardware under Bridge management.

## Auth
All calls require `Authorization: Bearer <JWT>` (admin role). See `authentication/armada-authentication.yml`.

## Steps
1. Check the discovery mode with `getDiscoveryType` (`GET /discoverytype`).
2. Kick off discovery with `discoverTopology` (`POST /device-discovery`).
3. Poll `getDeviceDiscoveryStatus` (`GET /device-discovery-status`) until discovery completes; read the mapped topology with `getTopology` (`GET /device-discovery`).
4. Review what is already imported with `getAllImportInfra` (`GET /infra/import`), split by `getAllComputeImportInfra` (`GET /infra/import/compute`) and `getAllStorageImportInfra` (`GET /infra/import/storage`).
5. Upload/import the discovered inventory with `importInfraPost` (`POST /infra/import/upload`).

## Errors
`400` (bad inventory payload), `401/403` (auth/RBAC), `500` (retry with backoff). See `errors/armada-problem-types.yml`.
