!!! cite "Web setup"
    This process is maintained by wizard and contains of 5 steps. Every step is reversable, so you are able to go back manually or wizard will redirect you to the erroneous step giving you a chance to fix certain options.

## 1. Initialization

Basic system requirements are being checked. Installation process will be aborted if web-server is configured incorrectly and system files are world-accessible. You want to mark the `web` folder as wwwroot in your web-server configuration and make sure the folders and files on the level above are not visible.

## 2. Requirements check

During this step installer checks if all required PHP extensions and environmental systems are available (including Java runtime and Git). If any extensions are missing, don't hesitate to go back to SSH CLI on your server and setup missing stuff. Reload page to check if changes took effect. 

## 3. Acquire credentials

You will be prompted to enter database and system credentials, as well as path to your Git executable if installer is unable to find it aidless. Fill all form inputs and proceed.

## 4. Integrity check

All settings are being validated and set in the beginning of this step. Acquired data is saved to relevant files and database. Therefore the step might take some time to complete. When data is saved, the integrity check will be performed. If everything works as intended, you may proceed to final step and start working with cBackup.

Also all files and directories permissions will be checked. Look through if everything is set correctly. If necessary - fix it from the shell via `chmod` command. 

## 5. Finalizing

The final step removes all runtime installation data from the system and redirects you to the authentication page.
