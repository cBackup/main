# Architecture

cBackup web interface is the application powered by Yii2 framework. Therefore [the official framework documentation](http://www.yiiframework.com/doc-2.0/) can be very useful if you would like to contribute to cBackup.

cBackup daemon is the Java application powered by Spring Framework.

# Developers' manifest

* **Project main language is English**;<br>please, keep all comments, commit messages and language strings in English.
* **Clean code**;<br>All code must be clear and clean. Big part of open source projects  indulge themselves in rapid development and messy code sins. We encourage you to write code as if your successor knows where do you live. Make you code beautiful and follow two principles:   
  * **KISS**<br>Keep It Simple and Stupid
  * **DRY**<br>Don't Repeat Yourself
* **Documentation matters**;<br>Keep all methods well-documented, write comments in unconventional code segments, accompanying documents for your commits to include them in official documentation later.
* **Yii:t() everything**<br>We are providing multilingual product. Please keep it up.

# Code conventions

* **Code must follow PSR-2 as close as possible**;<br>Don't be stingy on spaces and new lines. Well readable code saves hours of man hours. 
* **Take cue from [Yii2 coding standard](https://github.com/yiisoft/yii2/blob/master/docs/internals/core-code-style.md)**
  * Files MUST use either <?php or <?= tags
  * it MUST NOT use the other tag variations such as <?
  * There should be a newline at the end of file
  * Do not add trailing spaces to the end of the lines
  * Files MUST use only UTF-8 without BOM for PHP code
  * Code MUST use 4 spaces for indenting, not tabs
  * Class names MUST be declared in `StudlyCaps`
  * Class constants MUST be declared in all upper case with underscore separators
  * Method names MUST be declared in `camelCase`
  * Property names MUST be declared in `camelCase`
* **Database table names are singular**<br>E.g. `user`, `node`. The only exclusions are  many-to-many relations. M2M table should me named as `shedules_has_nodes`
* **Application components and namespaces should represent their roles and functionality**<br>E.g. `app\behaviors`, `app\helpers`. Try utilizing existing namespaces and folders.

# Translation

We use Transifex to keep our translation integrity. Also it's easy to add new language support with it's service. Feel free to join [cBackup on Transifex](https://www.transifex.com/cbackup/web-core/dashboard/) and contribute by adding, translating and maintaining new language.