# wp-staging-cli

**wp-staging-cli** is a high-performance command-line tool for processing WP Staging backup files. This tool allows you to extract, normalize, and inspect the contents of `.wpstg` backup files created by the WP Staging backup plugin.

This repo contains binary executables that can be used on WinOS, Linux and Mac OS to extract WP Staging backup files. 

**Important:** You can use this cli tool only with a valid [WP Staging Agency or Developer license key](https://wp-staging.com).

**Benchmarks:** 
- We extracted a 20GB backup in under 36 seconds on an AMD Ryzen™ 7 PRO 7840U with a fast SSD running Ubuntu 20.04.

## Features

- **Restore WordPress when its down**: Start this cli tool and instantly restore WordPress files and database, even when the site is unaccessable and broken.
- **Extract Backup Files and Database**: Access and extract the entire contents of `.wpstg` backup files without using WordPress.
- **Database Normalization**: Perform normalization on the database files within the backup.
- **Metadata Dumping**: Extract metadata from the backup file.
- **Index and Header Dumping**: Retrieve index and header information from the backup file.

## Installation

### Download Pre-Built Binary

1. Download executables for all major operating systems from [here](https://github.com/wp-staging/wp-staging-cli-releases/archive/refs/heads/main.zip).
2. Extract the zip and get the appropriate binary `wp-staging-cli` for your operating system from inside the `build` folder.
3. Optional: Move the `wp-staging-cli` binary to a directory in your `PATH` for easy access, e.g. for Linux:

```
mv wp-staging-cli /usr/local/bin/
```

## Usage

To run wp-staging-cli, use the following command:

```
wp-staging-cli [commands] [options] <backupfile.wpstg>
```

* **Commands** must be in the first order. When not specified, "extract" is used by default.
* **Options** and **Arguments** can be used in any order.
* **Options** can start with either a single "-" or a double "--".
* **Options** with values can be set with or without '='.

```
Commands:
  extract - Extract items from the backup. Default if no command is specified.
  restore - Restore the backup file.
  help    - Display all help message.

Arguments:
  backupfile.wpstg  - Path to the WP Staging backup file that will be processed. This argument is mandatory.

General Options:
  -l,  --license=<licensekey>       - WP Staging Pro License Key. Required to access the backup file.
                                      Alternatively, use the `WPSTGPRO_LICENSE` environment variable.
  -o,  --outputdir=<path>           - Specify the extraction directory path where processed files will be stored. Default: "./wp-staging-cli-output".
  -n,  --normalizedb                - Normalize database files during the `extract` process.
                                      This will replace all WP Staging specific placeholders and allows the sql file to be imported by
                                      any regular db admin tool.

       --workingdir=<path>          - Specify the working directory path where config-related files will be stored. Default: "~/.wp-staging-cli".
       --skip-config                - Don't reads command options from the configuration file located at "~/.wp-staging-cli/wp-staging-cli.conf".
       --siteurl=<siteurl>          - Specify a new Site URL.
       --db-prefix=<prefix>         - Specify a new database table prefix.
       --overwrite=<yes|no>         - Overwrite the target directory during `extract` and `restore` operations. Default: "yes".
       --verify                     - Verify the integrity of the extracted file.
       --yes                        - Automatically answers "yes" to confirmation prompts.
       --confirm-timeout=<num>      - Timeout duration (in seconds) for awaiting a "yes" response at confirmation prompts. Default: 30 seconds.
       --skip-extract               - Don't extract files and use previously extracted and existing files for `restore` process.
                                      For use case, when restore failed, the process can be continued without first extracting all files again.

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

  -d,  --debug                      - Display debug message.
  -q,  --quiet                      - Suppress output of processed backup items.
  -v,  --version                    - Display version information.
  -h,  --help                       - Display all help message.

Restore Options:
  -p,  --path=<path>                - Specify the WordPress root path for restoration. Default: "./".
  -wd, --overwrite-db=<yes|no>      - Remove database tables not present in the backup. Default: "yes".
  -wr, --overwrite-wproot=<yes|no>  - Remove files in the WordPress root path that are not in the backup or part of WordPress core. Default: "no".
       --db-innodb-strict-mode      - Enable InnoDB strict mode if needed. By default, it is turned off during database restoration.
       --db-file=<file>             - Use the extracted backup SQL file to resume database restoration in case of failure.
       --db-insert-batch-size=<num> - Number of queries to batch in a single insert operation. Default: 1000.
       --db-insert-multi=<yes|no>   - Use multi-row INSERT statements per query to improve performance. Default "yes".

Restore DB Options:
  This option overrides the DB-related configuration parsed from the wp-config.php file.
       --db-host=<string>           - Database Host.
       --db-name=<string>           - Database Name.
       --db-user=<string>           - Database User.
       --db-pass=<string>           - Database Password.
       --db-socket=<file>           - MySQL socket file path.
       --db-charset=<string>        - Database charset.
       --db-collate=<string>        - Database collate.
       --db-ssl-ca-cert=<file>      - SSL CA file path.
       --db-ssl-cert=<file>         - SSL certificate file path.
       --db-ssl-key=<file>          - SSL key file path.
       --db-ssl-mode=<mode>         - Connects to the database with SSL mode "skip-verify" or "preferred". Default: "skip-verify".
```

### Examples

```
wp-staging-cli extract --license=WPSTGPRO_LICENSE backupfile.wpstg
wp-staging-cli restore --license=WPSTGPRO_LICENSE backupfile.wpstg --path=/var/www/site
```

You may add the license key by using environment variable:

```
export WPSTGPRO_LICENSE=WPSTGPRO_LICENSE_KEY
```

At Windows OS command prompt

```
set WPSTGPRO_LICENSE=WPSTGPRO_LICENSE_KEY
```

#### Config File

By default, wp-staging-cli reads command options from the configuration file located at `~/.wp-staging-cli/wp-staging-cli.conf`.

```
# File: ~/.wp-staging-cli/wp-staging-cli.conf
--license=WPSTGPRO_LICENSE
--path=/path-to-restore
```

## Contributing
We welcome contributions to wp-staging-cli! Currently, we only accept bug reports and suggestions.

### How to Contribute
- If you have a bug report or suggestion, please open an [issue on the repository](https://github.com/wp-staging/wp-staging-cli-releases/issues).
- Pre-built binaries are available, and source contributions are currently not accepted.
- Review open issues before submitting to avoid duplicates.

## Acknowledgements
- [WP Staging Pro](https://wp-staging.com/) The Best WordPress Backup and Migration Plugin
- [Go Programming Language](https://go.dev/) The core language for this tool.
