# ams.project Stacks for ReadyStackGo — Preview Channel

Stack definitions for [ams.project](https://www.ams-erp.com/) by [ams.Solution AG](https://www.ams-erp.com/) — an enterprise project management system built on microservices.

> **Preview channel.** This repository holds **pinned, promoted** pre-release manifests
> for early customer deliveries (`X.Y.Z-preview.N`, images tagged `linux-vX.Y.Z-preview.N`).
> Previews are feature-incomplete previews of an upcoming version, **not for production**.
> When the version becomes feature-complete it moves to the
> [RC channel](https://github.com/Wiesenwischer/rsgo-ams-project-rc) (`*-rc`), then to the
> stable channel. The latest continuous-integration manifests live in the
> [CI channel](https://github.com/Wiesenwischer/rsgo-ams-project-ci) (`*-ci`).

## Usage

This repository is available as a stack source in [ReadyStackGo](https://github.com/Wiesenwischer/ReadyStackGo).
Add it during the setup wizard (**Stack Sources** step) or later under
**Settings → Stack Sources → Add → Git Repository**, using this repository's URL.

## Products

| Product | Description | Version | Stacks |
|---------|-------------|---------|--------|
| [ams.project](ams-project/4.0/) | Enterprise Project Management System | 4.0.0-preview.1 | 16 |
| [IdentityAccess](ams-identityaccess/3.2/) | Standalone Identity Provider | 3.2.0 | 1 |

> IdentityAccess ships at its own released version (`3.2.0`, `linux-v3.2.0`) — it is a
> separately versioned product and is **not** previewed together with ams.project.

### ams.project

Multi-stack product with Infrastructure, Platform, IdentityAccess and Business Services organized by bounded context:

- **Infrastructure** — EventStore, EventStoreDB, Redis
- **Platform** — Web BFF, Desktop Gateways, Admin Portal, Customer Documentation Portal
- **Business Services** — ProjectManagement, Discussions, Memo, SalesOrders, Export, ERP Integration, Capacity Planning, Production Planning, Reporting, Project Exporting, Project Import, Public API, Analytics, TaskContext

### ams.identityaccess

Standalone identity provider (IdentityServer / AdminPortal / ClientHub / EmailSender) that can be deployed independently of ams.project.

## Stack Format

Each product is organised **per minor version** (`ams-project/4.0/`, `ams-identityaccess/3.2/`), with a `stack.yaml` file in the [RSGO Manifest Format](https://github.com/Wiesenwischer/ReadyStackGo) in each version directory. Patch releases (e.g. 4.0.0 → 4.0.1) update the same directory; a new directory is added only for a new minor/major version. Multi-stack products use `include` references to organize sub-stacks.
