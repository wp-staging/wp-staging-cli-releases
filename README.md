# wpstg-extractor

The **wpstg-extractor** is a high-performance command-line tool for processing WP Staging Pro backup files. This tool allows you to extract, normalize, and inspect the contents of `.wpstg` backup files created by the WP Staging Pro plugin.

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

1. Download executables for all major operating systems from [here](https://github.com/wp-staging/wpstg-extractor-releases/archive/refs/heads/main.zip).
2. Extract the zip and get the appropriate binary for your operating system from the `build` folder.
3. Optional: Move the `wpstg-extractor` binary to a directory in your `PATH` for easy access, e.g. for Linux:

```
mv wpstg-extractor /usr/local/bin/
```

## Usage

To run wpstg-extractor, use the following command:

```
wpstg-extractor [options] <backupfile.wpstg>
```

### Arguments
- `<backupfile.wpstg>  - Path to the WP Staging backup file that will be processed. This argument is mandatory.`

### Options
```
  -l,  --license=<licensekey>   - WP Staging Pro License Key. Required for accessing the backup file.
  -o,  --outputdir=<directory>  - Specify the output directory where processed files will be stored.
                                  Default "./wpstgbackup" will be used.
  -s,  --slowdown-cpu           - Slow down CPU usage during the iteration process.
  -q,  --quiet                  - Do not show the extracted list.

  -n,  --normalizedb            - Perform database file normalization.
  -dp, --dbprefix=<dbprefix>    - Specify a new DB prefix to use with `--normalizedb`.
  -su, --siteurl=<siteurl>      - Specify a new Site URL to use with `--normalizedb`.

  -dm, --dump-metadata          - Display backup metadata from the backup file.
  -di, --dump-index             - Display backup index information from the backup file.
  -dh, --dump-header            - Display backup header information from the backup file.

  -or, --only-rootpath          - Extract the contents of the root path directory.
  -ow, --only-wpcontent         - Extract the contents of the 'wp-content' directory.
  -op, --only-plugins           - Extract the contents of the 'plugins' directory within 'wp-content'.
  -ot, --only-themes            - Extract the contents of the 'themes' directory within 'wp-content'.
  -om, --only-muplugins         - Extract the contents of the 'mu-plugins' directory within 'wp-content'.
  -ol, --only-languages         - Extract the contents of the 'languages' directory within 'wp-content'.
  -od, --only-dbfile            - Extract the database file from the specified location.
  -of, --only-file=<string>     - Extract the contents of files matching the specified string.
```

### Examples

```
wpstg-extractor --license=WPSTGPRO_LICENSE --outputdir=./wpstgbackup backup.wpstg
wpstg-extractor --license=WPSTGPRO_LICENSE --normalizedb --dbprefix=newprefix --siteurl=https://example.com backup.wpstg
```

With short options:

```
wpstg-extractor -l WPSTGPRO_LICENSE -o ./wpstgbackup backup.wpstg
wpstg-extractor -l WPSTGPRO_LICENSE -n -dp newprefix -su https://example.com backup.wpstg
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
For support or questions, please open an issue on the [GitHub repository](https://github.com/wp-staging/wpstg-extractor).

