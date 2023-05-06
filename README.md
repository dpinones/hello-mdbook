# How to deploy and work with this little example

## Setup

To build the current repo content, several packages are required.

1. Rust related packages:
    * cargo must be installed (install [rustup](https://rustup.rs/) if not already done).
    * install the following package with cargo: `cargo install mdbook mdbook-i18n-helpers`
2. Host packages:
    * gettext package for translations: `sudo apt install gettext`

## Build

To build the book, just use `mdbook build` being at the root of this repository.
This will generate the content into `./book` folder.

The most important file to build is the `SUMMARY.md`, which is giving `mdbook` the information
of which files must be included.

Also, all the information related to the extra files to be included can be found in the
`book.toml` configuration file.

## Translations

This book is targetting international audience, and we inspired our work from [Google repos](https://github.com/google/comprehensive-rust).
Please refer to [this page](https://github.com/google/comprehensive-rust/blob/5bbb68be2cee0f2ee1b5be96c97e5a6aad385b1f/TRANSLATIONS.md) for the original documentation. In this documentation details can be found to build translations and add new ones.

Basically, each translation can be found in a `.po` file where the translators only have to translate chunk of texts
extracted by the `gettext` tools.

**All files in the `src` directory MUST be written in english**. Then all the translation files can be
generated and updated with few commands.

When english text is changed, those are the step to merge the new content:

1. Rebuild the `messages.pot`:
   `MDBOOK_OUTPUT='{"xgettext": {"pot-file": "messages.pot"}}' mdbook build -d po`

2. Merge the changes, where unchanged messages are intact, deleted message are marked as old, and the updated messaged
   marked as fuzzy and must be updated before removing the marker.
   `msgmerge --update po/xx.po po/messages.pot`
