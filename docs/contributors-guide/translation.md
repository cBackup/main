# Transifex

cBackup is built with i18n support and is ready to be translated to any language community requires. As long we are open source product, to maintain convenient way of translation we use [Transifex.com](https://www.transifex.com/cbackup/). We aprreciate any contribution, you don't need to program anything to provide, fix, improve or maintain translation.

# Development tools

To enchance and adjust Yii i18n functionality for Transifex usage, we changed behavior of several built-in commands. Due to slightly different format of message files backend is rewritten, but commands still do what is intended, so you can use `./yii message/extract` to parse sources and extract messages. Extended commands:

* `./yii message/source` generates 'en-US' language files used as a source for Transifex;
* `./yii message/find-duplicates en-US` looks in specified language folder (en-US by default) and displays if there're any duplicates in message sources in different categories. Please note, that in some case it's ok to have duplicates in different categories, because the same string can be translated in other way because of context.
