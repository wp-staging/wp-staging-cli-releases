# wpstg-extractor

The **wpstg-extractor** is a command-line tool for processing WP Staging Pro backup files. This tool allows you to extract, normalize, and inspect the contents of `.wpstg` backup files created by the WP Staging Pro plugin.

This repo contains binary executables that can be used on WinOS, Linux and Mac OS to extract WP Staging backup files. (Requires a valid and active [WP Staging Pro](https://wp-staging.com) license.)

## Features

- **Extract Backup Files**: Access the contents of `.wpstg` backup files.
- **Database Normalization**: Perform normalization on the database files within the backup.
- **Metadata Dumping**: Extract metadata from the backup file.
- **Index and Header Dumping**: Retrieve index and header information from the backup file.

## Installation

To use `wpstg-extractor`, you may download a pre-built binary from the [releases page](https://github.com/wp-staging/wpstg-extractor/releases) or build it from source if you have Go installed.

### Download Pre-Built Binary

1. Visit the [releases page](https://github.com/wp-staging/wpstg-extractor/releases).
2. Download the appropriate binary for your operating system.
3. Move the `wpstg-extractor` binary to a directory in your `PATH` for easy access:

```
mv wpstg-extractor /usr/local/bin/
```

### Build from Source

Clone the repository and build the binary:

```
git clone https://github.com/wp-staging/wpstg-extractor.git
cd wpstg-extractor
make build
```

Move the wpstg-extractor binary to a directory in your PATH for easy access:

```
mv ./build/linux_amd64/wpstg-extractor /usr/local/bin/
```

`make build` will build all the targeted architectures. To create a single one for your OS:
```
go build
```

To reduce the binary size:

```
go build -ldflags="-s -w"
```

Move the wpstg-extractor binary to a directory in your PATH for easy access:

```
mv ./wpstg-extractor /usr/local/bin/
```

## Usage

To run wpstg-extractor, use the following command:

```
wpstg-extractor <backupfile.wpstg> [options]
```

### Arguments
- `<backupfile.wpstg>`: Path to the WP Staging Pro backup file that will be processed. This argument is mandatory.

### Options
- `--license=<licensekey>`: WP Staging Pro License Key. Required for accessing the backup file.
- `--outputdir=<directory>`: Specify the output directory where processed files will be stored. The default is output.
- `--normalizedb`: Perform database file normalization.
- `--dbprefix=<dbprefix>`: Specify a new DB prefix to use during the normalization process.
- `--siteurl=<siteurl>`: Specify a new Site URL to use during DB normalization.
- `--dump-metadata`: Dump metadata from the backup file.
- `--dump-index`: Dump index information from the backup file.
- `--dump-header`: Dump header information from the backup file.

### Examples

```
wpstg-extractor backup.wpstg --license=WPSTGPRO_LICENSE_KEY
```

```
wpstg-extractor backup.wpstg --license=WPSTGPRO_LICENSE_KEY --outputdir=/tmp/wpstgbackup
```

```
wpstg-extractor backup.wpstg --license=WPSTGPRO_LICENSE_KEY --dump-metadata
```

```
wpstg-extractor backup.wpstg --license=WPSTGPRO_LICENSE_KEY --dump-index
```

```
wpstg-extractor backup.wpstg --license=WPSTGPRO_LICENSE_KEY --dump-header
```

```
wpstg-extractor backup.wpstg --license=WPSTGPRO_LICENSE_KEY \
--normalizedb --dbprefix=newprefix --siteurl=https://example.com
```

You may add the license key by using environment variable:

```
export WPSTGPRO_LICENSE=WPSTGPRO_LICENSE_KEY
```

## Contributing
We welcome contributions to wpstg-extractor! If you have suggestions, bug reports, or want to contribute code, please follow the [contributing guidelines.](https://github.com/wp-staging/wp-staging-pro)

### How to Contribute
1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Make your changes and test them.
4. Submit a pull request with a description of your changes.

## License
This project is licensed under the [Proprietary Software License Agreement](./LICENSE.md).

## Acknowledgements
- [WP Staging Pro](https://wp-staging.com/) The Best WordPress Backup and Migration Plugin
- [Go Programming Language](https://go.dev/) The core language for this tool.

## Contact
For support or questions, please open an issue on the [GitHub repository](https://github.com/wp-staging/wpstg-extractor).

