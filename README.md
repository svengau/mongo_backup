# Mongo Database backups

A project to backup MongoDB databases, using github actions, and store the backups in a GH release.

The database backups are created using the [mongo-backup](/blob/main/.github/workflows/_mongo_backup.yml) action.

It follows the [Grandfather-Father-Son](https://en.wikipedia.org/wiki/Backup_rotation_scheme#Grandfather-father-son) Backup strategy (GFS).

## Backups

All backups follows a naming convention of `backup-<type>-<id>` to ensure backup rotation.

Examples:

- `backup-hourly-23H`
- `backup-daily-01_Monday`
- `backup-weekly-31`
- `backup-monthly-10_October`
- `backup-yearly-2023`

### Backup types

- Daily: Daily backups are created at 23:05 every day.
- Hourly: Hourly backups are created at 00:05 every hour.
- Monthly: Monthly backups are created at 01:10 every first day of the month.
- Weekly: Weekly backups are created at 23:30 every Sunday.
- Yearly: Yearly backups are created at 23:20 every 31st of December.
- On demand: backup triggered manually by running the workflow.

## Installation

Simply fork this repository and add one secret to your repository: go to "Settings -> Secrets and variables -> Actions", and add the following secret:

- DATABASE_URL: Connection string to your MongoDB database

Enjoy!

## Limitations

- this works smoothly with small databases, but you may need a more standard backup strategy for larger databases.
- anyone with access to the reposity will be able to access the backups.
