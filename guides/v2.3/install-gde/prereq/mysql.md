---
group: installation-guide
subgroup: Prerequisites
title: MySQL
menu_title: MySQL
menu_order: 25
---

## Help if you're just starting out {#mysql-help-beginner}

If you're new to all this and need some help getting started, we suggest the following:

*	[Is the Magento software installed already?]({{page.baseurl }}/install-gde/basics/basics_magento-installed.html)
*	[What is the software that the Magento server needs to run?]({{page.baseurl }}/install-gde/basics/basics_software.html)
*	[What operating system is my server running?]({{page.baseurl }}/install-gde/basics/basics_os-version.html)
*	[How do I log in to my Magento server using a terminal, command prompt, or SSH?]({{page.baseurl }}/install-gde/basics/basics_login.html)

## General guidelines {#instgde-prereq-mysql-intro}

{:.bs-callout .bs-callout-info}
The Magento application requires MySQL 5.6.x. Magento versions 2.1.2 and later are compatible with MySQL 5.7.x. Magento is also compatible with MySQL NDB Cluster 7.4.\*, MariaDB 10.0, 10.1, 10.2, Percona 5.7 and other binary compatible MySQL technologies.

Magento _strongly_ recommends you observe the following standard when you set up your Magento database:

*	Magento uses [MySQL database triggers](http://dev.mysql.com/doc/refman/5.0/en/triggers.html){:target="_blank"} to improve database access during reindexing. Magento does not support any custom triggers in the Magento database because custom triggers can introduce incompatibilities with future Magento versions.
*	Familiarize yourself with [these potential MySQL trigger limitations](http://dev.mysql.com/doc/mysql-reslimits-excerpt/5.1/en/stored-program-restrictions.html){:target="_blank"} before you continue.
*	If you use MySQL database replication, be aware that Magento does _not_ support MySQL statement-based replication. Make sure you use _only_ [row-based replication](http://dev.mysql.com/doc/refman/5.1/en/replication-formats.html){:target="_blank"}.

{:.bs-callout .bs-callout-warning}
Magento 2 currently utilizes `CREATE TEMPORARY TABLE` statements inside transactions, which are [incompatible](https://dev.mysql.com/doc/refman/5.7/en/replication-gtids-restrictions.html) with database implementations utilizing GTID-based replication, such as [Google Cloud SQL second-generation instances](https://cloud.google.com/sql/docs/features#differences).

{:.bs-callout .bs-callout-info}
If your web server and database server are on different hosts, perform the tasks discussed in this topic on the database server host then see [Set up a remote MySQL database connection]({{page.baseurl }}/install-gde/prereq/mysql_remote.html).

## Installing MySQL on Ubuntu {#instgde-prereq-mysql-ubuntu}

See one of the following sections for more information:

*	[Installing and configuring MySQL 5.7 on Ubuntu 16](#instgde-prereq-mysql57-ub16)
*	[Installing MySQL 5.6 on Ubuntu 14](#instgde-prereq-mysql56ubu14)
*	[Installing MySQL 5.6 on Ubuntu 12](#instgde-prereq-mysql56ubu12)

### Installing and configuring MySQL 5.7 on Ubuntu 16 {#instgde-prereq-mysql57-ub16}

This section discusses how to install MySQL 5.7 on Ubuntu 16.

{:.bs-callout .bs-callout-info}
The Magento application 2.1.2 and later are compatible with MySQL 5.7.

To install MySQL 5.7 on Ubuntu 16:

1.	Enter this command:

		sudo apt install -y mysql-server mysql-client

2. Start MySQL:

        sudo service mysql start

3.	Secure the installation:

		sudo mysql_secure_installation

4.	Test the installation:

		mysql -u root -p

	Sample output:

		Welcome to the MySQL monitor.  Commands end with ; or \g.
		Your MySQL connection id is 45
		Server version: 5.6.19-0ubuntu0.14.04.1 (Ubuntu)

		Copyright (c) 2000, 2014, Oracle and/or its affiliates. All rights reserved.

		Oracle is a registered trademark of Oracle Corporation and/or its
		affiliates. Other names may be trademarks of their respective
		owners.

		Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

		mysql>

5.	If you expect to import large numbers of products into Magento, you can increase the value for [`max_allowed_packet`](http://dev.mysql.com/doc/refman/5.6/en/program-variables.html){:target="_blank"} that is larger than the default, 16MB.

	{% include install/mysql_max-allowed-packet-ubuntu.md %}

6.	[Configure the Magento database instance](#instgde-prereq-mysql-config).

### Installing MySQL 5.6 on Ubuntu 14 {#instgde-prereq-mysql56ubu14}

To install MySQL 5.6 on Ubuntu 14:

1.	Enter this command:

		apt-get -y install mysql-server-5.6 mysql-client-5.6

2. Start MySQL:

        sudo service mysql start

3.	Secure the installation:

		mysql_secure_installation

4.	Test the installation by entering the following command:

		mysql -u root -p

	Sample output:

		Welcome to the MySQL monitor.  Commands end with ; or \g.
		Your MySQL connection id is 45
		Server version: 5.6.19-0ubuntu0.14.04.1 (Ubuntu)

		Copyright (c) 2000, 2014, Oracle and/or its affiliates. All rights reserved.

		Oracle is a registered trademark of Oracle Corporation and/or its
		affiliates. Other names may be trademarks of their respective
		owners.

		Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

		mysql>

5.	If you expect to import large numbers of products into Magento, you can increase the value for [`max_allowed_packet`](http://dev.mysql.com/doc/refman/5.6/en/program-variables.html){:target="_blank"} that is larger than the default, 16MB.

	{% include install/mysql_max-allowed-packet-ubuntu.md %}

6.	[Configure the Magento database instance](#instgde-prereq-mysql-config).

### Installing MySQL 5.6 on Ubuntu 12 {#instgde-prereq-mysql56ubu12}

To install MySQL 5.6 on Ubuntu 12, use the following instructions from [askubuntu.com](http://askubuntu.com/questions/433014/unable-to-install-mysql-5-6-in-ubuntu-12-04){:target="_blank"}.

1.	Enter the following commands in the order shown:

		apt-get -y update
		apt-add-repository ppa:ondrej/mysql-5.6
		apt-get -y update
		apt-get -y install mysql-server

2. Start MySQL:

        sudo service mysql start

3.	Secure the installation:

		mysql_secure_installation

4.	Test the installation:

		mysql -u root -p

	Messages similar to the following display:

		Welcome to the MySQL monitor.  Commands end with ; or \g.
		Your MySQL connection id is 43
		Server version: 5.6.21-1+deb.sury.org~precise+1 (Ubuntu)

		Copyright (c) 2000, 2014, Oracle and/or its affiliates. All rights reserved.

		Oracle is a registered trademark of Oracle Corporation and/or its
		affiliates. Other names may be trademarks of their respective
		owners.

		Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

		mysql>

5.	If you expect to import large numbers of products into Magento, you can increase the value for [`max_allowed_packet`](http://dev.mysql.com/doc/refman/5.6/en/program-variables.html){:target="_blank"} that is larger than the default, 16MB.

	{% include install/mysql_max-allowed-packet-ubuntu.md %}

6.	[Configure the Magento database instance](#instgde-prereq-mysql-config).

## Installing and configuring MySQL 5.7 on CentOS {#instgde-prereq-mysql57-centos}

This section discusses how to install MySQL 5.7 on CentOS 6 or CentOS 7.

{:.bs-callout .bs-callout-info}
The Magento application 2.1.2 and later are compatible with MySQL 5.7.

### Get MySQL 5.7 for CentOS 7

The following procedure is based on [How to Install Latest MySQL 5.7.9 on RHEL/CentOS 7/6/5 and Fedora 23/22/21](http://www.tecmint.com/install-latest-mysql-on-rhel-centos-and-fedora){:target="_blank"}.

As a user with `root` privileges, enter the following commands in the order shown:

	wget http://dev.mysql.com/get/mysql57-community-release-el7-7.noarch.rpm
	yum -y localinstall mysql57-community-release-el7-7.noarch.rpm

Continue with [Install and configure MySQL 5.7 on CentOS 6 or 7](#mysql57-centos-config).

### Get MySQL 5.7 for CentOS 6

The following procedure is based on [How to Install Latest MySQL 5.7.9 on RHEL/CentOS 7/6/5 and Fedora 23/22/21](http://www.tecmint.com/install-latest-mysql-on-rhel-centos-and-fedora){:target="_blank"}.

As a user with `root` privileges, enter the following commands in the order shown:

	wget http://dev.mysql.com/get/mysql57-community-release-el6-7.noarch.rpm
	yum -y localinstall mysql57-community-release-el6-7.noarch.rpm

Continue with the next section.

### Install and configure MySQL 5.7 on CentOS 6 or 7 {#mysql57-centos-config}

1.	Enter the following commands in the order shown:

		yum -y install mysql-community-server
		service mysqld start

2.	Verify the version:

		mysql --version

	Sample output follows:

		mysql  Ver 14.14 Distrib 5.7.12, for Linux (x86_64) using  EditLine wrapper

3.	Get the temporary database `root` user password:

		grep 'temporary password' /var/log/mysqld.log
4.	Secure the installation:

		mysql_secure_installation

	Follow the prompts on your screen to set a new password and configure other options.
5.	Configure MySQL 5.7 as discussed in [Configuring the Magento database instance](#instgde-prereq-mysql-config).

## Installing and configuring MySQL 5.6 on CentOS {#instgde-prereq-mysql-centos}

The following procedure is based on [Install MySQL Server 5.6 in CentOS 6.x and Red Hat 6.x Linux](http://sharadchhetri.com/2013/12/26/install-mysql-server-5-6-in-centos-6-x-and-red-hat-6-x-linux/){:target="_blank"}.

1.	*CentOS 6* Install the MySQL database:

		yum -y update
		sudo wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm && sudo rpm -ivh mysql-community-release-el6-5.noarch.rpm
		sudo yum -y install mysql-server

2.	*CentOS 7* Install the MySQL database:

		yum -y update
		sudo wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm && sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
		sudo yum -y install mysql-server

2.	Start MySQL:

		service mysqld start

3.	Set a password for the <tt>root</tt> user and set other security-related options. Enter the following command and follow the prompts on your screen to complete the configuration:

		mysql_secure_installation

4.	Verify the MySQL server version:

		mysql -u root -p

	Messages similar to the following display:

		Welcome to the MySQL monitor.  Commands end with ; or \g.
		Your MySQL connection id is 15
		Server version: 5.6.23 MySQL Community Server (GPL)

		Copyright (c) 2000, 2015, Oracle and/or its affiliates. All rights reserved.

		Oracle is a registered trademark of Oracle Corporation and/or its
		affiliates. Other names may be trademarks of their respective
		owners.

		Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

5.	If you expect to import large numbers of products into Magento, you can configure MySQL to use the [`max_allowed_packet`](http://dev.mysql.com/doc/refman/5.6/en/program-variables.html){:target="_blank"} parameter. We recommend a value of at least 16MB.

	{% include install/mysql_max-allowed-packet-centos.md %}

6.	Configure the Magento database instance as discussed in the next section.

## Configuring the Magento database instance {#instgde-prereq-mysql-config}

This section discusses how to create a new database instance for Magento. Although a new database instance is recommended, you can optionally install Magento into an existing database instance.

To configure a MySQL database instance:

1.	Log in to your database server as any user.
2.	Get to a MySQL command prompt:

		mysql -u root -p

3.	Enter the MySQL `root` user's password when prompted.
4.	Enter the following commands in the order shown to create a database instance named `magento` with username `magento`:

		create database magento;
		create user magento IDENTIFIED BY 'magento';
		GRANT ALL ON magento.* TO magento@localhost IDENTIFIED BY 'magento';
		flush privileges;

5.	Enter `exit` to quit the command prompt.

6.	Verify the database:

		mysql -u magento -p

	If the MySQL monitor displays, you created the database properly. If an error displays, repeat the preceding commands.

7.	If your web server and database server are on different hosts, perform the tasks discussed in this topic on the database server host then see [Set up a remote MySQL database connection]({{page.baseurl }}/install-gde/prereq/mysql_remote.html).

    We recommend you configure your database instance as appropriate for your business. When configuring your database, please keep the following in mind:

    -   Indexers require higher `tmp_table_size` and `max_heap_table_size` values (e.g., 64M). If you configure the `batch_size` parameter, you can adjust that value along with the table size settings to improve indexer performance. Refer to the [Magento Optimization Guide]({{page.baseurl }}/performance-best-practices/configuration.html) for more information.

    -   For optimal performance, make sure all MySQL and Magento index tables can be kept in memory (e.g., configure `innodb_buffer_pool_size`).

#### Related topics

*	[Set up a remote MySQL database connection]({{page.baseurl }}/install-gde/prereq/mysql_remote.html)
*	[Installing optional software]({{page.baseurl }}/install-gde/prereq/optional.html)
*	[Apache]({{page.baseurl }}/install-gde/prereq/apache.html)
*	[PHP](php-centos-ubuntu.html)
*	[Configuring security options]({{page.baseurl }}/install-gde/prereq/security.html)
*	[How to get the Magento software]({{ page.baseurl }}/install-gde/bk-install-guide.html)
