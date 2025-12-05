# DBX SDP Workshop

Automated user provisioning and catalog management for Databricks workshops.

## Quick Start

1. Edit `config.yaml` with your settings
2. Run `notebooks/workshop_setup.ipynb` in Databricks

## What It Does

1. **Parse Users** - Converts comma-separated user list to aliases (first3_last4)
2. **Configure Delta Share** - Sets up Delta Share recipient from config file
3. **Create Catalogs** - Generates user-specific catalogs: `{base_catalog}_{alias}`
4. **Assign Permissions** - Grants CAN MANAGE to each user for their catalog
5. **Create Volumes** - Provisions volumes with consistent naming across catalogs
6. **Load Data** - Copies data from source path to each volume
7. **Generate Report** - Creates summary table with provisioning status

## Configuration

All settings in `config.yaml`:
- User list (comma-separated names)
- Delta Share file path
- Catalog/schema/volume naming
- Data source location
- Dry run mode

## Directory Structure

```
├── config.yaml              # Configuration
├── notebooks/
│   └── workshop_setup.ipynb # Main provisioning notebook
└── data/                    # Source data files
```