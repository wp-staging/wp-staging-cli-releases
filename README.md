# wp-staging-cli

**wp-staging-cli** is a high-performance command-line tool for processing WP Staging backup files. This tool allows you to extract, normalize, and inspect the contents of `.wpstg` backup files created by the WP Staging backup plugin.

This repo contains binary executables that can be used on WinOS, Linux and Mac OS to extract WP Staging backup files. (Requires a valid and active [WP Staging Agency or Developer plan](https://wp-staging.com).)

**Benchmarks:** 
- Extracting a 20GB backup in under 36s on a AMD Ryzen™ 7 PRO 7840U and fast SSD on Ubuntu 20.04.

## Features

- **Extract Backup Files and Database**: Access the contents of `.wpstg` backup files.
- **Database Normalization**: Perform normalization on the database files within the backup.
- **Metadata Dumping**: Extract metadata from the backup file.
- **Index and Header Dumping**: Retrieve index and header information from the backup file.

## Installation

### Download Pre-Built Binary

1. Download executables for all major operating systems from [here](https://github.com/wp-staging/wp-staging-cli-releases/archive/refs/heads/main.zip).
2. Extract the zip and get the appropriate binary for your operating system from the `build` folder.
3. Optional: Move the `wp-staging-cli` binary to a directory in your `PATH` for easy access, e.g. for Linux:

```
mv wp-staging-cli /usr/local/bin/
```

## Usage

To run wp-staging-cli, use the following command:

```
wp-staging-cli [options] <backupfile.wpstg>
```

### Arguments
- `<backupfile.wpstg>  - Path to the WP Staging backup file that will be processed. This argument is mandatory.`

### Options
```
Commands:
  extract - Extract items from the backup. Default if no command is specified.
  restore - Restore the backup file.

Arguments:
  backupfile.wpstg  - Path to the WP Staging backup file that will be processed. This argument is mandatory.

General Options:
  -l,  --license=<licensekey>       - WP Staging Pro License Key. Required to access the backup file.
                                      Alternatively, use the `WPSTGPRO_LICENSE` environment variable.

  -o,  --outputdir=<path>           - Specify the working directory path where processed files will be stored.
                                      The "wpstg-cli" will be appended to the specified path. Default: "./wpstg-cli".

  -e,  --extractdir=<string>        - Specify the name of the extraction directory. Default: "extract".
  -s,  --skip-confirm               - Skip confirmation prompt.
  -w,  --overwrite=<yes|no>         - Overwrite the target directory during `extract` and `restore` operations. Default: "yes".
  -v,  --version                    - Display version information and exit.
  -h,  --help=<all>                 - Display this help message and exit. Use 'all' to show additional help.
  -q,  --quiet                      - Suppress output of processed backup items.
  -d,  --debug                      - Display debug message.
       --slowdown-cpu               - Reduce CPU usage during the iteration process.
       --skip-extract               - Use existing extracted files during the `restore` process.

  -n,  --normalizedb                - Normalize database files during the `extract` process.
                                      This will replace all WP Staging specific placeholders and allows the sql file to be imported by
                                      any regular db admin tool.
       --siteurl=<siteurl>          - Specify a new Site URL.
       --dbprefix=<dbprefix>        - Specify a new database prefix.

  -or, --only-wproot                - Process only the 'wp root' item in the backup.
  -ow, --only-wpcontent             - Process only the 'wp-content' item in the backup.
  -op, --only-plugins               - Process only the 'plugins' item in the backup.
  -ot, --only-themes                - Process only the 'themes' item in the backup.
  -om, --only-muplugins             - Process only the 'mu-plugins' item in the backup.
  -ou, --only-uploads               - Process only the 'uploads' item in the backup.
  -ol, --only-languages             - Process only the 'languages' item in the backup.
  -od, --only-dbfile                - Process only the database file in the backup.
  -oe, --only-dropins               - Process only the dropins file in the backup.
  -of, --only-file=<string>         - Process only items that match the specified string.

  -sr, --skip-wproot                - Skip processing the 'wp root' item in the backup.
  -sw, --skip-wpcontent             - Skip processing the 'wp-content' item in the backup.
  -sp, --skip-plugins               - Skip processing the 'plugins' item in the backup.
  -st, --skip-themes                - Skip processing the 'themes' item in the backup.
  -sm, --skip-muplugins             - Skip processing the 'mu-plugins' item in the backup.
  -su, --skip-uploads               - Skip processing the 'uploads' item in the backup.
  -sl, --skip-languages             - Skip processing the 'languages' item in the backup.
  -sd, --skip-dbfile                - Skip processing the database file in the backup.
  -se, --skip-dropins               - Skip processing the dropins file in the backup.
  -sf, --skip-file=<string>         - Skip processing items that match the specified string.

  -dm, --dump-metadata              - Display backup metadata from the backup file.
  -di, --dump-index=<data>          - Display backup index from the backup file. Use 'data' to show additional information.
  -dh, --dump-header                - Display backup header from the backup file.
  -do, --dump-options               - Display the command options that have been parsed.

Restore Options:
  -p,  --path=<path>                - Specify the WordPress root path for restoration. Default: "./".
  -wd, --overwrite-db=<yes|no>      - Remove tables that are not in the backup. Default: "no".
  -wr, --overwrite-wproot=<yes|no>  - Remove files in the WordPress root path that are not in the backup or part of WordPress core. Default: "no".
       --dbinnodb-strict-mode       - Enable InnoDB strict mode if needed. By default, it is turned off during database restoration.
       --dbfile=<file>              - Use the extracted backup SQL file to resume database restoration in case of failure.

Restore DB Options:
  This option overrides the DB-related configuration parsed from the wp-config.php file.
       --dbhost=<string>            - Database Host.
       --dbname=<string>            - Database Name.
       --dbuser=<string>            - Database User.
       --dbpass=<string>            - Database Password.
       --dbcharset=<string>         - Database charset.
       --dbcollate=<string>         - Database collate.
       --dbssl-ca-cert=<file>       - SSL CA file path.
       --dbssl-cert=<file>          - SSL certificate file path.
       --dbssl-key=<file>           - SSL key file path.
       --dbssl-mode=<mode>          - Connects to the database with SSL mode skip-verify or preferred. Default: skip-verify.
```

### Examples

```
wp-staging-cli --license=WPSTGPRO_LICENSE --outputdir=./wpstgbackup backup.wpstg
wp-staging-cli --license=WPSTGPRO_LICENSE --normalizedb --dbprefix=newprefix --siteurl=https://example.com backup.wpstg
```

With short options:

```
wp-staging-cli -l WPSTGPRO_LICENSE -o ./wpstgbackup backup.wpstg
wp-staging-cli -l WPSTGPRO_LICENSE -n -dp newprefix -su https://example.com backup.wpstg
```

You may add the license key by using environment variable:

```
export WPSTGPRO_LICENSE=WPSTGPRO_LICENSE_KEY
```

At Windows OS command prompt

```
set WPSTGPRO_LICENSE=WPSTGPRO_LICENSE_KEY
```

## Contributing
We welcome contributions to wpstg-extractor! If you have suggestions, bug reports, or want to contribute code, please follow the [contributing guidelines.](https://github.com/wp-staging/wp-staging-pro)

### How to Contribute
1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Make your changes and test them.
4. Submit a pull request with a description of your changes.

## Acknowledgements
- [WP Staging Pro](https://wp-staging.com/) The Best WordPress Backup and Migration Plugin
- [Go Programming Language](https://go.dev/) The core language for this tool.

## Contact
For support or questions, please open an issue on the [GitHub repository](https://github.com/wp-staging/wp-staging-cli).

