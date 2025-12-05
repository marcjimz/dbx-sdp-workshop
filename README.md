# DBX SDP Workshop

Automated user provisioning and catalog management for Databricks workshops.

## Quick Start

1. Edit `config.yaml` with your settings
2. Copy `config.share.example` to `config.share` and add your Delta Share credentials
3. Run `notebooks/workshop_setup.ipynb` in Databricks

## What It Does

1. **Parse Users** - Converts comma-separated email list to aliases (first3_last4 from email)
2. **Configure Delta Share** - Sets up Delta Share recipient from config file
3. **Create Catalogs** - Generates user-specific catalogs: `{base_catalog}_{alias}`
4. **Assign Permissions** - Grants CAN MANAGE to each user for their catalog
5. **Create Volumes** - Provisions volumes with consistent naming across catalogs
6. **Load Data** - Copies data from source path to each volume
7. **Generate Report** - Creates summary table with provisioning status

## Configuration

### config.yaml
Main configuration file with settings:
- User list (comma-separated email addresses)
- Catalog/schema/volume naming
- Data source location

### config.share
Delta Share recipient credentials file (provided after creating a Delta Share in Databricks):
- Bearer token
- Endpoint URL
- Expiration time

**Note:** `config.share` is gitignored - never commit credentials!

## Directory Structure

```
├── config.yaml              # Configuration
├── config.share.example     # Delta Share credentials template
├── notebooks/
│   └── workshop_setup.ipynb # Main provisioning notebook
└── data/                    # Source data files
```