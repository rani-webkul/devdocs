---
group: installation-guide
title: Install Magento using Composer
redirect_from:
  - guides/v2.2/install-gde/prereq/integrator_install.html
  - guides/v2.2/install-gde/prereq/integrator_install_composer.html
  - guides/v2.2/install-gde/prereq/integrator_install_ce.html
  - guides/v2.2/install-gde/prereq/integrator_install_ee.html
functional_areas:
  - Install
  - System
  - Setup
---

{% include install/composer-overview.md %}

## Prerequisites

Before you continue, you must do the following:

-  Set up a server that meets our [system requirements][]
-  Create the [Magento file system owner][]
-  [Install Composer][]{:target="_blank"}
-  Obtain [authentication keys][] for the Magento code repository

## Get the metapackage

To get the Magento metapackage:

1. Log in to your Magento server as, or switch to, the [Magento file system owner][].
1. Change to the web server docroot directory or a directory that you have configured as a virtual host docroot.
1. Create a new Composer project using the {{site.data.var.ce}} or {{site.data.var.ee}} metapackage.

    **{{site.data.var.ce}}**

    ```bash
    composer create-project --repository=https://repo.magento.com/ magento/project-community-edition:<version-tag> <install-directory-name>
    ```

    **{{site.data.var.ee}}**

    ```bash
    composer create-project --repository=https://repo.magento.com/ magento/project-enterprise-edition:<version-tag> <install-directory-name>
    ```

    When prompted, enter your Magento authentication keys. Public and private keys are created and configured in your [Magento Marketplace][].

    To install {{site.data.var.ce}} version 2.2.9 run in current folder:

    ```bash
    composer create-project --repository=https://repo.magento.com/ magento/project-community-edition:2.2.9 .
    ```

    If you encounter errors, such as `Could not find package...` or `...no matching package found`, make sure there are no typos in your command. If you still encounter errors, you may not be authorized to download {{site.data.var.ee}}. Contact [Magento support](https://magento.com/support) for help.

    See [troubleshooting][] for help with more errors.

## Set file permissions

You must set read-write permissions for the web server group before you install the Magento software. This is necessary so that the Setup Wizard and command line can write files to the Magento file system.

```terminal
cd /var/www/html/<magento install directory>
find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} +
find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} +
chown -R :www-data . # Ubuntu
chmod u+x bin/magento
```

## Install Magento

There are two options for installing Magento:

-  Command line
-  Web Setup Wizard

### Command line

This example assumes that the Magento install directory is named `magento2ee`, the `db-host` is on the same machine (`localhost`), and that the `db-name`, `db-user`, and `db-password` are all `magento`:

```bash
bin/magento setup:install \
--base-url=http://localhost/magento2ee \
--db-host=localhost \
--db-name=magento \
--db-user=magento \
--db-password=magento \
--backend-frontname=admin \
--admin-firstname=admin \
--admin-lastname=admin \
--admin-email=admin@admin.com \
--admin-user=admin \
--admin-password=admin123 \
--language=en_US \
--currency=USD \
--timezone=America/Chicago \
--use-rewrites=1
```

{: .bs-callout-info }
For `--backend-frontname` we recommend a random URI for security purposes. A random URI is harder for hackers or malicious software to exploit.

{:.bs-callout .bs-callout-tip}
For a full description of the CLI install options, refer to [Install the Magento software from the command line][].

### Web Setup Wizard

As an alternative to the CLI, use your browser to navigate to Magento's setup wizard:

```url
http://<Magento-host-or-IP>/<path-to-magento-root>/setup
```

For example: `http://localhost/magento2ee/setup`

{:.bs-callout .bs-callout-warning}
You cannot use the Web Setup Wizard if your docroot is set to the `pub/` directory. See [Modify docroot for security][].

<!-- Link Definitions -->
[Magento Marketplace]: https://marketplace.magento.com/customer/accessKeys/
[Modify docroot for security]: {{page.baseurl}}/install-gde/tutorials/change-docroot-to-pub.html
[Install the Magento software from the command line]: {{page.baseurl}}/install-gde/install/cli/install-cli-install.html#instgde-install-cli-magento
[troubleshooting]:{{page.baseurl}}/install-gde/trouble/tshoot_composer-fail.html
[Magento file system owner]: {{page.baseurl}}/install-gde/prereq/file-sys-perms-over.html
[authentication keys]: {{page.baseurl}}/install-gde/prereq/connect-auth.html
[Install Composer]: https://getcomposer.org/download/
[system requirements]: {{ page.baseurl }}/install-gde/system-requirements.html
[Magento file system owner]: {{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html
