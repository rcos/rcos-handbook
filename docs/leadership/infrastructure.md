# RCOS Infrastructure

Over a handful of semesters, different cohorts of Coordinators have gradually designed, developed, deployed, forgotten, redesigned, redeveloped, redeployed, and reforgotten RCOS infrastructure. This documentation exists to try to end that cycle.

## RCOS Accounts & Passwords

It is imperative that RCOS infrastructure and social media accounts are always accessible to Coordinators and Faculty Advisors from a secure, centralized location. We currently use [BitWarden](https://vault.bitwarden.com/#/vault) for this.

### Access to BitWarden Vault

Coordinators must be securely sent the username and password combination to the BitWarden account upon becoming a Coordinator. This account grants access to all other RCOS accounts so naturally it must be kept extremely secure.

### New RCOS Accounts

Coordinators in the past used personal accounts for RCOS infrastructure. Once they graduated, succeeding Coordinators lost access and sometimes even knowledge of those important accounts. Therefore, it is imperative that **personal accounts are NEVER used for RCOS infrastructure or social media** but instead use the `rcos.management@gmail.com` email and are added to the RCOS BitWarden vault.

## RCOS Cloud

We have an RCOS DigitalOcean account (details are in the BitWarden) and a "RCOS" project within that account. We use two features, [Droplets](https://www.digitalocean.com/products/droplets/) and [Database Clusters](https://www.digitalocean.com/products/managed-databases/).

### RCOS Droplet

The droplet is simply a server running Debian 10 (buster) with a couple of services running on it. This server uses Caddy and Docker to run Telescope (see RCOS Website below) and Hasura (see RCOS Database below).

To connect via SSH to the server (only do this if absolutely necessary!) use:

```
ssh <username>@<ip>
```

Where the values for `<username>`, `<ip>`, and the password you will be prompted for are in the BitWarden under "DigitalOcean Droplet (Debian Server)" or similar.

### Database Cluster

The managed database cluster runs PostgresQL 12 and is automatically updated and configured by DigitalOcean! Convenient! No outside connections to the database are allowed, and any modification to data should be done through Hasura (see RCOS Database below).

## RCOS Website - rcos.io

The [RCOS website](https://rcos.io) is now run using [Telescope](https://github.com/rcos/Telescope/). More documentation will be added here as more features are added to Telescope.

## RCOS Database API - Hasura

We run [Hasura](https://hasura.io/) on our Droplet to provide a fully-functional GraphQL API for the Postgres database. It's pretty darn cool. This GraphQL API serves as the gateway to the database. All clients such as rcos.io, automation scripts, and more can only interact with RCOS data via the Hasura API and can never directly connect to the database.

To open the Hasura console, install the [Hasura CLI](https://hasura.io/docs/latest/hasura-cli/install-hasura-cli/) clone the [rcos-data](https://github.com/rcos/rcos-data) repository, and run inside it:

```sh
hasura console --admin-secret xxxxxxxxxxxxxxxxxxxxxxxx
```

Where the admin secret is the "Hasura Admin Secret" from the [RCOS Leadership Bitwarden](../passwords). This gives you a playground to view and edit data directly or through custom GraphQL queries you write.

## Updating Infrastructure

1. SSH into the DigitalOcean droplet using the instructions above.
2. Pull the latest `rcos-data` repository updates, e.g. `cd rcos-data && git pull origin main`
3. Restart docker containers with `docker-compose down && docker-compose up -d`
