# Inventory Viewer

**Inventory Viewer** is a plugin for [NetBox](https://github.com/netbox-community/netbox) that displays modules (NetBox `dcim.Module` objects) in tables, grouped by their module types. This plugin is especially helpful if you need a quick overview of installed modules and their properties (like serial numbers, asset tags, location, cable connections, notes, and custom fields).

---

## Features

- **Grouped Module Tables**: Displays modules organized by module type on a dedicated page.
- **Custom Fields Integration**: Shows data from custom fields (e.g., “rok_zavedeni” or “merici_bod”) if present.
- **Cable Connections**: Prints out cable termination endpoints for each module, indicating how they’re connected.
- **Site & Location Overviews**: For each module, provides an at-a-glance view of where it resides (site, location, device).
- **Easy Navigation**: Integrated into NetBox’s main menu (under “Plugins”) for fast access to the module tables.

---

## Requirements

This plugin has been developed and tested on:

- **NetBox**: version `4.1.6`
- **Python**: version `3.10.12` or higher

While it may work on later NetBox versions, these are the ones used during development and testing. If you encounter any incompatibility, please open an issue.

---

## Installation

### Step 1: Install using pip

```bash
pip install inventory_viewer
```
### Step 2: Add the plugin into PLUGINS array in configuration.py
```bash
PLUGINS = [
    'inventory_viewer',
    # Other plugins...
]
```
### Step 3: Run netbox(for example)
```bash
python manage.py runserver
```

## Usage
### View Modules
1. In the NetBox main menu, find “Inventory Viewer” under the Plugins section.

2. The plugin automatically lists all modules in NetBox, grouped by module type (e.g., Silicom N5010, Silicom N6010, etc.).

3. Each module’s entry shows:
    - Serial (SN)
    - Custom Fields like “rok_zavedeni,” “merici_bod,” etc.
    - Asset Tag (Ev. č.)        
    - Location (site, location, device)
    - Cable Connections (includes connected interfaces or ports and where they lead)
    - Notes (comments field)

### Cable Connections
When a module is connected via front/rear ports or interfaces, the plugin displays a short summary describing each cable’s endpoints, for example:
```bash
DeviceA/Eth1 <-> DeviceB/Eth3
```
### Custom Fields
If your NetBox instance has custom fields like “rok_zavedeni” or “merici_bod” defined for the dcim.Module model, those values automatically appear as columns in the module table.

## Project Structure
```
inventory_viewer/
├── views.py               # Transfer and linking logic
├── templates/             # HTML templates
├── urls.py                # Plugin URLs
├── navigation.py          # Plugin menu entries
└── tables.py/             # Custom table
```

## Changelog
### v1.0
- Initial release: Displays modules grouped by module type in tables
- Shows cable connections, device location, and custom fields
- Integrates directly into NetBox’s plugin menu

## Notes
- Non-Intrusive: This plugin does not override NetBox’s core behavior or templates. It only adds new pages and logic within the plugin framework.

- Custom Fields: If you have not defined the custom fields (“rok_zavedeni”/“merici_bod”), you have to define them in your netbox instance, i tried to make this via python script but it didn't work. I defined rok_zavedeni as integer and merici_bod as text.

- Cable Data: The plugin relies on standard dcim.Module relationships (frontports, rearports, interfaces). If a module’s device or ports are not set properly, the cable connection info may appear incomplete.

## Author
Viktor Kubec  
BUT FIT Brno student  
MIT License  
GitHub: [vubeckubec/inventory_viewer](https://github.com/vubeckubec/inventory_viewer)  
PyPi: [inventory_viewer](https://pypi.org/project/inventory-viewer/1.0/) 
