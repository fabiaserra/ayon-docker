ayon-docker
===========

This is the official Docker-based deployment for the Ayon Server. 
Ayon is a robust tool designed to manage and automate workflows in the animation and visual effects industries.

The Docker image includes both:

- [ayon-backend](https://github.com/ynput/ayon-backend): The server backend
- [ayon-frontend](https://github.com/ynput/ayon-frontend): Web interface


Installation
------------

You can use the provided `docker-compose.yml` as a template to start your own deployment.

For more information on installation and user guides, 
please visit our [documentation website](https://ayon.ynput.io/docs/system_introduction).

### Demo projects

To help you get familiar with the interface, the `demo/` directory includes three demo project templates:

- `demo_Commercial`
- `demo_Big_Episodic`
- `demo_Big_Feature`

To deploy these demo projects to your server, run:

- `make demo` on Unix systems
- `manage.ps1` demo on Windows

*NOTE: These demo projects can take a while to create.*

## Postgres Setup

After initial deployment of the server, there may be additional manual steps required to ensure postgres extensions are
working properly. Specifically, if you see this error:

```log
ERROR:  operator class "public.gin_trgm_ops" does not exist for access method "gin"
```

You will need to connect to the database as the `postgres` user and run the following commands:

```shell
# Connect
psql -h <ayon-postgres-instance> -U postgres ayon
```

```SQL
CREATE EXTENSION IF NOT EXISTS "pg_trgm";
ALTER EXTENSION pg_trgm SET SCHEMA public;
```
