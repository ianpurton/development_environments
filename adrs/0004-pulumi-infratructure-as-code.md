# 0004. Infratstructure as code solutions

Date: 31-08-2020

## Status

Accepted

## Context

Best practice for deploying micro service applications is to use infratstructure as code tooling. The aim is deploy the entire stack all from source code.

### Criteria

* Should work with our chosen cloud provider. (Digital Ocean)
* Easy to learn and use.
* For loops, functions and type safety where possible.
* Should handle secrets

### Considered Options

1. Terraform.
1. Pulumi.

## Decision

We chose Pulumi. https://www.pulumi.com/

Pulumi was easy to learn and we could use a language we already knew (Typescript). Terraform would require learning a new language.

Pulumi with Typescript fits in with our front end architecture as we are already using typescript for progressive enhancement on the front end.

## Consequences

We now have the entire infrastructure mapped as code.