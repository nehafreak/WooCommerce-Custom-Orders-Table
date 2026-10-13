# WooCommerce Custom Orders Table

A WordPress plugin designed to improve WooCommerce order data storage by using a dedicated database table for commonly accessed order information. The plugin aims to reduce reliance on WordPress post meta and support more efficient database queries for WooCommerce stores.

## Overview

WooCommerce traditionally stores order information across WordPress posts and multiple post meta entries. As order volume increases, these records can contribute to database growth and make certain queries less efficient.

This plugin provides an alternative storage approach by consolidating commonly used order fields into a custom, indexed database table. It uses WooCommerce's CRUD architecture to manage order data and provides WP-CLI commands for migrating and restoring existing order information.

**Note:** Compatibility and performance depend on the plugin version, WooCommerce version, and store configuration. Test migrations on a staging site and maintain a database backup before making changes.

## Features

- Dedicated database table for commonly used WooCommerce order data
- Indexed storage designed to support efficient queries
- Integration with WooCommerce CRUD interfaces
- WP-CLI commands for order migration management
- Batch processing to help control memory usage
- Option to preserve original post meta during migration
- Backfill functionality to restore order data to post meta

## Requirements

- WordPress
- WooCommerce 3.5.1 or newer, as specified by the original project
- WP-CLI for command-line migration operations
- Database backup before migrating existing orders

Check the plugin code and current WooCommerce documentation to confirm compatibility with modern WooCommerce versions and High-Performance Order Storage (HPOS).

## Installation

1. Download or clone this repository.
2. Place the plugin folder inside `wp-content/plugins/`.
3. Activate the plugin from the WordPress admin dashboard.
4. Back up the database before migrating existing orders.
5. Use WP-CLI to inspect and migrate order data.

## Order Migration

The plugin provides WP-CLI commands for managing order data. Run these commands from your WordPress installation directory.

### Count orders awaiting migration

```bash
wp wc orders-table count
```

### Migrate order data

```bash
wp wc orders-table migrate
```

The migration command transfers supported order data from post meta into the custom orders table. Orders are processed in batches, with a default batch size of 100.

To specify a batch size:

```bash
wp wc orders-table migrate --batch-size=50
```

To preserve the original post meta during migration:

```bash
wp wc orders-table migrate --save-post-meta
```

Use `--batch-size=0` to disable batching, if supported by your installed version.

**Important:** Without the preservation option, the migration may delete the original post meta after successful processing. Always verify the implementation and back up your database before proceeding.

### Restore order data to post meta

```bash
wp wc orders-table backfill
```

The backfill command copies supported data from the custom orders table into the corresponding WordPress post meta fields. This may significantly increase the size of the post meta table.

## Development and Testing

Test the plugin in a staging environment before using it on a production store. Verify order creation, updates, checkout, reporting, extensions, and any integrations that depend on WooCommerce order storage.

## License

Refer to the repository's included license file for the applicable licensing terms.
