# DBX SDP Workshop

Automated user provisioning and catalog management for Databricks workshops.

## Prerequisites

**IMPORTANT:** Before running the workshop, ensure a Delta Share has been created and shared in Databricks.

This workshop uses Databricks-to-Databricks Delta Sharing, which does not require credential files.

## Quick Start

1. Edit `config.yaml` with your Delta Share settings (provider, share name, schema, volume)
2. Update the user list with workshop participant email addresses
3. Run `notebooks/workshop_setup.ipynb` in Databricks

## What It Does

1. **Parse Users** - Converts comma-separated email list to aliases (first3_last4 from email)
2. **Mount Delta Share** - Mounts the pre-shared Delta Share to a local catalog
3. **Create Catalogs** - Generates user-specific catalogs: `{base_catalog}_{alias}`
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
- Data source location (fallback)

**Delta Share Setup:**
- Provider identifier format: `cloud:region:provider:identifier`
- Example: `azure:eastus2:databricks:field-eng-east`
- Share name matches your Delta Share in Databricks

## Directory Structure

```
├── config.yaml              # Configuration
├── notebooks/
│   └── workshop_setup.ipynb # Main provisioning notebook
├── requirements.txt         # Python dependencies
└── data/                    # Source data files (optional)
```