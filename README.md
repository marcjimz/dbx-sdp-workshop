# DBX SDP Workshop

Automated user provisioning and catalog management for Databricks workshops.

## Prerequisites

**IMPORTANT:** Before running the workshop, ensure a Delta Share has been created and shared in Databricks.

This workshop uses Databricks-to-Databricks Delta Sharing, which does not require credential files.

### Verify Delta Share Exists

Before running the notebook, verify your Delta Share is accessible:

```sql
-- Check providers
SHOW PROVIDERS;

-- Check shares
SHOW SHARES;

-- Verify specific share
DESCRIBE SHARE `your-provider`.`your-share`;
```

## Quick Start

1. Verify your Delta Share exists (see above)
2. Edit `config.yaml` with your Delta Share settings (provider, share name, schema, volume)
3. Update the user list with workshop participant email addresses
4. Run `notebooks/workshop_setup.ipynb` in Databricks

## What It Does

1. **Parse Users** - Converts comma-separated email list to aliases (first3_last4 from email)
2. **Mount Delta Share** - Mounts the pre-shared Delta Share to a local catalog
3. **Create Catalogs** - Generates user-specific catalogs: `{base_catalog}{alias}`
4. **Assign Permissions** - Grants CAN MANAGE to each user for their catalog
5. **Create Volumes** - Provisions volumes with consistent naming across catalogs
6. **Load Data** - Copies data from Delta Share volume to each user volume
7. **Generate Report** - Creates summary table with provisioning status

## Configuration

### config.yaml
Main configuration file with settings:
- User list (comma-separated email addresses)
- Delta Share provider and share name
- Catalog/schema/volume naming
- File glob pattern for copying files

**Delta Share Setup:**
- Provider identifier: Run `SHOW PROVIDERS;` in Databricks and use the **EXACT** value from the `name` column
  - Format: `cloud:region:type:identifier`
  - Example with name: `azure:eastus2:databricks:field-eng-east`
  - Example with UUID: `aws:us-west-2:1a2b3c4d-5e6f-7g8h-9i0j-1k2l3m4n5o6p`
- Share name: Run `SHOW SHARES;` in Databricks and use the exact value (e.g., `scp-demo`)

## Directory Structure

```
├── config.yaml              # Configuration
├── notebooks/
│   └── workshop_setup.ipynb # Main provisioning notebook
├── requirements.txt         # Python dependencies
└── data/                    # Source data files (optional)
```
