Quickly setup an Odoo 17 CE instance using docker for testing purposes

## Usage

To start the app run

```bash
docker compose up -d
```

## Updating instance

**Important notes:**

- Direct edits on standard views will be overwritten
- Custom inherited views, new manual views built from custom addons, customization from odoo studio will be preserved.

### 1. Create Backup

Always create a full backup from the database manager (db_dump + filestore) `http://<your-server-ip>:8069/web/database/manager` in case a rollback is necessary.

### 2. Pull latest image of odoo

On the docker-compose.yml directory, run:

```bash
docker compose pull odoo
```

### 3. Stop running container

Prevents active writes to the database during updating

```bash
docker compose stop odoo # (or caintainer name)
```

### 4. Run database upgrade command

Spins up a temporary container, isolated container to apply the changes to the database and gets removed upon compeltion.

```bash
docker compose run --rm odoo odoo -d your_database_name -u all --stop-after-init
```

### 5. Restart odoo instance

```bash
docker compose up -d odoo
```
