---
name: Inspect platform capacity and catalog
description: Read Bridge platform capacity, dashboard stats, available flavours, and the deployable service catalog before provisioning.
api: openapi/armada-orchestrator-openapi-original.yml
operations: [getDashboardStats, getTotalCapacity, getCatalog, getMetalFlavours, getVMFlavours, getVGPUFlavours, getOsImages, getClusterVersions, getCapabilities]
---

# Inspect platform capacity and catalog

Before provisioning clusters or VMs, read what the platform can offer.

## Auth
All calls require `Authorization: Bearer <JWT>`. See `authentication/armada-authentication.yml`.

## Steps
1. Read overall utilization with `getDashboardStats` (`GET /dashboard`) and `getTotalCapacity` (`GET /totalcapacity`).
2. Enumerate deployable services with `getCatalog` (`GET /catalog`) and platform features with `getCapabilities` (`GET /features`).
3. List hardware options: `getMetalFlavours` (`GET /metal/flavour`), `getVMFlavours` (`GET /vms/flavour`), `getVGPUFlavours` (`GET /vms/vgpu-flavours`), and OS images `getOsImages` (`GET /osimages`).
4. Check supported Kubernetes cluster versions with `getClusterVersions` (`GET /clusters/versions`).

## Errors
`401/403` (auth/RBAC), `500` (retry). See `errors/armada-problem-types.yml`.
