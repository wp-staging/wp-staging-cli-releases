## v1.2.0

- Add multisite support.
- Add a command option to verify the checksum of the extracted file.
- Fix PHP serialization with indexed arrays.
- Fix data chunk calculation on compressed backups.
- Fix extraction when skipping the database file.
- Fix overwrite during restoration.
- Fix overwrite on the database and preserve the wp table from deletion.

## v1.1.0

- Add restore command.
- Add option to exclude files from extraction and restoration.
- Add option to overwrite wp root during restoration.
- Add option to remove tables that are not in the backup.
- Add option to dumping index with additional information.
- Fix extraction randomly failing on compressed backups.

## v1.0.3

- Refactor to wp-staging-cli.

## v1.0.2

- Fix progress output on win10 and later.

## v1.0.1

- Fix to build as static binary.

## v1.0.0

- Various fixes and enhancements.

## v0.0.0

- Initial release for internal use.