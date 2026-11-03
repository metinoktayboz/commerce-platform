# 0001. Single repository with a Maven multi-module build

- Status: Accepted
- Date: 2026-10-29

## Context
commerce-platform will grow into several services (order, inventory, payment). We need to decide
how to organize them: one Maven multi-module build in a single repository, or independent Maven
projects (each with its own POM, wrapper and CI pipeline).

## Decision
Use one repository with a parent POM (inheriting `spring-boot-starter-parent`) and one module per
service. `order-service` is the first module; later services are added as sibling modules.

## Consequences
- Dependency and plugin versions are managed in one place; a framework upgrade (e.g. Spring Boot 4)
  is done once for all services.
- A single `./mvnw verify` builds and tests everything, and one CI workflow covers the repository.
- Services are coupled at build time: they share versions and are released together. A single
  module can still be built with `./mvnw -pl <module> -am verify`.
- Shared code goes into a `common` module only when there is a clear need, to avoid hidden coupling
  between services.
