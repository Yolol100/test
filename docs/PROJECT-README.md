# ACF Page Text Manager

ACF Page Text Manager puts supported WordPress text fields in one admin screen. It covers page and post content, ACF fields, supported SEO metadata and image text. Editors can make individual changes or use CSV and Excel files for larger updates.

This guide has been rewritten for the review sample. It is based on the [original project documentation](https://github.com/Yolol100/ACF-Text-Manager/blob/3784555c4eccdc31afeb8cff0b6e38cd871effbb/README.md). The [PHP sample](../samples/class-import-processor.php) comes from that project, with English comments added. Its executable code and existing Dutch user messages are unchanged.

## Why this plugin exists

Related text can be spread across several WordPress screens. That makes a larger content update awkward to review. The plugin brings supported fields together and gives editors a way to move content into a spreadsheet and back.

It is a content editing tool, not a complete website migration tool. It does not support every field from every plugin.

## Getting started

Use the full plugin from the [original repository](https://github.com/Yolol100/ACF-Text-Manager), not this sample repository. Check the original release documentation for its WordPress, PHP and ACF requirements.

1. Make a backup and try the plugin on a staging copy first.
2. Install and activate the full plugin. Activate ACF for the ACF import and export workflow.
3. Open the plugin's text management screen in WordPress. The original menu label is `Tekstbeheer`.
4. Select a page or post and review the supported fields.
5. For a bulk update, export a small selection, edit the values and import the file again. Read any warnings and check the saved content before using a larger file.

Keep physical media filename changes off unless they are needed and have been tested. Changing a filename can affect image links. The full plugin has an extra opt-in control for this, and the import processor also checks for confirmation.

## Reading the code sample

Start with `Import_Processor::process()`. The method takes a token and loads a prepared plan. The file upload, column mapping and plan building happen elsewhere in the full plugin.

The processor checks that the plan exists, belongs to the current user and has not been explicitly blocked during preparation. It selects the next batch, checks permission for each item and applies the appropriate value rules before saving. ACF fields and special fields use separate update paths.

The plan keeps the cursor, update count and error messages between requests. On completion, the processor clears the content cache, deletes the temporary plan and returns a summary.

## Why it is built this way

**Separate preparation from writing.** Reading a spreadsheet and deciding which fields it refers to are different jobs from saving content. Keeping them apart makes each part easier to follow.

**Work in batches.** A request handles a limited number of updates rather than the whole import. This reduces work per request, but does not guarantee that a request cannot time out.

**Check access at the point of use.** Owning a plan does not automatically mean someone can edit every item in it. The processor checks each item. The full plugin's AJAX handler also checks its own permission and nonce before calling the controller.

**Do not treat every false return as a failed write.** ACF can return false when the saved value already matches the requested value. The processor reads the value back and compares it before reporting that case as an error. See the [ACF update_field reference](https://www.advancedcustomfields.com/resources/update_field/).

## Limits worth knowing

A completed import is not the same as an entirely successful import. Reported row failures are recorded and processing continues. Those rows are not automatically retried by this class. The progress percentage counts attempted updates, not successful writes, and the final response shows at most 20 warnings.

This is not an all-or-nothing transaction. Earlier writes remain when a later row fails. The sample does not lock concurrent requests or compare every current value with the value saved during preparation. It is not a promise of conflict-free editing or automatic recovery from every interruption.

## Checks before using it

On staging, check a normal update, an expired token, a plan owned by another user, an item the user cannot edit, and a media filename change without confirmation. Also try an unchanged ACF value and an import large enough to need several batches. Read the saved values and warnings, not just the progress bar.

These are suggested checks, not a report that they have all been run for this review copy. The original project's [compatibility workflow](https://github.com/Yolol100/ACF-Text-Manager/blob/3784555c4eccdc31afeb8cff0b6e38cd871effbb/.github/workflows/wordpress-compatibility.yml) checks syntax and WordPress loading. It is not a full import test suite.

## More detail

The [original WordPress documentation](readme.txt) and [release history](CHANGELOG.md) are preserved as source examples. Their version entries describe the original project, not new releases of this sample. The original project's [license](https://github.com/Yolol100/ACF-Text-Manager/blob/3784555c4eccdc31afeb8cff0b6e38cd871effbb/LICENSE) also applies to the copied plugin code.
