# WordPress code and documentation samples

I'm Andrew Baeten. This repository contains a small part of my ACF Page Text Manager project and its documentation, collected here for review.

## Code sample

[Read the import processor](samples/class-import-processor.php) - 236 lines, including comments and blank lines.

The class applies prepared content updates in batches. It checks who owns the import, checks access to each item, saves values and reports progress and errors. The comments explain decisions that are not obvious from the method names alone.

This is an annotated copy of the [original 215-line file](https://github.com/Yolol100/ACF-Text-Manager/blob/3784555c4eccdc31afeb8cff0b6e38cd871effbb/includes/Admin/Services/class-import-processor.php). Only English comments were added. The executable PHP and existing Dutch user messages are unchanged.

## Documentation

Start with the [project guide](docs/PROJECT-README.md). It explains the problem, setup, import flow, code choices and limitations. This guide was rewritten for the review copy.

The [WordPress documentation](docs/readme.txt) and [changelog](docs/CHANGELOG.md) are preserved copies from the original project. Their release history belongs to that project, not this sample repository.

## What was checked

Both versions of the sample pass PHP 8.4 syntax checking. Their 1,281 executable tokens match after comments and whitespace are excluded. That confirms this annotation did not change the executable code. It does not prove that every import scenario works in WordPress; a full runtime test was not performed for this copy.

This repository is not an installable plugin. The sample needs WordPress, ACF and other classes from the [full project](https://github.com/Yolol100/ACF-Text-Manager). The original project's [license](https://github.com/Yolol100/ACF-Text-Manager/blob/3784555c4eccdc31afeb8cff0b6e38cd871effbb/LICENSE) applies to the copied plugin code.
