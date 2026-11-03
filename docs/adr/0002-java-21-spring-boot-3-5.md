# 0002. Java 21 and Spring Boot 3.5

- Status: Accepted
- Date: 2026-10-29

## Context
We need a Java and Spring Boot baseline. Most enterprise teams today run Java 21 (LTS) with
Spring Boot 3.x; Spring Boot 4.x (Spring Framework 7, Jackson 3) is current but adoption is
still early. Spring Boot 3.5 is the last 3.x minor; its open-source support ended on 2026-06-30
and 3.5.16 is the last OSS release. Only commercial support continues.

## Decision
Use Java 21 (LTS) and Spring Boot 3.5.16. Library versions come from the Spring Boot BOM without
overrides (e.g. Testcontainers 1.21.4, Flyway 11.7.2). PostgreSQL 17 is used because this
Flyway version predates PostgreSQL 18.

## Consequences
- The stack matches what most enterprise codebases run today.
- No more OSS patches for Spring Boot 3.5; dependency and security alerts are expected over time
  in this public repository.
- After the core phases, the project will be migrated to Spring Boot 4.x deliberately, recorded
  in its own ADR that supersedes this one.
