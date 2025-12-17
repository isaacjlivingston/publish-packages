# Hello, DSB! (Developer Handbook)🚂

## Table of Contents
1. [Introduction](#introduction)
2. [Development Standards & Best Practices](#development-standards-best-practices)
3. [Tools & Technologies](#tools-technologies)
4. [Development Workflow](#development-workflow)
5. [Environment Setup](#environment-setup)
6. [CI/CD](#cicd)
7. [Testing Guidelines](#testing-guidelines)
8. [Security Practices](#security-practices)
9. [Documentation Standards](#documentation-standards)
10. [Collaboration & Communication](#collaboration-communication)
11. [Onboarding for New Developers](#onboarding-for-new-developers)
12. [Repository Conventions](#repository-conventions)
13. [Observability](#observability)
14. [Platform & Repo Lifecycle](#platform-repo-lifecycle)
15. [Change Log](#change-log)

---

## Introduction

Welcome! This handbook explains **how we work**, the **tools we use**, and the **standards we follow** so you can move fast with confidence.

- **[DSB IT Strategy](https://dsbintranet.sharepoint.com/sites/OekonomiITNewex/SitePages/DSB-IT-Strategy.aspx)**: High-level strategy and future digital platform
- **[Enterprise Architecture](https://confluence.dsb.dk/spaces/CIID/pages/1736730/DevOps)**: [IT Landscape](https://confluence.dsb.dk/spaces/EA/pages/240550170/Overarching+IT+Landscape), [IT Domains](https://confluence.dsb.dk/spaces/EA/pages/99812799/IT+Domains)
- **[DevOps](https://confluence.dsb.dk/spaces/CIID/pages/1736730/DevOps)**: Documentation on Developer tools (Ex. MAX)
- **[Getting started in IT (Danish)](https://dsbintranet.sharepoint.com/sites/IT-ServiceGodtigang/SitePages/Kom-Godt-Igang---Administrationen.aspx)**: Guide on getting setup with your computer, outlook, etc.
- **[Depo (Developer Portal)](https://depo-portal-ui-tooling.prd.tog.azure.dsb.dk/)**: Templates, system catalog, and more

**Where to ask questions:**
- **[DevOps Community](https://teams.microsoft.com/l/channel/19%3A9769a65d79d141d4ac63f51d684faa58%40thread.tacv2/DevOps%20Community%20and%20Support?groupId=c6d30580-c90f-46a3-931e-84c3212fb8a4&tenantId=f44c53ea-a4c3-499c-bf1e-a1891b565e1d)**: General development questions, especially about common tools (Jira, Confluence, Github)
- **[MAX Community](https://teams.microsoft.com/l/channel/19%3Ang6b40w9wshkgUGxVQXubU-lAB44t4lcXJR4ehN-8EA1%40thread.tacv2/MAX%20Community%20and%20Support?groupId=c6d30580-c90f-46a3-931e-84c3212fb8a4&tenantId=f44c53ea-a4c3-499c-bf1e-a1891b565e1d)**: Questions about MAX, our Kubernetes-based development platform
- **[Depo Community](https://teams.microsoft.com/l/channel/19%3AgOcYXPZansrMicDA__ic85C-izhZRyBoO-vPGbggv5c1%40thread.tacv2/Depo%20Community?groupId=a8f67344-6a5c-45b7-a9d2-2cb17e8eb8d5&tenantId=f44c53ea-a4c3-499c-bf1e-a1891b565e1d&ngc=true&allowXTenantAccess=true)**: Questions about Depo, our developer portal

---

## Development Standards & Best Practices

- **Language/Area specific style guides:**
  - **Java**: SalesComponents coding standards
  - **.Net**: Template for building dotnet services in MAX
  - **Next.js/React**: Used for dsb.dk development
  - **MAX Template**: Create MAX workloads and packages
  - *Is your language or area missing? Let us know in the comments!*

- **General guidelines:**
  - Prefer readability over cleverness
  - Keep commits small and focused
  - Use meaningful names; contextual logging
  - Fail fast and visibly

- **Security by default:**
  - See [Information Security Manual  - See [Information Security Manualfor DSB's full security requirements
  - Follow recommendations from code quality tools like Sonarqube
  - Use a Software Composition Analysis (SCA) tool

---

## Tools & Technologies

- **Version control:** GitHub (DSB org). Repositories are **private by default**. DSB employees get org-wide read access via the "everybody" team. External consultants get team-scoped access. "Internal" or **public** repos can be created on demand via the DevOps Team.

- **Key platforms:**
  - **MAX**: Standardized build/deploy/monitor platform (Kubernetes, microservices, DDD-inspired namespaces).  
    - MAX overview | MAX docs
  - **Sentinel Observability**: Prometheus + Grafana Stack + ClickHouse. See MAX Observability for more details.
  - **Depo**: Developer portal for finding and creating microservices/interfaces with templates.
  - **AI assistance**: GitHub Copilot (see internal docs for access).

---

## Development Workflow

- **Branching & Git hygiene:**
  - Default branch is `main`. If using Git-Flow, set `develop` as default and merge to `main` on release.
  - Prefer almost-linear history: short-lived branches + Pull Requests
  - Protect the default branch, rebase before merging, delete branches after merge
  - Merge to `main` to keep PR context discoverable

- **Recommended protection/settings:**
  - Require a Pull Request before merge
  - Require >1 approval
  - Disallow bypassing protections
  - Allow merge commits
  - Suggest updating PRs
  - Auto-delete head branches

- **Pull Requests:**
  - Keep PRs small and focused
  - Include rationale, testing notes, and screenshots for UI changes
  - Request at least one peer review from an owning team member

- **Use Jira to track development**

---

## Environment Setup

Each team has their own setup and language, so chat with your team.  
If you want to add a link to your team's guide, please let us know in the comments.

---

## CI/CD

- **GitHub Actions** is the default. Prefer internal runners (`@dsb-ubuntu-dind`) for network access and zero cost (install extra tools via actions).
- Cloud runners share 50,000 minutes/month; Mac runners cost 10× vs Linux—check with DevOps before using.
- Use concurrency groups to queue workflows and limit parallelism.
- **Pipelines & promotion:** If running on MAX, you can see your deployments on Sentinel.
- **Artifacts & images:** Can you add a link to the new container registry? (Contact: Søren Rindal Nielsen)

---

## Testing Guidelines

- **Unit tests** (fast, isolated) required for new code and critical paths.
- **Integration tests** across service/data-store boundaries. See Integration Testing-Integrationtesting) and technical details.
- **User Acceptance** tests the end-to-end business flow. See User Acceptance Testing.

---

## Security Practices

See Information Security Manual for DSB's full security requirements.

- **Secrets:** Store in approved secrets managers and never commit secrets.
- **Access:** Principle of least privilege; rotate keys; enforce 2FA.
- **Code & dependency scanning:** Sonarqube

---

## Documentation Standards

- Every repo must have a current **README.md** covering:
  - What it does, who develops/uses it
  - Where docs live
  - How CI/CD works (badges welcome)
  - Where it’s deployed

- Use Markdown.  
- Each project/team should also have a Confluence space.

---

## Collaboration & Communication

- **DevOps Hub**: Announcements about our development tools and a community for questions.
- **MAX**: Announcements and community.
- **Teams**: Select the domain (e.g., IT, Commercial), then the department.  
  - See all teams here
  - Commercial ARTs
  - DriftsART
- **Meeting etiquette:** Agenda-first, notes + action items

---

## Onboarding for New Developers

- **Accounts & groups:** Join AD group `GithubUsers` to receive your DSB GitHub invite. For GitHub Copilot, join `GitHubCopilotUsers`. Inactive users (no activity in 30 days / never used) are removed automatically.
- **Getting started in IT (Danish):** Guide
- Teams will have team-specific onboarding.

---

## Repository Conventions

- **Naming guidelines:**  
  Patterns:
  - `domain-boundedcontext` (e.g., `trafficinformation-passengerinformationdecorator`)
  - `domain-packageName` (e.g., `ticketing-fraud-detection`, `safety-optics`)
  - `stack-packageName` (e.g., `java-extensions`)
  - `platform-service` (e.g., `prometheus-configuration`, `github-sync`)
- Org admins may rename repos that don’t follow guidelines.

- **Teams & ownership:**  
  Use GitHub Teams to group repos, control write/merge rights, tag repos with team names, and ensure ownership beyond individuals.

---

## Observability

See MAX Observability for an overview of the observability platform.  
Configure alert and recording rules via the shared platform. For non-standard needs, use **Legacy-Exporter**.

---

## Platform & Repo Lifecycle

- Automated maintenance keeps GitHub tidy:
  - Repos with **no activity** archived after 2 years (unless topic `no-archive`)
  - Archived repos move to **cold storage** after 3 years (main branch history preserved; other branches dropped)
  - Empty repos deleted after 14 days
  - Short names (<8 chars) trigger issues
  - Teams without maintainers: System Team will locate an owner
  - Users removed from DSB AD: GitHub org access revoked

- **Cold storage** is a mono-repo; available topics:
  - `no-archive`: never archive this repo
  - `cold-storage`: move this repo to cold storage immediately

---

## Change Log

- **2025-11-18** – added link to AI Launchpad, Depo and MAX template
- **2025-11-17** — Removed unused sections, updated link to observability platform. Removed note at the top of the page
- **2025-10-03** — Cleaned up and removed dead links
- **2025-10-02** — Initial version created

---
