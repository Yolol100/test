# Code and documentation samples

This repository contains selected samples from my original WordPress plugin, **ACF Page Text Manager**. It is intended for reviewing my code and documentation, not for installation as a complete plugin.

## Question 1 — Code sample

[PHP import processor (215 lines)](samples/class-import-processor.php)

This class processes previously prepared imports. It checks that the import plan belongs to the current user, verifies edit permissions, handles updates in batches, records errors and reports progress. It relies on other classes in the original plugin.

Original file: https://github.com/Yolol100/ACF-Text-Manager/blob/main/includes/Admin/Services/class-import-processor.php

## Question 2 — Documentation examples

- [Project README and usage guide](docs/PROJECT-README.md) — problem, functionality, setup, use, safety and verification
- [WordPress plugin documentation](docs/readme.txt) — detailed WordPress-facing instructions and release information
- [Changelog](docs/CHANGELOG.md) — maintenance and changes across versions

The full, working project can be found at https://github.com/Yolol100/ACF-Text-Manager.

**Source:** Original code and documentation by Andrew Baeten; copied here as portfolio samples. The documentation links back to the source where necessary.
