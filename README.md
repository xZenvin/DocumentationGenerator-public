# DocumentationGenerator-public
A repository to host builds of my Documentation Generator tool, for everyone to use.

<p align="center">
<img alt="GitHub release (latest by date)" src="https://img.shields.io/github/v/release/xZenvin/DocumentationGenerator-public?label=latest%20release&logoColor=blue&style=for-the-badge">
<img alt="GitHub issues" src="https://img.shields.io/github/issues-raw/xZenvin/DocumentationGenerator-public?label=open%20issues&style=for-the-badge">
</p>

---

<p align="center">
Documentation and usage instructions can be found in this repository's <a href="https://github.com/xZenvin/DocumentationGenerator-public/wiki">Wiki</a>.
</p>

---

# Quick Start: Using the CLI
The CLI is the main way of interfacing with the DocGen, until the UI is in a working state. \
It can work completely off of command line arguments and thus is perfectly suited to be invoked by shell scripts automating CI. \
If no arguments are given, execution will be interactive and prompts will appear for filling in relevant parameters.

## `documentation`
The `documentation` command tells the executable to generate documentation files, based on the given parameters.

### Synopsis
```
documentation
  [-s|-settings <settings file path>]
  [-o|-output <output directory>]
  [-version <version>]
  [-p|-pause <true|false>]
  [-l <link repository file path>]
```
### Options
- `-s|-settings` (required) \
  The path given for this option must be a local file path pointing to a text file in JSON format.
  The file must contain a valid configuration for the documentation generator.
- `-o|-output` \
  If given a value, this will override the `Output:BaseDirectory` specified in the [Generation Settings](https://github.com/xZenvin/DocumentationGenerator-public/wiki/GenerationSettings#outputsettings).
- `-version` \
  If given a value, this will overwrite the `Input.Version` specified in the generation settings.
- `-p|-pause` \
  If set to `true`, the console will wait for user input after the process has finished or failed.
  This defaults to `false` and is mainly meant for debugging purposes.
- `-l` \
  If given a value, this will override the `Input:LinkRepository` specified in the [Generation Settings](https://github.com/xZenvin/DocumentationGenerator-public/wiki/GenerationSettings#inputsettings). \
  *(Release `pre-0.0.2+`)*
  
## `links`
The `links` command allows creating a link repository file that can be used in future generation processes to eliminate the need for link prompts.
  
### Synopsis
```
links
  [-s|-settings <settings file path>]
  [-o|-output <output file path>]
  [-v|-validate <true|false>]
  [-p|-pause <true|false>]
```

### Options
- `-s|-settings` (required)\
  The path given for this option must be a local file path pointing to a text file in JSON format.
  The file must contain a valid configuration for the documentation generator.
- `-o|-output` (required)\
  The path of the output link repository file. This must be a valid file path.
  The file extension will automatically be changed to `.zdlr`.
- `-v|-validate` \
  If set to `true`, given links will be validated via web request, and a verification prompt will be given if the request returned an error. \
  This defaults to `false`.
- `-p|-pause` \
  If set to `true`, the console will wait for user input after the process has finished or failed.
  This defaults to `false` and is mainly meant for debugging purposes.

## Exit Codes
Below is a table of exit codes that the CLI may return after finishing or failing, and their respective meanings.
| Code | Reason |
|-----:|:-------|
|0     | The process finished without errors. |
|-1    | The process failed due to an internal error of the generator. |
|-2    | The process name given was invalid. |
|-3    | The number of arguments given was invalid. |
|-4    | The Settings file provided via the `-s\|-settings` option did not exist or could not be parsed. |
|-5    | The output path was invalid so that the generation result could not be written. |
