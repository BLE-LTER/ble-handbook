---
title: BLE LTER Information Management Handbook
subtitle: Everything, including the kitchen sink
author: An T. Nguyen and Tim Whiteaker -- BLE-LTER Information Managers
date: 2021-08-29
---

<a id="header"></a>

<!-- MarkdownTOC -->

- [Front matter issues](#front-matter-issues)
	- [Introduction to BLE LTER Information Management](#introduction-to-ble-lter-information-management)
	- [Our philosophies](#our-philosophies)
	- [Preamble](#preamble)
- [Tools](#tools)
	- [Tools we use](#tools-we-use)
	- [Tools we develop and maintain](#tools-we-develop-and-maintain)
	- [Getting access to things](#getting-access-to-things)
- [All about data and metadata](#all-about-data-and-metadata)
	- [High level step-by-step](#high-level-step-by-step)
	- [Metadata database](#metadata-database)
	- [Metadata template](#metadata-template)
	- [Data processing](#data-processing)
	- [Metadata processing and EML](#metadata-processing-and-eml)
	- [Data archiving](#data-archiving)
	- [BLE specific data/metadata style rules](#ble-specific-datametadata-style-rules)
- [Website](#website)
	- [Our website technologies](#our-website-technologies)
	- [How to update website](#how-to-update-website)
	- [Branding](#branding)
	- [Miscellaneous website notes](#miscellaneous-website-notes)
	- [Algolia](#algolia)
- [Bibliographic management](#bibliographic-management)
	- [Zotero best practices](#zotero-best-practices)
	- [Misc notes](#misc-notes)
- [Personnel management](#personnel-management)
	- [Add/update personnel contact information](#addupdate-personnel-contact-information)
	- [Mailing list admin](#mailing-list-admin)
- [Reporting](#reporting)
	- [Obtaining metrics](#obtaining-metrics)
	- [Presentations](#presentations)

<!-- /MarkdownTOC -->


<a id="front-matter-issues"></a>
# Front matter issues

<a id="introduction-to-ble-lter-information-management"></a>
## Introduction to BLE LTER Information Management

Beaufort Lagoon Ecosystems (BLE LTER) is a new site and member of the Long Term Ecological Research Network. The project was first funded in 2017 as one of three sites newest to the network. 

Information management was integral to the project from the start; our NSF proposal included a detailed section on the data types we will produce and how each of them will be treated. The information management team has been important project members ever since.

Tim Whiteaker (Tim) was first recruited as project data/information manager by lead project PI Ken Dunton from the 2017 beginnings. An T. Nguyen (An) was recruited by team in November 2018 and officially started in March 2019.

<a id="our-philosophies"></a>
## Our philosophies

We use modular components in our IM system and workflow -- as opposed to a comprehensive solution like [DEIMS](https://deims.org/). We try to use existing solutions whenever possible and not modify them willy nilly; we've found that there's almost always a tool somewhere suited to our purposes even in its vanilla form.

See our website summary on our information management system here at https://ble.lternet.edu/ims.

<a id="preamble"></a>
## Preamble

Dear reader, 

We speak in first person throughout this handbook. Writing in a suitably third person, passive, or imperative voice didn't come naturally.

<a id="tools"></a>
# Tools

<a id="tools-we-use"></a>
## Tools we use

### Languages

An uses a lot of R. Tim uses a lot of Python. We also write things in JavaScript, HTML, CSS, Markdown, SQL. 

Our metadata is based on the Ecological Metadata Language (EML), which is XML. Many of the actual tools we use and develop revolve around making, reading, and validating EML. Lots more on this later on.

### Software and tools

Note that while many of the tools listed below are enterprise products (or have a paying option), we strive to keep our IM system free and sustainable. With the increasing abundance of open-source and free tools, we hope to be able to do so for a long time.

- We use GitKraken as our Git client, and GitHub to manage, publicize, and collaborate on Git repositories. GitKraken integrates with GitHub well (you can use GH credentials in GK), and has a really neat tree visualization of changes in a repository.

- We use a variety of text editors to examine and edit plain text files. Tim uses VS Studio Code and An uses Sublime Text. Big note: other IMs we know heavily use the Oxygen XML Editor to edit and validate their EML documents. Oxygen is decidedly not free, although they do give out academic licenses if their logo is displayed on one's website. We decided not to go that route, and just use a text editor to look at EML. This works fine for our automated-everything, no-manual editing philosophy.

<a id="tools-we-develop-and-maintain"></a>
## Tools we develop and maintain

<a id="javascript-apps"></a>
### Javascript apps

1. PASTA-JavaScript-Search-Client

Search and show result data packages from PASTA (EDI) on website.

https://github.com/BLE-LTER/PASTA-JavaScript-Search-Client

2. Zotero-JavaScript-Search-Client

Search and show result publications from a Zotero library on website.

https://github.com/BLE-LTER/Zotero-JavaScript-Search-Client

3. Lunr-Index-and-Search-for-Static-Sites

Simple index and search for static sites.

https://github.com/BLE-LTER/Lunr-Index-and-Search-for-Static-Sites

<a id="r-packages"></a>
### R packages

1. MetaEgress

Create EML (Ecological Metadata Language) documents from LTER-core-metabase.

https://github.com/BLE-LTER/MetaEgress

2. insitu

Read, process, and flag hydrography data from BLE LTER Core Program sampling.

https://github.com/BLE-LTER/insitu

3. bleutils

Utility functions for BLE IMs.
 
https://github.com/BLE-LTER/BLE-LTER-utils

<a id="getting-access-to-things"></a>
## Getting access to things

a.k.a. rough personnel handover action plan

We use many tools that will need logins, some needing certain privilege levels. A new person on BLE's IM team will need to make sure they have access to:

- Stache `*`
- UTBox (shared drived with BLE team as a whole, we also use this for sharable file links) `+`
- UT-Austin Disk network storage (more day-to-day IM working directories) `*`
- The official IM email BLE-IM@utexas.edu address `+`
- BLE's PostgreSQL instance of LTER-core-metabase `*`
- Netlify (static website host) `$`
- Collaborator to the BLE-LTER Github organization
- Editor on Zotero group library
- EDI's three portals: production, staging, and development (one login for all)
- UTLists (Sympa mailing list management software) `+`
- Slack groups for LTER IMs (at https://lter.slack.com). Optional: EDI/NCEAS groups.
- Subscription to the im@lternet.edu mailing list, plus imc@lternet.edu for the lead IM
- Google Account for YouTube, etc. - beaufortlagoons@gmail.com. Credentials in Tim's UT Stache, shared with our lead PI Ken Dunton

Legend:

`*` UT Austin service, requires affiliation to UT (UT EID)

`+` UT Austin service, does not require affiliation to UT

`$` Tim only has the credentials

Most of these are individual accounts and each IM team member manage their own, however some accounts are shared between the BLE IM team as a whole. The most important is the PASTA 'BLE' account under 'LTER' affiliation. Only this account can upload new or revised data packages with the "knb-lter-ble" scope. All three EDI portals (production, staging, and development), plus the corresponding LTER ones, share the same authentication system, and so we log on to all of them with the same credentials.

Tim and An have their own individual accounts to metabase. However there are accounts set to do certain things (e.g. 'backup_user' has read-only access to be able to dump database contents everyday).

Stache (UT service) contains the passwords to these shared accounts.
For other things that are individual-based, a new IM team member will need to be granted access and appropriate privileges.

#### Getting remote access 

How to remote access into your UT desktop, if based out of UT and working remotely:

1. Step 1, connect to the UT VPN server

UT uses the Cisco AnyConnect software. This is available for all major operating systems. Simply download and follow instructions on UT's IT wiki. You will need to have set up two-factor authorization with your UT EID.

2. Step 2, use a remote desktop protocol. This is built into Windows systems, and require more software in other OS. The most success An's had on Linux is with the FreeRDP2 library. 

Sometimes the Remote Desktop won't connect. Restarting your own computer sometimes solves that. The work computer you're VPNing into might be off though, in which case contact the service desk for help. They might need to physically go turn the computer on. You can also do this yourself if you have access.

<a id="all-about-data-and-metadata"></a>
# All about data and metadata

<a id="high-level-step-by-step"></a>
## High level step-by-step

1. Receive data and metadata from researchers. This might be a long process, and we might hear about datasets long before we actually get them.

2. Enter metadata into metabase, clarifying with researchers along the way. Process the data, reformat it to whatever. Make metadata. 

3. Archive at EDI (staging). Send staged data package to researchers for approval and make changes as requested. Archive at EDI (production).

4. Let BLE and the world know. BLE has a formal data notification policy below. 

<a href="#header">Back to top</a>
<a id="metadata-database"></a>
## Metadata database

See https://github.com/LTER/lter-core-metabase for a first stop documentation on LTER-core-metabase as a product and a project. This section in the handbook primarily concerns usage of metabase at BLE and certain issues we've encountered.

<a id="installation-and-admin"></a>
### Installation and admin

#### Postgres woes and how to overcome them

Very verbose -- for complete newbs to the DB admin world. Windows specific, but I think once you get an idea of how the pieces get together, operating system doesn't matter as much.

Assuming a vanilla installation from executable (.exe) on Windows as downloaded from the PostgreSQL website. Some assumptions might not apply in other scenarios (e.g. where the default data directory is). 

**NOTE:** A good chunk of trouble might be avoided if PostgreSQL is _not_ installed in C:\Program Files. This folder is write-protected in many work PC systems where you are not the admin, and generally quite inaccessible in many ways. Change the directory during the installation process. 

<a id="issues-ive-run-into"></a>
#### Issues I've run into

<a id="serverservice-not-running"></a>
##### Server/service not running
One day as fine as any other, you log on to your computer and open up DBeaver ready to do some ecological data management. The database refuse to connect, citing "Connection to localhost:5432 refused. Check that the hostname and port are correct and that the postmaster is accepting TCP/IP connections." Boom. What's happening? 

This normally means the server associated with the Postgres instance, a.k.a cluster (see below), that your database lives on, is not running. In my experience, the default cluster is normally set to auto-start its server at system startup; this is not true for other clusters.

How to start a Postgres server:

Go to Command Prompt. Navigate with `cd` to the directory with all the nifty Postgres programs, generally under <directory you installed Postgres into>\PostgreSQL\<version number>\bin. Now call `pg_ctl` with option `- D <path to your directory>` then `start`. Similarly you can also call `stop`. 

What if this doesn't work:

Does it say permission denied anywhere in the cmd log? Is your data directory in Program Files? It's time to change it. 

Follow these directions since it is fairly comprehensive (while everything else here is bits and pieces from stackoverflow): [see here.](https://radumas.info/blog/tutorial/2016/08/08/Migrating-PostgreSQL-Data-Directory-Windows.html)

<a id="how-to-set-up-remote-connection-to-locally-hosted-postgres-database-on-windows"></a>
#### How to set up remote connection to locally hosted Postgres database on Windows

<a id="1-general-things-you-need"></a>
##### 1. General things you need
You need:
- To know the IP addresses of both the server and client machines, aka the PCs hosting the database and the PC trying to access it. This might mean a public-facing address or an internal one. Consult whoever is the network admin, since you'll need to talk to them by the end of this guide anyway. 
- To have set up a user and password with at minimum CONNECT rights to the database in question.

<a id="2-on-the-server-pc"></a>
##### 2. On the server PC

###### Figure out where the data "cluster" is

A Postgres data cluster is a separate instance of Postgres. There can be multiple clusters on the same server/machine. Each cluster lives in its own data directory, can be configured differently, contain separate sets of databases, and uses a different "server" and port. Note that the Postgres "server" is different from the machine server, and I lack the understanding to elaborate further.  

When you install Postgres on Windows, the default cluster is located in C:\Program Files\PostgreSQL\<pg version number>\data. Look there. This location changes depend on where you installed PostgreSQL for the first time. This default cluster will use the port 5432.

You might want to either change the default cluster directory, or create a new cluster in a different directory (via the command line , for these reasons:

- You might not have write access in C:\Program Files. This was the case with me.
- You might want to host it somewhere, of course. I briefly looked into hosting a cluster on the UT-Austin network file server, but decided against this route because (1) this seems to be a BAD IDEA(tm) reliability-wise in the DB admin world, and (2) it is unclear to me what the host to the cluster would then be. 

Proceed only once you know where the cluster in which your database resides is, and what is the port the cluster uses.

###### Change the cluster configuration
In the directory where the Postgres cluster lives, there are a number of .conf files. These contain the very high level configuration settings to the entire cluster, so treat them with caution. 

You need to change two files:

1. postgres.conf

Change listen_addresses to the client's IP address(es). You need to string-quote it. In BLE's case, this is the IP mask for the CWE group. This tells Postgres to "listen" or in other words, to expect connection attempts from these addresses.

2. pg_hba.conf

The 'hba' stands for host-based authentication. This file controls who can connect to the cluster and how they can do it.

Add a line to the end as following:
host all all <client IP address> md5;

This tells Postgres to allow the connection attempt from the specified address 
with md5 authentication.

**NOTE:** the slash thing in an IP address is very important here. Example: if you say 10.157.28.0 without appending "/24", eventually downstream you will not be able to connect to the cluster at all with a generic message, e.g. "could not load pg_hba.conf".

###### Change firewall rules to open port
Now that we're done telling Postgres to expect and allow connection, we need to tell the operating system the same. Create a Windows Defender Firewall inbound rule to open up port TCP 5432, or whatever port your cluster uses. Enable this rule. Contact your network admin if you can't do this or don't have the right to do so. This is likely the case if you see anything that says "group policy".

<a id="on-the-client-pc"></a>
##### On the client PC
Use this connection information:

Host: <server IP address>
Port: <cluster port>
Database: <your database name>
User: <your username>
Password: <your password>

<a id="our-metabase-implementation"></a>
### Our metabase implementation

We're using a Postgres instance on An's machine (IP address 10.157.18.129, computer number for IT purposes CRWR-D08182).

To connect:
Host: 10.157.18.129
Port: 5432
Database: ble_metabase
User:
Password:

To enable Tim to connect, we had to work with ITG. They set up a firewall policy
for An's computer which opens TCP port 5432 for just the CWE general network
(10.157.18.0/24). They then ran a gpupdate on An's computer.

#### Roles: Users/Groups || Permissions

Postgres has a somewhat confusing (to me) permission management scheme. To minimize confusion and make it easy, we make a distinction:

1. LOGIN ROLES (i.e. users):

- can login: you have to use a login role's credentials to initially connect to a database. Login roles need to be created with passwords.
- are associated conceptually with either ACTUAL PEOPLE, or TASKS to be performed on the database.
- to be able to perform said tasks, login roles _inherit_ permissions from the groups they are a member of.
- if other people join the team, or web apps that use the database are developed, a new login role should be created for their use, with membership to the appropriate groups.

2. GROUP ROLES:

- cannot login: you can not use a group credential to make the initial connection to a database. It follows that group roles do not have passwords. To grant membership to a group role, the logged in user has to be an admin of the group role, so this is not a security loophole. 
- are associated conceptually with PERMISSIONS on the database. Permissions to the database are granted on a group basis for easy management.
- there are three established groups, corresponding with three broad levels of permissions. I do not foresee needing another group role.
  - `ble_group_readonly` has CONNECT, USAGE, and SELECT
  - `ble_group_readwrite` has all of the above, plus INSERT and UPDATE
  - `ble_group_owner` has all of the above, plus (1) ability to GRANT membership in group roles

##### Existing structures

| Role name | Attribute | Members of | Notes |
|---|---|---|---|
| an | Create role, create DB, can login | {ble_group_owner, ble_group_readonly, ble_group_readwrite} |  |
| backup_user |  | {ble_group_readonly} | Used for daily automated backups (see below). |
| ble_group_owner | Group, cannot login | {} | Owns the database and all its objects. |
| ble_group_readonly | Group, cannot login | {} |  |
| ble_group_readwrite | Group, cannot login | {} |  |
| postgres | Superuser, can login, Create role, Create DB, Replication, Bypass RLS | {} |  |
| read_only_user |  | {ble_group_readonly} |  |
| read_write_user |  | {ble_group_readonly, ble_group_readwrite}  |  |
| tim | Create role, Create DB, can login | {ble_group_owner, ble_group_readonly, ble_group_readwrite} |  |

We use UT's Stache service to share passwords to the shared users. Tim and An each manage their own.

**NOTE**: postgres is the superuser on the entire cluster on An's machine (or more generally, the default superuser on most clusters). Do not use for mundane tasks, especially creating new objects (tables/roles/databases), since it then becomes the default owner and it's quite a hard task to revoke ownership from its clutches, since it's generally exceedingly difficult to remove ownership for superusers.

#### User privileges needed to connect to and edit the database

When creating a new user, you need to do the following. Or re-use the read_only_user and read_write_user roles created in install scripts.

At minimum:

* CONNECT ON DATABASE
* USAGE ON SCHEMA (repeat for all schemas. execute in the SQL editor tool in DBeaver or command-line psql)
* A read and query-only user: above, plus SELECT ON TABLE (repeat for all tables+views in all schemas)
* A user with write privileges: above, plus UPDATE, INSERT ON TABLE (repeat for all tables+views in all schemas)
* An all-powerful user: CONNECT and USAGE, plus GRANT ALL ON ALL TABLES

Consider granting DEFAULT privileges as well to grant access to future tables.

Granting permissions such as SELECT, UPDATE, or ALL is perhaps most easily
performed in DBeaver.

1. In DBeaver, under the database, expand Roles.
2. Double-click a user.
3. Click Permissions in the accordion.
4. Expand the schema, and then expand Tables.
5. Select all tables.
6. Check all desired boxes, or click Grant All to grant everything even if the
   box isn't already checked.
7. Click Save.

Example SQL statement:

```sql
GRANT USAGE ON SCHEMA lter_metabase TO backup_user;
ALTER DEFAULT PRIVILEGES FOR ROLE postgres IN SCHEMA pkg_mgmt GRANT ALL ON TABLES TO ble_group_owner;
```

Also, executing this SQL snippet would perform all BLE role-related tasks from scratch on a new PG cluster empty of roles. This creates both login-enabled users and groups, grant rights to groups, and assigns users to appropriate groups. 

Remember to (1) change passwords, and (2) swap out roles "an" and "tim" with appropriate usernames for real users if applicable. 

```sql
--
-- Sample SQL to set up roles on a brand new server in preparation for a database restore
-- Replace password strings
--

CREATE ROLE an;
ALTER ROLE an WITH NOSUPERUSER INHERIT CREATEROLE CREATEDB LOGIN NOREPLICATION NOBYPASSRLS PASSWORD '%password%';
CREATE ROLE backup_user;
ALTER ROLE backup_user WITH NOSUPERUSER INHERIT NOCREATEROLE NOCREATEDB LOGIN NOREPLICATION NOBYPASSRLS PASSWORD '%password%';
CREATE ROLE ble_group_owner;
ALTER ROLE ble_group_owner WITH NOSUPERUSER INHERIT NOCREATEROLE NOCREATEDB NOLOGIN NOREPLICATION NOBYPASSRLS;
COMMENT ON ROLE ble_group_readonly IS 'This group owns everything in the database, thus has all rights current and future.';
CREATE ROLE ble_group_readonly;
ALTER ROLE ble_group_readonly WITH NOSUPERUSER INHERIT NOCREATEROLE NOCREATEDB NOLOGIN NOREPLICATION NOBYPASSRLS;
COMMENT ON ROLE ble_group_readonly IS 'This group has GRANT SELECT ON TABLES plus default future permissions for the same.';
CREATE ROLE ble_group_readwrite;
ALTER ROLE ble_group_readwrite WITH NOSUPERUSER INHERIT NOCREATEROLE NOCREATEDB NOLOGIN NOREPLICATION NOBYPASSRLS;
COMMENT ON ROLE ble_group_readwrite IS 'This group has SELECT INSERT and UPDATE rights to all tables plus default permissions for future tables.';
CREATE ROLE read_only_user;
ALTER ROLE read_only_user WITH NOSUPERUSER INHERIT NOCREATEROLE NOCREATEDB LOGIN NOREPLICATION NOBYPASSRLS PASSWORD '%password%';
CREATE ROLE read_write_user;
ALTER ROLE read_write_user WITH NOSUPERUSER INHERIT NOCREATEROLE NOCREATEDB LOGIN NOREPLICATION NOBYPASSRLS PASSWORD '%password%';
CREATE ROLE tim;
ALTER ROLE tim WITH NOSUPERUSER INHERIT CREATEROLE CREATEDB LOGIN NOREPLICATION NOBYPASSRLS PASSWORD '%password%';


--
-- Role memberships
--

GRANT ble_group_owner TO an WITH ADMIN OPTION GRANTED BY postgres;
GRANT ble_group_owner TO tim WITH ADMIN OPTION GRANTED BY postgres;
GRANT ble_group_readonly TO an WITH ADMIN OPTION GRANTED BY postgres;
GRANT ble_group_readonly TO backup_user GRANTED BY postgres;
GRANT ble_group_readonly TO read_only_user GRANTED BY postgres;
GRANT ble_group_readonly TO read_write_user GRANTED BY postgres;
GRANT ble_group_readonly TO tim WITH ADMIN OPTION GRANTED BY postgres;
GRANT ble_group_readwrite TO an WITH ADMIN OPTION GRANTED BY postgres;
GRANT ble_group_readwrite TO read_write_user GRANTED BY postgres;
GRANT ble_group_readwrite TO tim WITH ADMIN OPTION GRANTED BY postgres;
```

<a id="add-ons-to-vanilla-metabase-that-are-specific-to-ble"></a>
#### Add-ons to vanilla metabase that are specific to BLE

1. Addition of two "year" columns to DataSetPersonnel

After deciding to eschew listing people as creators in BLE Core Program datasets (see section on Core Program), we settled on a solution to include a separate data table (a separate data entity in EML terms) listing personnel and their year(s) associated with a dataset. We also list the same list of people as associated parties in EML, sans year(s) as EML does not have a suitable field. 

This practice requires a few modifications to our instance of LTER-core-metabase. Normally we refrain from deviating from the vanilla version of LTER-core-metabase archived at https://github.com/LTER/lter-core-metabase We archive the SQL code we used for this modification, in case we ever need to restart our metabase from an install of the vanilla. The file `add_yearspan_to_DSpersonnel.sql` contains the SQL and also reproduced below.

The pkg_mgmt.personnel_years_associated view is queried by the function `bleutils::export_personnel` to export a CSV for use in data packages. 

```sql
-- add two columns to DS personnel

ALTER TABLE lter_metabase."DataSetPersonnel" 
	ADD COLUMN "BeginYear" int DEFAULT 2018,
	ADD COLUMN "EndYear" int DEFAULT 2018;

-- alter primary key 
-- so that it's possible to have people with two different roles, 
-- or people that hop on and off the project

ALTER TABLE lter_metabase."DataSetPersonnel" 
	DROP CONSTRAINT "PK_DataSetPersonnel";

ALTER TABLE lter_metabase."DataSetPersonnel"
	ADD CONSTRAINT "PK_DataSetPersonnel"
	PRIMARY KEY("DataSetID", "NameID", "AuthorshipRole", "BeginYear");

-- create VIEW

CREATE OR REPLACE VIEW pkg_mgmt.personnel_years_associated AS 
	SELECT d."DataSetID" as datasetid,
	p."GivenName" as givenname,
	p."MiddleName" as middlename,
	p."SurName" as surname,
	d."AuthorshipRole" as role,
	d."BeginYear" as beginyear,
	d."EndYear" as endyear,
    i."IdentificationURL" AS orcid
    FROM lter_metabase."DataSetPersonnel" d
     LEFT JOIN lter_metabase."ListPeople" p ON d."NameID"::text = p."NameID"::text
     LEFT JOIN lter_metabase."ListPeopleID" i ON d."NameID"::text = i."NameID"::text
    WHERE i."IdentificationSystem"::text = 'ORCID'::text AND d."AuthorshipRole"::text != 'creator'
  ORDER BY d."DataSetID", d."AuthorshipOrder";

-- grants for above VIEW

  ALTER TABLE pkg_mgmt.personnel_years_associated OWNER TO ble_group_owner;

REVOKE ALL ON TABLE pkg_mgmt.personnel_years_associated FROM PUBLIC;
REVOKE ALL ON TABLE pkg_mgmt.personnel_years_associated FROM ble_group_owner;
GRANT SELECT,INSERT,UPDATE ON TABLE pkg_mgmt.personnel_years_associated TO ble_group_readwrite;
GRANT SELECT ON TABLE pkg_mgmt.personnel_years_associated TO ble_group_readonly;
GRANT ALL ON TABLE pkg_mgmt.personnel_years_associated TO ble_group_owner;
```

<a id="regular-tasks"></a>
### Regular tasks

#### Backups and restores

##### Backups

A scheduled task on An's computer backs up the database to the **daily_backups**
folder once per day and logs the standard output and error (stdout & stderr) in **daily_backups/logs**. The task also copies the backups to An's Box Sync folder, which gets auto-synced to the cloud, wherever that is. Yay for multiple backups to multiple servers!

Reminders for a smooth backup experience: disconnect from the database (in DBeaver: right-click database name/Disconnect) and quit DBeaver when not using it. This is not essential, I'm pretty sure the backup process will still run without it, I think it just threw up an error one time and quitting DBeaver solved it, so yea. 

Having these backups mean that we're not at all tethered to any particular instance of a database, or the PG server on my computer (despite devoting so many words to its setup). It can implode tomorrow and all I've lost is the time it takes to set up a new one, plus some random test databases.

The backups folder can be a bit cluttered, since there are hundreds of backups, soon to be thousands. We also sometimes go weeks without change to the underlying metabase, so there will be many duplicates in content. I've contemplated writing a little script to delete these duplicates once in a while. However, the duplicates in content are not actually true duplicates from a computer's perspective, since the pg_dump utility includes the date and time in the text body, not just the file names, so it's a little harder to tease this out.

##### Restore

Backups are made in plain-text SQL format. This means we can open it in a text editor and just, you know, look at it for any irregularities. This also means we cannot use the pg_restore tool or restore via right-click on a database in DBeaver/Tools/Restore, which requires a special format. To restore from plain-text format, either right-click on a newly created database in DBeaver/Tools/Execute script, or run the file on a newly created and connected to database in command-line psql.

Existing users must be created prior to running the SQL to restore into another
server that's not the original host. It is less work to create new users than make a backup
without user privileges, then assign them.

Use this snippet, which is a copy from the one above.

```sql
--
-- Sample SQL to set up roles on a brand new server in preparation for a database restore
-- Replace password strings
--

CREATE ROLE an;
ALTER ROLE an WITH NOSUPERUSER INHERIT CREATEROLE CREATEDB LOGIN NOREPLICATION NOBYPASSRLS PASSWORD '%password%';
CREATE ROLE backup_user;
ALTER ROLE backup_user WITH NOSUPERUSER INHERIT NOCREATEROLE NOCREATEDB LOGIN NOREPLICATION NOBYPASSRLS PASSWORD '%password%';
CREATE ROLE ble_group_owner;
ALTER ROLE ble_group_owner WITH NOSUPERUSER INHERIT NOCREATEROLE NOCREATEDB NOLOGIN NOREPLICATION NOBYPASSRLS;
COMMENT ON ROLE ble_group_readonly IS 'This group owns everything in the database, thus has all rights current and future.';
CREATE ROLE ble_group_readonly;
ALTER ROLE ble_group_readonly WITH NOSUPERUSER INHERIT NOCREATEROLE NOCREATEDB NOLOGIN NOREPLICATION NOBYPASSRLS;
COMMENT ON ROLE ble_group_readonly IS 'This group has GRANT SELECT ON TABLES plus default future permissions for the same.';
CREATE ROLE ble_group_readwrite;
ALTER ROLE ble_group_readwrite WITH NOSUPERUSER INHERIT NOCREATEROLE NOCREATEDB NOLOGIN NOREPLICATION NOBYPASSRLS;
COMMENT ON ROLE ble_group_readwrite IS 'This group has SELECT INSERT and UPDATE rights to all tables plus default permissions for future tables.';
CREATE ROLE read_only_user;
ALTER ROLE read_only_user WITH NOSUPERUSER INHERIT NOCREATEROLE NOCREATEDB LOGIN NOREPLICATION NOBYPASSRLS PASSWORD '%password%';
CREATE ROLE read_write_user;
ALTER ROLE read_write_user WITH NOSUPERUSER INHERIT NOCREATEROLE NOCREATEDB LOGIN NOREPLICATION NOBYPASSRLS PASSWORD '%password%';
CREATE ROLE tim;
ALTER ROLE tim WITH NOSUPERUSER INHERIT CREATEROLE CREATEDB LOGIN NOREPLICATION NOBYPASSRLS PASSWORD '%password%';


--
-- Role memberships
--

GRANT ble_group_owner TO an WITH ADMIN OPTION GRANTED BY postgres;
GRANT ble_group_owner TO tim WITH ADMIN OPTION GRANTED BY postgres;
GRANT ble_group_readonly TO an WITH ADMIN OPTION GRANTED BY postgres;
GRANT ble_group_readonly TO backup_user GRANTED BY postgres;
GRANT ble_group_readonly TO read_only_user GRANTED BY postgres;
GRANT ble_group_readonly TO read_write_user GRANTED BY postgres;
GRANT ble_group_readonly TO tim WITH ADMIN OPTION GRANTED BY postgres;
GRANT ble_group_readwrite TO an WITH ADMIN OPTION GRANTED BY postgres;
GRANT ble_group_readwrite TO read_write_user GRANTED BY postgres;
GRANT ble_group_readwrite TO tim WITH ADMIN OPTION GRANTED BY postgres;
```


#### Applying new features or patches

Remember to log in with a user in group ble_group_owner when changing the schema. This simplifies permission issues downstream, such as when granting default privileges for new tables to other users.

Keep an eye on the LTER-core-metabase Github repository. "Watching" the repo will trigger email updates. An currently maintains this project, so by default keeps up with new patches and in fact wrote a lot of them. The "migration" branch will contain the latest sequentially numbered patches, see documentation on that repo for information on this system. Check the table `pkg_mgmt.version_tracker_metabase` for information on past applied patches. Note that occasionally new "one big file/OBF" or essentially a schema dump with all patches incorporated. If BLE instance of metabase has fallen too far behind, instead of applying a whole lot of patches, you might want to consider setting up a new instance from the latest OBF, dump out data from the old metabase, and insert into the new. 

Once you've determined that a patch needs to be applied:

- inspect it. If there are new GRANT statements involved, these changes are necessary: `%db_owner%` to `ble_group_owner`, `read_write_user` to `ble_group_readwrite`, and `read_only_user` to `ble_group_owner`. 
- either:
	- download the .sql patch, make changes, make sure the BLE metabase is the active DB in DBeaver (right click > make active), then right click > execute script.
	- copy the raw SQL code into a new SQL editor window in DBeaver, make changes, then execute line by line or Ctrl+A > Ctrl+Enter to execute the whole thing.
 
<a href="#header">Back to top</a>
<a id="metadata-template"></a>
## Metadata template

We use a metadata template to collect information about datasets from scientists. This is structured similarly to metabase, while maximizing legibility and user friendliness for researchers. 

It consists of: 
- a metadata template (.xlsx file)
- four pages of instructions (PDF)
- abstract and methods templates (.docx files)
- example package, which is a .zip of data files and accompanying, filled-out metadata templates

On Box, we keep a zip and publishes it on a stable link https://utexas.box.com/v/ble-metadata-template. This zip should always be updated to the latest canon version. BLE website links to this zip. 

Austin Disk is where we keep the canon version: under BLE LTER > Data-notes > BLE practices > metadata_template > canon. This itself is a git repo at https://github.com/BLE-LTER/ble-metadata-template for version control purposes.

<a id="how-to-update-template"></a>
### How to update template
This is a copy of the README on the git repo.

#### Template Excel

1. Open file `metadata_template.xlsx`
2. Make changes. Make changes to example package if applicable. Make changes to instructions if applicable.
3. Save file(s)
4. See common steps.

#### PDF instructions

1. Open file `data_submission_instructions.md`
2. Make changes. Hit save on source Markdown.
3. Open command prompt on a computer with pandoc enabled and saved in the system PATH. 
4. Navigate to the current directory containing template and source Markdown. 
5. Execute these commands in Windows Command Prompt. pandoc needs to be installed and visible on your system (e.g. in the system PATH). In my case, pandoc comes bundled with RMarkdown/RStudio and RStudio kindly adds it to the PATH environment variable for me.  

```
>K:

>cd "K:\Data-Notes\BLE-Practices\metadata_templates\canon"

>pandoc data_submission_instructions.md --pdf-engine=xelatex -o data_submission_instructions.pdf
```
6. Check result PDF to make sure your edits appear.
7. See common steps.

<a id="common-steps-after-editing"></a>
#### Common steps after editing

After any updates, be sure to:
- Git commit and push changes
- Zip template package up, be sure to include:
	- Excel
	- PDF
	- sample package
- Save to Box > Beaufort LTER > Website > FileLinks > "metadata_template.zip". Using that exact archive name will ensure links and version control work.

<a href="#header">Back to top</a>
<a id="data-processing"></a>
## Data processing

<a id="data-directory-structure"></a>
### Data directory structure

We use a certain directory structure for working with data packages.

Under the Austin disk folder at `\\austin.utexas.edu\disk\engr\research\crwr\Projects\BLE-LTER` we have a Data directory. Each data package constitutes a child directory under Data. All operations with this data package are performed within this folder. Naming convention is `(dataset ID)_(dataset nickname)`, e.g. "12_sediment_pigment".

Within each data package directory:
-  "FromPI" contains data and metadata files as scientists sent them. If there have been multiple versions recived from PIs, then create folders with ISO dates received as dir names. If lots of confusing versions, consider making a README to explain the difference. 
- "Clean" contains 
	- data files after processing and ready to submit. When I go to upload to EDI, this is where I'd browse to.
	- A directory named something like "EML_generation" or "EML_RPRoject_datasetID". This is where R scripts and RProject files (history, RData) live.
	- In some earlier datasets, "EML_generation" can be level with "Clean" and/or can contain final data files. 


<a id="how-to-initiate-a-new-data-package"></a>
### How to initiate a new data package

Run `bleutils::init_datapkg(*insert dataset_id*, *insert dataset nickname*)` in any R console. This will (1) create a folder named datasetid_nickname under our Austin disk Data folder, with sub-folders called FromPI and Clean > EML_generation, and (2) create a R script named datasetid.R from template with the appropriate IDs subbed into function calls. The parent folder defaults to "K:/Data" on my machine. Modify the `base_path` argument in `init_datapkg()` if needed.

- Our dataset IDs increment from 1. `init_datapkg()` will return error if you attempt to use an ID already existing within that folder, and tell you the next available ID (i.e. the largest existing ID + 1). I don't see any reason right now to skip numbers, so this should work. 

- I do this fairly early on in the process: normally, as soon as PI have sent us a file somewhere, even if it's a sample with no metadata, since we know there's data coming at some point. I do not enter any information into metabase until we receive complete good quality metadata.

- Create a new R project under EML_generation/EML_RRproject_(datasetID) for easy project management. I looked into how to automate this with `init_datapkg()`, no dice so far. Instead, one has to open RStudio, select File/New Project/Associate project with existing directory, then navigate to the correct folder to initiate a new project.

<a id="data-processing-1"></a>
### Data processing

All data processing should be performed in scripts for transparency and reproducibility, and also for our convenience: PIs often re-send data, and all changes by us made manually in Excel will be lost. I use R and therefore a lot of our workflows and helper functions are centered around R, but there's no reason another scripting language would not work. 

The R script created by `init_datapkg()` has pre laid-out sections (but no code, can't template processing code) for light data processing. For tasks beyond renaming columns or fixing small typos, I would create a new script.

Data are read in from the FromPI directory, and written out to Clean (which ideally is parent to the R script). This ensures reproducibility and transparency of processing steps taken.

#### netCDF

##### When to use

Gridded data with lots of observations can be packaged a lot smaller in netCDF than CSV form. Generally, we do this when a CSV would exceed circa 20 million rows and 5/6 columns in long table form, resulting in a CSV file > 1 GB. Remember that lat/lon/time/site codes already take up 3-4 columns.

netCDF cannot be checked for data-metadata congruency by PASTA's ECC.

##### How to generate netCDFs

This of course depends on the source format. We have done and attempted to do this twice as of March 2020 for datasets 5 (hydrology model by Mike Rawlins) and 7 (moorings by Jeremy Kasper) and have some insights.

- R and Python can both handle these tasks. Use package `ncdf4` in R and module `netCDF4` in Python. In our folder for dataset 7, see merge_nc.py for an example python routine and 
netcdf.R for an example R routine. 

- Execute the conversion on local storage, not Austin disk. A network drive dramatically slows these packages down by as much as 100 times. Our python routine that takes 6 seconds on local disk takes 650 seconds on Austin disk. The equivalent R routine that takes 5 minutes on local disk takes at least 2 hours. R is indeed quite a bit slower than python here. 

- Mike Rawlins' dataset used the EASE-grid, on a Lambert azimuthal projection. We had a lot of trouble configuring the netCDF file so that ArcGIS would pick up the EASE-grid. For more documentation on what we did, see folder Data > 5_rawlins > netcdf.

#### netCDF metadata 

##### in the netCDF file

We strive to make the netCDFs self-contained with complete metadata on their own. This might mean duplicating metadata already in EML, even if the netCDF will be packaged with EML. 

Our goal for netCDFs:

- Compliance with CF conventions

- Compliance with the applicable NCEI netCDF template. See list of templates [here](https://www.nodc.noaa.gov/data/formats/netcdf/v2.0/). 

- Opens in ArcGIS with correct projection and correct location (i.e. ArcGIS recognizes the CRS plus the lat/lon values).

Possible metadata duplication between EML and netCDF global attributes:

- title: use overall dataset title
- summary: use overall dataset abstract
- keywords: use keywords applicable to data in netCDF form (assuming there are other data entities packaged alongside netCDF)

##### in EML

Document the netCDF as otherEntity. Metabase already has netCDF as a file type that would fill in the correct metadata.

<a href="#header">Back to top</a>
<a id="metadata-processing-and-eml"></a>
## Metadata processing and EML

<a id="enter-metadata-into-metabase"></a>
### Enter metadata into metabase

Once a metadata template is received from the data correspondent (can be PIs, can be Core Program manager Nathan, can be someone else) and is reasonably filled out, I start the process of transferring the information from the template Excel to metabase. I used to edit the template itself, e.g. to fill in hidden attributes columns, but no longer do so as it was IMO unnecessary extra work.

I populate metabase for a new dataset in this order:

1. Tables that do not reference other tables via FKs 
- DataSet. Edit title and abstract as needed during.
- DataSetMethod. Enter methods in docbook format, edit for formatting, tense, and clarity. I do this manually; but one can use pandoc (command line tool, comes with RStudio) to do this. 
- DataSetTemporal

Common pitfalls:
- Forgetting closing tags in docbook formatted abstract/methods
- Having ampersands "&" in docbook formatted things. Very common in references. This will result in a "failed to parse" xml error in the very last EML generation step. Use "&amp;"
- Having less than/greater than signs "</>" in docbook formatted things.

2. Tables that do reference other tables via FKs but still are relatively simple
- DataSetEntities
- DataSetSites
- DataSetKeywords
- DataSetPersonnel
- DataSetAnnotation
- DataSetAttributeAnnotation
- DataSetMethod* (Software/Protocols/Instruments/Provenance). With the exception of Provenance, the other tables haven't seen play so far.

Before entering info into these tables, one can scan for things that entries that might not be present in the List* tables yet, e.g. keywords we've never used before or a person we've never listed on previous datasets, and enter that information into corresponding parent List* tables. However, sometimes it's easier to just enter the info into the DataSet* tables and let DBeaver tell you what's missing from the parent table when you go to save it.

3. Tables that are more involved
- DataSetAttributes (remember: check units (1) if they're in EMLUnitDictionary yet, and (2) if they have abbreviations in our style yet)
- DataSetAttributeEnumeration
- DataSetAttributeMissingCodes

Sometimes it is easier and quicker to copy attributes and enumeration/missing codes from similar existing datasets. This is especially true for Core Program datasets. 

Common pitfalls: 
- not having a TextPatternDefinition when attribute is nominalText or ordinalText. I normally just say "any text".
- not having an Unit or a NumberType when attribute is interval or ratio 
- enumerated (categorized/coded) attributes MUST be specified as nominalEnum or ordinalEnum. Otherwise even if they have corresponding entries in DataSetAttributeEnumeration, resulting EML will not have code/definition pairs

#### Misc quirks

- If somebody doesn't have an ORCID, there still MUST be an entry for them in ListPeopleID. Just leave the column IdentificationURL as NULL (allowable in metabase schema). If there's no entry for them, the resulting personnel table exported from metabase will not have that person (the associatedParty tree still includes them).

<a id="exporting-eml"></a>
### Exporting EML
Once metadata in metabase is complete, it's time to start data processing and exporting EML. One does this in R.

- Open up the RProject associated with the dataset and open up script `dataset(datasetID).R`. This script would have been generated from template for you if `bleutils::init_datapkg()` was called to initialize the package. The RProject has to be created manually; I haven't found a way around that. 
- The script should be set up with most of the script lines you need, with dataset IDs subbed into function call arguments. 

In short, there are these function calls to execute each time you generate a new EML:
- `MetaEgress::get_meta()`. This queries metabase for that dataset ID. Most of the time this call will be wrapped in a call to `bleutils::append_units()`. The R console will ask you for your metabase username & password after this is called. Any user with READ privileges would suffice.
- `MetaEgress::create_entity_all()`. This assembles the data entity components of EML.
- `MetaEgress::create_EML()`. This takes the assembled entities and assembles the other stuff and outputs a complete emld list structure ready to be validated and written to file.
- `EML::eml_validates()` tests the resulting emld structure for schema validity.
- `EML::write_eml()` writes the emld list structure to file.

The resulting EML would be deposited into the same directory as the script.

<a id="revisions"></a>
### Revisions

Make sure to do these tasks if a dataset needs to be revised:

- Increment the Revision number in metabase's DataSet table. Note that this number is always the current *production* revision number. The *staging* revision number can get much higher. I manually edit revision numbers in EML when uploading to the staging server.
- Add a note in metabase's pkg_mgmt.maintenance_changehistory table. 

<a href="#header">Back to top</a>
<a id="data-archiving"></a>
## Data archiving

<a id="where-we-archive"></a>
### Where we archive

We archive most data packages at the Environmental Data Initiative (EDI).  The
exception is for entities for which a more suitable archive already exists, such
as GenBank for genomics data.

Because we use EDI as the sole source of our online data catalog, we still
archive in EDI at least a summary table for externally archived datasets such as
genomics data.

<a id="which-member-node-are-we"></a>
#### Which member node are we

When signing in to the EDI data portal and asked for a member node, we're urn:node:LTER.  EDI filters on the package identifier (knb-lter-ble): any of the "knb-lter-[site acronym]" packages go through urn:node:LTER, while the rest go through urn:node:EDI.

<a id="replication"></a>
#### Replication

We replicate our EDI data packages so that they show up in the Arctic Data Center
catalog.  There's a single DOI for a data package, which resolves to the LTER
Data Portal (i.e., EDI).

Replication requires these two steps:

1. The dataset must be synced and indexed at search.dataone.org.  If you search
   for "knb-lter-ble" and find the dataset, then it is indexed.  Syncing is something
   EDI manages, but sometimes the process lags, so if you notice something isn't
   synced after a couple of weeks, contact EDI to see what's going on.
2. Once the dataset is synced to DataONE, the BLE information manager must
   provide the DOI of the dataset to ADC so they can harvest the metadata.

We wrote [a replication guide](https://docs.google.com/document/d/1QJyj3biai9k5Kaxp3v3Rk2r7pmjirYRHMLySgagMAnw/edit#heading=h.wn7g8mmmpq5c). In this we expound on how to best enable replication between EDI-DataONE-ADC and what we as IMs can do to facilitate this. Aside from metadata best practices, this guide also recommends adding a snippet of XML into additionalMetadata:

```xml
<additionalMetadata>
    <metadata>
      <d1v1:replicationPolicy xmlns:d1v1="http://ns.dataone.org/service/types/v1" numberReplicas="1"
        replicationAllowed="true">
        <preferredMemberNode>urn:node:ADC</preferredMemberNode>
      </d1v1:replicationPolicy>
    </metadata>
  </additionalMetadata>
```

However, as of April 2020 this is not feasible to implement in an automated way via MetaEgress yet. This is because the EML R package currently does not support additional namespaces (e.g. "d1v1" in the code snippet above. See issue #289 on their github here https://github.com/ropensci/EML/issues/289).

BLE has an affiliation agreement with AOOS. Rather than archive with AOOS as they typically require, we continue to archive at EDI with our relevant packages linked from AOOS's [ocean acidification data page](https://aoos.org/alaska-ocean-acidification-network/ocean-acidification-data/). Links are provided such that they always point to the latest revision of a dataset, e.g., [https://portal.edirepository.org/nis/mapbrowse?scope=knb-lter-ble&identifier=9](https://portal.edirepository.org/nis/mapbrowse?scope=knb-lter-ble&identifier=9). In case AOOS needs a cached copy of the data, we instructed them to subscribe to dataset updates via [EDI's event subscription service](https://portal.edirepository.org/nis/eventSubscribe.jsp).

<a id="why-we-archive-at-edi"></a>
#### Why we archive at EDI

We want our datasets to show up in both the LTER data portal (which EDI handles)
and the Arctic Data Center (ADC), so we must replicate. Replication is currently
(2020-01-08) one-way.  PASTA is not intrinsically tied to DataONE so data does not flow in from
DataONE.  (This is for flexibility; EDI is not dependent on where DataONE goes down
the road.)  ADC uses MetaCat so is intrinsically tied to DataONE.

So, we can only go from EDI to ADC, which is why we archive at EDI.

When BLE started, we discussed this with our program officer Roberto Delgado,
and he approved our plan of EDI being the primary data site with replication at
ADC, in an email sent on April 26, 2019.  He documented this in the eJacket
under Diary notes for the record.

<a id="who-does-the-archiving"></a>
### Who does the archiving

The BLE information manager archives data packages at EDI. For entities that are
not archived at EDI, such as genomics data going to GenBank, the individual
researcher typically archives that entity, since they probably are already
familiar with the archives for their field.

<a id="how-we-archive-at-edi"></a>
### How we archive at EDI

We currently submit data and EML metadata manually via the [EDI data portal](https://portal.edirepository.org/nis/harvester.jsp).

<a id="handling-large-files"></a>
#### Handling large files

As of 2020-01-08, EDI has a maximum upload limit of 500 MB per file. If a file
in your data package exceeds this limit, you must place the file online, and
provide a link to the file in EML. EDI's PASTA system will harvest the file and
update the link in EML.

At The University of Texas, the easiest way to place the file online is to
upload it to UT Web until it is harvested, and then remove it. This has been
tested on a 2 GB file.  There is a UT Web website for some of BLE PI Ken
Dunton's various Arctic projects, arcticstudies.org, which can be used
for temporary BLE big file storage.

To upload a file to UT Web:

1. Submit a service request ticket for access to utw10130, the UT Web space for
   what is the arcticstudies.org website.  You will need a UT EID for this.
2. Install FileZilla.
3. In FileZilla, connect to panel.utweb.utexas.edu, port 22, using your EID
   credentials.
4. Browse to /home/utweb/utw10130/public_html/tmp.
5. Upload the file(s) to that folder. After the upload, be sure the file has
   "read" permissions for public users by viewing the file's properties in
   FileZilla.
6. Update the EML file for the data package to includes links to the files.  For
   example, for a file named big_file.csv, the link would be <https://arcticstudies.org/tmp/big_file.csv>.

If UT Web is no longer an option, you could try:

- Box with sftp. Not sure of the details, but you can create some sort of
  AUTHID with keys for automated processes to put and get things from Box.
- Office 365 Teams (backend SharePoint). You could ask IT to create a Microsoft
  Team for you and you could try their cloud storage to see if it works any
  differently than Box. Every Team has 25 TB of storage available.
- TACC.  It may be a pain because they are now requiring two-factor
  authentication, but perhaps they have worked those bumps out.
- Send a hard disk to EDI.
- Send list of 3rd party URLs such as for Box.com for your entities to
  support@environmentaldatainitiative.org and ask them to supply a working URL that you can insert into your
  EML.

Note that file sharing services such as Box and Google Drive will not work as
direct links in EML, not even if you ask for a direct link from those services,
because behind the scenes they use redirects without proper responses. The links
work fine in a browser but not for the PASTA harvester, hence the last bullet in
the list above, in which the EDI manually downloads the file from Box, uploads
it somewhere, and then sends the link so you can insert it into EML.

Care to know more about why those supposedly direct links won't work? EDI uses
an initial test with an HTTP HEAD call to ascertain the liveness of URLs.
Because the assume that an HTML response is generally either an error or a
request to login - that is, not data (unless clearly stated in EML in the
"physical/dataFormat/externallyDefinedFormat/formatName" as "text/html", they
judge the quality test as a failure when they do receive a "Content-Type" as
"text/html". In the case of the UTexas Box URLs for a CSV file, for example,
they see a "text/html" content type for the HEAD method (in addition to a 404
Not Found response), but a "text/csv" for the GET method.  For example, the
following two requests entered in a command window would return different
responses (assuming the BOX link is valid):

```shell
curl -i -L -X HEAD https://utexas.box.com/shared/static/4yti3q0sbvytbfk078eimwxfrlw5cccz.csv

curl -i -L -X GET https://utexas.box.com/shared/static/4yti3q0sbvytbfk078eimwxfrlw5cccz.csv
```

What **should** happen is that the responses are the same. In this case, even
redirects are OK. For example, try

```shell
curl -i -L -X HEAD https://sbc.lternet.edu/external/InformationManagement/tmp/kelp_microsatellite_markers_CARP_20090910_geospatial.csv
```

<a id="fair-checkers"></a>
### FAIR Checkers

Once a dataset is archived, you can check its FAIR compliance at EDI or DataONE using links like the ones below.

* https://portal.edirepository.org/nis/reportviewer?packageid=knb-lter-ble.18.2
* https://search.dataone.org/quality/https%3A%2F%2Fpasta.lternet.edu%2Fpackage%2Fmetadata%2Feml%2Fknb-lter-ble%2F18%2F2

<a id="our-websites-data-catalog"></a>
### Our website's data catalog

Our website uses the PASTA Javascript client to query the EDI repository for our datasets and display them on a webpage. This query looks for the identifier 'knb-lter-ble'. Our website also links to the same set of datasets at ADC via a canned query -- a general search for "Beaufort Lagoon Ecosystems".

To ensure that both queries will return the entire BLE data corpus -- and nothing else:

- Put "Beaufort Lagoon Ecosystems LTER" in the keywords section of every single dataset. 
- Use the 'knb-lter-ble' scope while archiving at EDI.

### Data notification policy

**Part 1: When a dataset is initially published (i.e., version 1)**

a. Any people associated with the dataset (i.e., people who appear as authors, contacts, associated parties, etc., in the metadata) are sent a data announcement like the template [data_announcement.md](data_announcement.md).

b. The information manager (IM) will briefly announce the dataset to the BLE team via the ble-lter-all listserv (ble-lter-all@utlists.utexas.edu), providing the citation which includes the DOI.

c. The social media manager, as notified by the IM, will announce the dataset to the public via Twitter and Facebook.

**Part 2: When a dataset is revised**

a. If data are revised, the IM will announce to ble-lter-all as in 1b as well as any people associated with the dataset.  The IM will indicate if the revision is appending new data or changing existing data.  If changing existing data, the IM will highlight the changes (side note: we must also remember to document the changes in the metadata).

b. If only metadata are revised, e.g., fixing a typo in a contact address, then no notifications are sent.

<a href="#header">Back to top</a>
<a id="ble-specific-datametadata-style-rules"></a>
## BLE specific data/metadata style rules

Refer to BLE as either "Beaufort Lagoon Ecosystems LTER" or "BLE LTER". Avoid using just "BLE" except when talking to other LTER people, as it's without context, and avoid the hyphenated form "BLE-LTER". 

<a id="types-of-datasets-by-ble-involvement"></a>
### Types of datasets by BLE involvement

We roughly categorize three types of datasets, according to the degree and kind of BLE involvement:

1. "Core Program" datasets. These are the ongoing research projects that collect core, baseline data about the lagoons, and inform all other projects within BLE. These are considered the brainchild of BLE itself as an organization, not any one PI.

2. "PI-driven" datasets. These arise from the research interests of individual PIs, and are primarily funded by BLE.

3. "PI-driven" datasets that are not primarily funded by BLE. These get handled and archived by us on an individual basis after approval by the lead PI(s).

<a id="all-datasets"></a>
### All datasets

#### Units are abbreviated and appended to column names

Per PI Yvette Spitz's request and concern over easily accessing attribute unit information, as of April 2020 we have decided to:

- publish a short user's guide to accessing metadata, accessible from our website data catalog and at https://utexas.box.com/v/ble-access-metadata
- adopt a practice of appending abbreviated units to column names, e.g. "temp_C" or "DOC_g_L"

##### Here's how this is implemented during our normal workflow

1. Attribute names are entered into metabase as usual. I.e. the column DataSetAttributes.ColumnName for above example would read "temp."
2. If applicable, the attribute is associated with a fully spelled out unit, i.e. DataSetAttributes.Unit has "celsius"
3. The handling IM makes sure that this unit has an abbreviation, i.e. the corresponding row in EMLUnitDictionary has column abbreviation filled out. Note: initially I've gone into metabase and filled out abbreviations for the units we do use (i.e. referenced as FK in DataSetAttributes.Unit); as we make use of new units their abbreviations need to be entered as well. Use the SQL query `SELECT DISTINCT id, abbreviation FROM lter_metabase."EMLUnitDictionary" d INNER JOIN lter_metabase."DataSetAttributes" a ON d.id = a."Unit";` to return a result set of only units we currently use. Edits on column abbreviation in the result set apply to the parent EMLUnitDictionary table. 
4. How to abbreviate: abbreviate each component in the unit according to convention, separating each component by underscores. No super/subscripts, no "per", no special characters (e.g. "micro" is u). E.g. "micromolePerMeterSquaredPerDay" becomes umol_m2_day. Where there are widely acknowledged existing abbreviations, use them, e.g. "partPerMillion" is ppm. 
5. During processing in R, e.g. in script dataset1.R (all datasets have this script within a R project folder), the `MetaEgress::get_meta` call gets wrapped by a call to `bleutils::append_units`, e.g. `metadata <- append_units(get_meta("ble_metabase", dataset_ids = 1))`. `append_units` appends the unit abbreviation on file to the attribute name after an underscore, e.g. "temp" becomes "temp_C" in all the appropriate metadata tables. 
	- If `append_units` is not called, EML metadata produced will not have units in column names
	- After, use `bleutils::rename_attibutes` to rename the headers of the appropriate data file. Columns in data must be in exact order of attributes listed in metadata; make sure this is true. `rename_attributes` requires the queried metadata list structure as input, so it will always take whatever attribute names are listed, whether `append_units` was called or not.
6. proceed as usual with EML generation.

##### Why we do it this way:

- No modifications to metabase schema. We are pretty pro-vanilla-metabase. The column we use EMLUnitDictionary.abbreviation is an existing column and an under-utilized one; we only modify its contents.
- No direct modification of attribute names mean that all attributes sharing the same unit are appended to consistently and using the same abbreviation. If we want to change the abbreviation we can do it and re-generate EML in one fell swoop, without having to go in and edit all the attributes using that unit. 
- Very easy to leave it off a dataset (just don't call `append_units`), although finer grained control, e.g. leaving units off of specific columns, is not possible to do in R at the moment.

##### Updating the EMLUnitDictionary table

Updates to the EMLUnitDictionary might be necessary with new versions of EML. Our plan is to perform a full/outer join on the existing EMLUniDictionary keeping all rows, so that (1) our custom edited abbreviations survive the mode, (2) metabase continues to support older and custom units.

<a id="core-program"></a>
### Core Program data

Datasets produced by the Core Program fall under an umbrella and as such need to follow a common format. Following are practices we have for Core Program datasets following much discussion and trial-and-error. 

There are two documents on Box with some of these rules oriented towards our Project Managers/scientists to help them as they submit Core Program data. This is [a spreadsheet](https://utexas.app.box.com/file/422189027582) with predefined columns and the appropriate way to assign them to data, and this is a [Word doc](https://utexas.app.box.com/file/649019663047) written by CB with the general workflow of Core Program data from lab to our IM's hands. 

This handbook version is a much more exhaustive version for IMs. 

#### Types of CP data 

According to the source: 
- data from water samples
- data from sediment samples
- data from moorings/instruments

The first two are discrete and obtained during our three annual field campaigns, while moorings give continuous data. This determines how we apply some of the following practices, so be sure to know which type the dataset you're working with is. 

#### Dataset titles 

- Mention time series if data is continuous from moorings
- Mention water/sediment if sample type is such
- end with "from (insert types of sites) along the Alaska Beaufort Sea coast, (year data begins)-ongoing".
- E.g. "Sediment pigment from lagoon sites along the Alaska Beaufort Sea coast, 2018-ongoing"

<a id="data-columns"></a>
#### Data columns 

Column names:

- lowercase (station not Station)
- capitalized only when denoting standard acronyms (PAR for photosynthetically active radiation) or when it's part of the variable name (pH)
- underscores between words (date_time not date.time)
- units appended to the end
- date_time for mooring datasets and date_collected for discrete datasets

Standard columns, also in this order:

- node: Central/East/West (discrete samples only)
- lagoon: Elson East/Elson West/Simpson/Stefansson/Jago/Kaktokvik/not applicable. River stations are assigned the lagoon they discharge into. Ocean stations are assigned "not applicable." (discrete samples only)
- station: station codes or IDs (e.g. KALD2).
- season: under ice/break up/open water (discrete samples only)
- date_time: date and time in YYYY-MM-DD hh:mm:ss or YYYY-MM-DD hh:mm format. Normally applies to instrument data. Exception is when archiving raw data (see dataset ID 3, hydrography), then another date time format might be ok. Continuous/mooring data.
- date_collected: date in YYYY-MM-DD format. Discrete data.
- water_column_position: surface/bottom. There is also mid-column, which CP data does not use. Formerly we assigned river and ocean stations "not applicable" but now all shallow/river/ocean stations are assigned "surface." (discrete water samples only)
- sample_depth (discrete water samples only)
- [data columns, including notes]
- collection_method: grab/pump (discrete water samples only)
- station_name: fully spelled out station names, e.g. Kaktovik Deep Station 2 
- latitude
- longitude
- station_depth
- habitat_type: lagoon/river/ocean
- station_sampling_priority: primary/secondary/river/ocean (discrete samples only)

Data sort, sort all CP datasets by these columns in this order before submission. Use the R function `bleutils::sort_cp_rows` to do this quickly, only after `bleutils::rename_attributes` has been called to ensure that column names are exactly as below. Be sure to specify the `type` argument to `sort_cp_rows` to be one of three "water", "sediment", or "mooring".

- node (discrete only)
- lagoon (discrete only)
- station
- date_collected (discrete only) / date_time (mooring)
- water_column_position (discrete water samples only)

#### Entities 

Entity names:

- Include variables in data
- Include timeframe to year resolution
- Do not include "BLE LTER"
- Example: Dissolved organic carbon and total dissolved nitrogen, 2018-ongoing

Data table entity descriptions:

- Include variables in data
- Include timeframe to year or month resolution
- End with some variation to the effect of "from BLE LTER Core Program, [month and year this dataset starts]-ongoing"
- Example: Dissolved organic carbon and total dissolved nitrogen from BLE LTER Core Program sampling, Aug 2018-ongoing
- If raw data or some other variation of data, prepend designation to description of finished data. E.g. Raw data: Dissolved organic carbon and total dissolved nitrogen from BLE LTER Core Program sampling, Aug 2018-ongoing

Other entity descriptions:

- State clearly what the other entity is and how it relates in the context of the package.
- Example: Annotated RMarkdown script to process, calibrate, and flag raw TCM data.

File names:

- underscored
- Prepend with "BLE_LTER"
- Then with the nickname for the dataset if applicable, e.g. "hydrography", not if dataset is nicknamed after PI. I avoid PI nicknames in contexts outside of BLE IM team though, as it makes less sense for users. E.g. dataset ID is nicknamed informally "Rawlins" within the team, after Mike Rawlins, but in the published dataset the shortname is "hydromodel". 
- For data files: add one or two word descriptive moniker for data, if the dataset has more than one primary data sheet.
- Examples: 
	- "BLE_LTER_hydrography_CTD.csv". I used to add the timeframe to filenames, e.g. "BLE_LTER_CTD_2018_ongoing.csv" but on reflection I do not think this is necessary. 
	- "BLE_LTER_sediment_pigment.csv" "sediment_pigment" is the dataset nickname, but also the content of the only data table.
- Personnel tables are named "BLE_LTER_datasetnickname_personnel.csv". E.g. "BLE_LTER_hydrography_personnel.csv".
- Additional files that are not data, e.g. deployment details, script, or schematics: use the the same principles as naming data files. E.g. "BLE_LTER_hydrography_CTD_QAQC.Rmd" or "BLE_LTER_SIMB_deployment_information.csv". 


<a id="personnel--responsible-parties"></a>
#### Personnel / Responsible Parties

<a id="creator"></a>
##### Creator

Core Program packages only have one creator with the organization name "Beaufort Lagoon Ecosystems LTER, Core Program". See the entry in metabase with NameID "blecreator-core". This is in order to generate citations in this form: 

> Beaufort Lagoon Ecosystems LTER, Core Program. 2019. Stable oxygen isotope ratios of water (H2O-d18O) from coastal river, lagoon, and open ocean sites along the Beaufort Sea, Alaska, 2019-ongoing. Environmental Data Initiative. https://doi.org/DOI_PLACE_HOLDER. Dataset accessed 12/04/2019.

So that they are analogous to this citation from a PI-driven dataset (see comm. with Ken Dunton/Jim McClelland October/November 2019):

> Beaufort Lagoon Ecosystems LTER, V. Lougheed. 2019. Carbon flux from aquatic ecosystems of the Arctic Coastal Plain along the Beaufort Sea, Alaska, 2010-2018. Environmental Data Initiative. https://doi.org/DOI_PLACE_HOLDER. Dataset accessed 12/04/2019.

<a id="other-people"></a>
##### Other people

Other people involved in the dataset will be credited as an associated party in the EML record. The order might still matter, so order as the PI have written them down in the template. To be listed as an associated party, a person has to have handled/been responsible for the data at some point, so as to be able to answer questions if necessary. The PI supplies this list normally, so not an action item for us, just FYI. 

In addition to listing people as associated parties in EML, we will include a personnel table as a data entity. This table will essentially have the same information as the EML entries, but also include years of involvement in this role with the dataset so that data users can track down appropriate people to ask about specific periods in the dataset. We use an add-on to vanilla metabase to keep track of people and years (see section BLE add-ons to vanilla metabase). 

To generate a CSV table once metabase is populated, use the R function 

`bleutils::export_personnel` 

This function takes care of querying metabase for the specified dataset ID, and spits out a ready made personnel CSV. Rough naming convention is `BLE_LTER_[dataset nickname]_personnel.csv`. 

I call this function from inside the directory with other data files. I list the personnel entity last in metabase: e.g. if there are five actual data entities, the EntitySortOrder for the personnel table is 6. Note that due to a MetaEgress quirk, all dataTables will be listed before all otherEntities. 

Remember to list the seven columns of the personnel CSV in DataSetAttributes. Easiest way is to duplicating the same set of attributes from a previous Core Program dataset. 

<a id="stations"></a>
#### Stations

Core Program sampling makes use of a certain number of fixed stations. Normal practice for PIs in their data is to include station codes (e.g. KALD1). For Core Program datasets and most other datasets where this is applicable, it's our practice to include contextualizing columns in the same data table. These include: station name (KALD1 is Kaktovik Lagoon Deep Station 1), lat/lon coordinates, habitat type (river/ocean/lagoon), type (primary/secondary/river/ocean), lagoon (Elson East, Elson West, Stenfansson, Simpson, Kaktovik, Jago), and node (West/Central/East).

Use the function `add_cp_cols` from the R package `bleutils` to do this quickly on a R data.frame, assuming that it contains a column containing station codes.

Example usage: 

```r
# df is a R data.frame with "station" column containing station codes
df <- bleutils::add_cp_cols(df, "station")
```

#### Misc

- Data is "2018-ongoing" not "2018-2019" although we might only have 2018-2019 data as of publication. Except in EML's temporalCoverage where we actually specify begin and end dates.
- updateFrequency is annual
- pubDate is the latest year of publication/revision. E.g if data was originally published to EDI production in 2019, but revised 2020, pubDate is 2020. Note that EDI's auto-generated citation actually always reflect this, although EML might say otherwise.

*Why salinity is included in the pH package even though it is part of the CTD dataset*

Even though salinity isn't necessary to derive the final pH value from the raw data, and it was measured by an entirely separate sensor, it is probably the first thing an end-user will want to compare the pH data against so it would be very helpful to simply include this column to save someone having to find and merge the CTD data to the pH data.

We add a dataSource element in EML via metabase's DataSetMethodProvenance table to document this relationship. We also make explicit in the attributeDescription of the salinity column that these values are taken from the hydrography dataset.

*Why pH is packaged separately from hydrography*

- They require very different methods for calibration and QA/QC.
- pH data is novel and deserves its own package.
- Our pH measurements are not as geographically widespread as our hydrographic measurements.
- They are collected for different LTER sub-goals (hydrography main goal = understand hydrographic exchange. pH main goal = understand carbon dynamics).

<a id="pi-driven-datasets"></a>
### PI-driven datasets

Follow conventions set out by PI and edit sparingly when needed and when feasible. Most metadata conventions from the Core Program should still be followed to the most feasible degree.

The biggest difference between CP datasets/PI-driven/non-BLE funded datasets is the degree of attribution we give to BLE in the metadata. 

Generally, we give credit to BLE in these following places:

1. BLE is first creator, appears in citations (sole author in CP data)
2. The position of BLE information manager is listed as contact points for the dataset
3. BLE is listed as the parent project, along with our core personnel
4. Our LTER award is listed as the funding source
5. BLE is listed as the metadata provider

For non-BLE funded datasets, where we still archive the data, we skip 1, 3, and 4, and keep 2 and 5. This means removing any mention of BLE as a project in the creator + associated parties list, so only the people involved appear in the citation, and modifying the boilerplate to remove BLE project and funding information, and replace with appropriate copy (ask the PI for this). 

<a href="#header">Back to top</a>
<a id="website"></a>
# Website

<a id="our-website-technologies"></a>
## Our website technologies

Our website is built from static HTML pages and hosted with Netlify. There is no content management system (e.g. Drupal, Wordpress). In fact, there is no static website generator (e.g. Hugo, Jekyll) involved either.

Somewhat exhaustive list of website technologies we use:
- Netlify for hosting and deployment
	- Algolia X Netlify for search
- A Github repo as both production and development source code at https://github.com/BLE-LTER/LTER-website
- Bootstrap 5 for pre-cooked CSS and Javascript
- FontAwesome for icons
- Leaflet for maps
- Google Fonts for webfonts (Libre Franklin)
- Google Analytics for tracking usage
- Twitter embedded timeline
- YouTube for embedded videos
- Custom apps (see Tools we develop section):
	- Data Catalog built on PASTA API
	- Bibliography search interface
	- Search tool

<a id="how-to-update-website"></a>
## How to update website 

<a id="minor-content-updates"></a>
### Minor content updates

i.e. adding text or images to existing layout element in existing pages.

Open corresponding HTML file from the master branch and edit away. Each page might have different layout setup so it takes a bit of sleuthing to figure out where to add stuff if you're not familiar with it.

<a id="less-minor-updates"></a>
### Less minor updates

i.e. changing layout, styles or add new pages.

To change styling of existing layout elements:

- Experiment with devtools in whatever browser you're using. Or use inline style first. 
- When it looks good, migrate the styling to Bootstrap class, existing custom class, or add new class/id styling in `public/css/app.css`.
- Check out this Bootstrap4 all classes reference from W3schools too: https://www.w3schools.com/bootstrap4/bootstrap_ref_all_classes.asp. I used it a lot when trying to figure out if there's an already existing class that fits what I'm trying to do, or what a class Tim put in there does.

To add a new layout element:

- Hard to say anything generally applicable here.

To build/update search index:

- Start a node command prompt (or a regular command prompt if node is in your path).
- Browse to root `LTER-website` folder.
- Enter this command: `node build_index.js`.
- Cut and paste the resulting `lunr_index.js` file into the `public/js` folder.

To add a new page:

- Copy an existing page. Remember, the <head> element of all pages has to have the HTML comments `<!-- begin common head -->` and `<!-- end common head -->` in order for `apply_template.js` to work. So, creating a brand new, empty .html file will not work.
- Update header for new page (i.e. run `apply_template.js`).
- Edit page content as desired. Remember to remove the template page's existing content. 
- Add page to sitemap.xml.
- Update search index.

To change footer/header/common HTML `<header>` element:

- Edit `template.html` to include desired header, navigation, footer, etc.
- Start a node command prompt (or a regular command prompt if node is in your path).
- Browse to root `LTER-website` folder.
- Enter this command: `node apply_template.js`.

<a id="branding"></a>
## Branding

Currently (2020-01-08), we use a set of web-safe sans-serif fonts as an all-purpose font. After the website design update (some time before summer 2020), we'll use Libre Franklin (free webfont available through Google Fonts) for all copy. Libre Franklin is the approved sans-serif typeface alternative for UT Austin.

<a id="logo-color-reference"></a>
### Logo color reference
Colors as used in our official logo, RGB version:

ocean: 
- dark blue
	- hex #015cab
	- rgb(1, 92, 171)

- 1st lighter blue
	- hex #1e63af
	- rgb(30, 99, 175)

- 2nd lighter blue
	- hex #3170b7
	- rgb(49, 112, 183)

ice:

land:
- dark green
	- hex #51612b
	- rgb(81, 97, 43)

- 1st lighter green
	- hex #637724
	- rgb(99, 119, 36)

- 2nd lighter green
	- hex #798e36
	- rgb(121, 142, 54)

<a id="where-we-use-these-colors"></a>
#### Where we use these colors:

This pertains to the upcoming website redesign:

Ocean dark blue (#015cab) as primary "dark" background color. Use white text against it. Might also use as text color, preferably in bolded big heading text (font-weight 700 or above).

Land dark green (#51612b) as accent "dark" background color. Use white text against it. Might also use as text color but prolly only in very big bolded heading text.

### North Slope coastline motif

<a id="miscellaneous-website-notes"></a>
## Miscellaneous website notes

- Job postings need to include a diversity statement. See email communication from Ken circa Dec 2019. Example: Our BLE LTER program benefits from nurturing a culture of diversity. We encourage applications from potential students that are traditionally underrepresented to help us connect our research to the broader global community.

<a id="algolia"></a>
## Algolia

Here we document the nitty gritties of Algolia search on our website. 

#### Why we like it

We use it because of (1) automatic re-indexing triggered with every deployment of our website (a.k.a every push to the Github repository), (2) their instant search and fuzzy search feature.

#### How to make it work

First, go to https://github.com/algolia/algoliasearch-netlify/blob/master/docs/GettingStarted.md and read their getting started guide.

These are steps we need to do.

(1) Set up and indexing
- Install the Algolia plugin for Netlify. Note that this is done not on the Netlify GUI, but on a different website specifically for Algolia X Netlify. Follow the link and directions in the Github guide. You will need the appropriate Netlify login.
- Link up Algolia with the Netlify site you want. This is again done in the Algolia x Netlify site.
- Modify the Algolia plugin settings in the Netlify config file "netlify.toml". One finds this in the base directory of the website git repo. See https://github.com/algolia/algoliasearch-netlify/tree/master/plugin#available-parameters for the available parameters. The ones I've found most relevant: 
	- "pathPrefix". This should be the same as the Netlify "publish" directory, which in our case is "/public".
	- "customDomain". This matters a lot if you are on a fork or a branch, which means the URL you're checking is not our canonical ble.lternet.edu referred to in the sitemap and in HTML header canonicals, and will lead to lots of indexing failures. In which case, set this to "ble.lternet.edu". No "https".
	- "branches". Algolia can create different indices for different branches on the git repo, but it needs to be told specifically which ones. If you're experimenting on a different branch other than master, say "['master', 'yourbranchname']" and delete the latter once merged into master.
	- "template". This determines how Algolia will break up the index records. There are two options as of 2021-01-21: "default" and "hierarchical". The former will index by page, the latter by headings within a page. We chose the latter, since our website has comparatively few pages but a lot of information within each page.
- Check out and make sure the indexing of the website contents is to satisfaction. To do this, trigger a deployment of the Netlify site. Generally a new commit to the git repo will accomplish this, so consider doing this on a branch. Or alternatively trigger a deployment manually in the Netlify GUI, since you're most likely logged in for most of this anyway. Under the deployment log, if Algolia and Netlify have been linked up correctly, the log will give you a URL to the crawler records. Follow the link and check out the records. The "successful" count should roughly be equal to the number of distinct pages we have, plus one for the sitemap. Don't worry about the "ignored" category; my understanding is that Algolia does the indexing based on our sitemap, and it will look for common sitemap naming schemes; whatever doesn't work go into "ignored". 

(2) Incorporate Algolia into front end 

- Algolia has a plug-and-play front-end and this is what we use. It looks great, although the search result panel has a small, unobstrusive Algolia logo. Not ideal, but not bad. There is the option to write one's own front end.

- Copy the snippet of info Algolia gives you once you've linked Netlify with Algolia. It will look something like this, with the IDs and API key identifying our site.

```
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@algolia/algoliasearch-netlify-frontend@1/dist/algoliasearchNetlify.css" />

<script type="text/javascript" src="https://cdn.jsdelivr.net/npm/@algolia/algoliasearch-netlify-frontend@1/dist/algoliasearchNetlify.js"></script>

<script type="text/javascript">

  algoliasearchNetlify({

    appId: 'TCXC3S30W1',

    apiKey: '4192e022ca7324b819c06709a91b57e9',

    siteId: '84d8b51e-beb6-4843-bee0-a636ab45efe9',

    branch: 'master',

    selector: 'div#search',

  });

</script>
```

- Double check to make sure the IDs and API key are correct and refer to the appropriate Netlify page. There are two API keys Algolia will give you, the searchAPI is ok to put in public code, and the other is super not ok. Make sure it's not the latter in the snippet. If you copy from the site that risk is minimal. 

- Double check that the "branch" param in the snippet says the correct branch(es). Yes, the branches need to be specified in both the `netlify.toml` file and here.

- Edit the selector if needed.

- In our page template (`templates/template.html` in base git directory), copy and paste the first line into the HTML header. Copy and paste the `<script>` tag into the "end of body" div we have for scripts. 

- Add the selector (the default case is a div with a "search" ID attribute) where you want a search box to go in the template. We normally have it on the navbar.

- Run `apply_template.js` to apply the template.

- Git commit and push to trigger deployment. Check out your handiwork and adjust if needed.

#### Misc. observations and notes

1. Formatting headers

A nice feature of the "hierarchical" indexing is that once users select a search result from the drop-down result panel, they will be taken directly to the corresponding section. This is pretty neat. To make this happen, the underlying markers need to be in HTML source code. 

This indexing by Algolia relies on headings (`<h1>` to `<h6>` HTML tags). Each heading will need to have its own ID attribute. E.g. `<h1 id="title"> title </h1>`.

Keep this in mind when adding content.
  
2. Internal "SEO"

Think about logical breaks in content so that headings (and therefore searchable "sections") can be strategically placed. What will users search for on our site? The spots where headings are customarily placed in a page are a good start.

3. Commitments and usage limits

The free tier we get with Algolia and Netlify allows for 20 monthly "commitments". According to their website, a commitment equals to 1000 searches and 1000 records. We are probably not in any danger, but it is something to look out for. 
Algolia will also send usage reports to the email address associated with the Netlify page. This report details keywords used and their frequencies, etc., and whether there were any keywords that resulted in no hits. This latter especially would be useful to think about new content or SEO.

4. CSS mods

There are two minor modifications in CSS I made; otherwise we lifted their front-end wholesale. 

- min-width for the class ".aa-Form" was set to 250px, originally 150px. This is the search box.
- position for the class ".aa-Panel" was set to fixed, so that the search results panel does not disappear once we scroll down the page. 
- both needed the !important declaration to override Algolia's styling.




<a href="#header">Back to top</a>
<a id="bibliographic-management"></a>
# Bibliographic management

We use Zotero to manage our non-data publications.  BLE has a BLE-IM login for Zotero, and that login owns the LTER-BLE Zotero group.

<a id="zotero-best-practices"></a>
## Zotero best practices

See Zotero best practices here https://environmentaldatainitiative.files.wordpress.com/2019/04/zotero_best_practices.pdf. 

<a id="how-to-add-a-new-item"></a>
### How to add a new item

Easiest way is to use the Zotero connector, a browser add-on for Chrome/Firefox/etc, which can harvest metadata about a publication directly into the Zotero desktop application, saving you a lot of trouble.

1. If you have not already done so, install the Zotero desktop application, and also Zotero Connector. In the Zotero desktop application, sync to the [BLE library](https://www.zotero.org/groups/2211939/lter-ble/library).  Make sure you have write access to the library. Configure Zotero to not sync attachments.
2. Open the Zotero desktop application and click the LTER-BLE group to make it active. Zotero Connector will always save items to whatever library/collections you have open and have write access to.
3. In your Web browser, navigate to the Web page for the journal article (or book chapter, or what have you). 
4. Click the Zotero Connector button on the browser toolbar.

Once the metadata is harvested, make sure to:

- add the item to appropriate sub-collection under the LTER-BLE group library:
	- "For-Website" if item is to appear on publication page. These are primarily peer-reviewed journal articles but can include papers in conference proceeding as long as they are published in an edited volume.  What we are trying to avoid is listing a bunch of conference abstracts.
	- "For-Network" if item is to appear in the broad LTER network group library (see [instructions for contributing to the LTER group library](https://lternet.edu/lter-publications-and-products-instructions/))
- add appropriate custom tags (via Tags tab, right hand pane on Zotero desktop): 
	- LTER-Funded for work funded by BLE
	- LTER-Enabled - 1) pubs by BLE personnel that were enabled by the LTER but funded through other sources, 2) pubs by non-BLE personnel that were enabled by BLE through leveraging of logistical support, sample collections, etc., and 3) pubs by non-BLE personnel that use BLE datasets.
	- Foundational for work we are building our work on
	- LTER-BLE for work added to the For-Network collection
- add data URL if applicable to "Extra" field. URL **must** begin with "https://doi.org/"
- edit metadata fields as needed if Zotero wasnt able to fill them out
- skim the work for unpublished BLE datasets, and if any are found, work with the investigator to publish them (while you're at it, it wouldn't hurt to read the work and build your understanding of BLE science!)
- if your Zotero desktop application does not automatically sync to the library in the cloud, initiate a sync
- Update the BLE website. A cached copy of the bibliography harvested from Zotero is used for the website, so the cache must be updated each time an item is updated in our bibliography. To update the cache, use NodeJS to run the file harvest_zotero.js in the website root folder. This will update the file biblio_data.js in the public js folder. Git-commit and push to reflect changes onto the live website.

<a id="misc-notes"></a>
## Misc notes

The DOI field for entries should NOT start with "https://doi.org" but "10.XXXX". Otherwise, the Zotero API will pre-pend the former string resulting in duplication.

If you are adding a Core Program dataset as a Zotero entry (i.e. via using the Zotero browser button while on the EDI data portal), and the first author reads "Beaufort Lagoon Ecosystems LTER, Core Program" with the comma, then Zotero will read in "Core Program" as a first name. This would then lead to the exported citation possibly listing author "Beaufort Lagoon Ecosystems LTER, C. P.". To fix this, go to the entry details. Under the first author, remove "Core Program" from the first name field and paste it into the last name field. The rest of the metadata provided by EDI and extracted by Zotero is usually pretty good and needs no modifications. 

### Linking data and pubs

On the journal site: PIs would normally cite data packages. Not IM's job.

On our site bibliography: put each data DOI on its own line in the Extra field in Zotero. You must include the `https://doi.org/` part in order for the DOI to show up at as a data link on the website.

On EDI: use the portal "Journal citations" tool to manually add journal pubs to dataset landing page. Currently (2020-03-23) you must do this for each dataset revision on which you want the journal link to appear.

<a href="#header">Back to top</a>
<a id="personnel-management"></a>
# Personnel management

We do not yet have a dedicated tool for central personnel management beyond:

1. Tracking who's involved with which datasets in what role (so far for all datasets), during what years (this is done for Core Program datasets only). This takes place mostly in our metadata database (metabase). See section on Core Program personnel.

2. What's under "People" or "Team" on our website. This is edited manually when called for.

3. A Box spreadsheet for purposes of LTER/NSF reporting requirements and viewing by team members, stored under Beaufort LTER/Personnel. 

<a id="addupdate-personnel-contact-information"></a>
## Add/update personnel contact information

Make sure to do the following:

- Update the Box spreadsheet under Beaufort LTER/Personnel
- Update Marty Downs if appropriate
- Update our website display
- Update metabase in several places (lter_metabase."ListPersonnel" and mb2eml_r.boilerplate.project). They might not have an entry in metabase yet.
- Update appropriate mailing lists

<a id="mailing-list-admin"></a>
## Mailing list admin

We maintain several mailing lists for BLE LTER. Distribution and management are
based on [UTLists](utlists.utexas.edu), which in turn is based on Sympa
software. 

We have settled on these settings. However, see config section below if you ever wanna change.

Only list members can send messages. Messages are not moderated. Replies to messages from others will be sent to the entire list, i.e., default reply behavior is reply-all. Email the original poster directly for tangential thoughts, specific questions, etc. 

List members can invite others to join, but a list owner must approve once a
person has been invited. An Nguyen, Tim Whiteaker, Christina Bonsell, and Nathan McTigue own/admin the lists. No moderators are set, so mods are the same as owners. Note that owners are not necessarily subscribers. Owners/mods can always post to a group, but if they are not themselves subscribed, will not be included on conversations they didn't initiate. 

These are the lists as of June 2020:

1. [ble-lter-all@utlists.utexas.edu](ble-lter-all@utlists.utexas.edu)

Includes everybody: PIs, PMs, IMs, students, postdocs, affiliates (e.g. Amanda Kelley) and other project personnel (e.g. Stephanie Jump, Brandy Cervantes). Might exclude affiliates on a
case by case basis. 2020 PI meeting in Anchorage agreed on using a listserv like
this for potential paper and project discussions. 

2. [ble-lter-pi@utlists.utexas.edu](ble-lter-pi@utlists.utexas.edu)

Includes all PIs and Tim, who admins the list. Others can post messages to the list after moderation from an admin but would not see regular conversations. This is at the request of Ken Dunton and Jim McClelland so that potentially confidential messages do not circulate outside of PIs.

3. [ble-lter-student@utlists.utexas.edu](ble-lter-student@utlists.utexas.edu)

Includes all (and, per Ken and Jim, only) officially affiliated students. Others can post messages to the list after moderation from an admin but would not see regular conversations. This is so that people can post e.g. papers reading group or forwarded job ads, etc.

4. [ble-lter-staff@utlists.utexas.edu](ble-lter-staff@utlists.utexas.edu)

Includes staff (IMs, PMs, postdocs, and other project personnel, but generally not affiliates).

<a id="list-maintenance"></a>
### List maintenance

These tasks need to be done periodically:

- Review membership and subscribe/un-subscribe people manually as they join/leave the project. We might want to ask graduating students if they want to remain subscribed. In the future we might want to give people DIY instructions instead. E.g. point people to the UTlists webpage to subscribe or give them instructions how to subscribe via emailing sympa@utlists.utexas.edu. 

- Review for bouncing (invalid) addresses. 

- Check if messages are getting past spam filters. We'll assume the best and look into it if issues come up. 

- From August 2020 on, UTLists will delete mailing list archives that are more than 4 years old. Our mailing lists were created in September 2019. So, before September 1st 2023, old archives need to be downloaded. Unfortunately I don't know of any options to download them in a nice format besides UTLists' clunky way. 

<a id="list-config"></a>
### List config

Most of this is done at initial setup. Adjust as needed. Note that An also created and is admin on another list called [ble-lter-test@utlists.utexas.edu](ble-lter-test@utlists.utexas.edu) for config testing purposes; e.g. all subscribers are just me. 

For documentation, I've found that [this article collection from UChicago](https://uchicago.service-now.com/it?id=kb_article&kb=KB00016472) is more helpful that what UT offers. Both unis seem to have similar Sympa instances; the admin config options are named similarly. The UChicago articles expand on how different options behave. 

config options of note: 

- Who can post? 
	- @all: "Restricted to subscribers". We mostly want only members of any given list posting. Owners/admins/mods can always post. 
	- @student, @pi, and @staff lists: "Private, moderated for subscribers". Essentially means anyone who knows this address can post, but an admin needs to approve. We really only mean other BLE people not in respective lists to post there if they want, e.g. a faculty or staff member can post to the student list, etc. 

- Who can see the list? "Concealed except for subscribers". This means our lists do not show up publicly on the UTLists website.

- Who can (un)subscribe? "Owners approval". Admin needs to approve (un)sub requests.

- Include a footer message under "message templates". I go with variations on "Distribution list for BLE LTER *insert audience*. Replies will be sent to the whole group. Email *insert list email* to send a message to the group."

<a id="reporting"></a>
# Reporting

<a id="obtaining-metrics"></a>
## Obtaining metrics

### Data citations

We need a detective! The mystery: How to find where our data are cited.

a. Google scholar detects automated scraping and bans IPs. The current workaround is to pay for a proxy service that spawns our requests across a gazillion servers/IPs (one example here), but that is not honoring Google's policy so we (BLE) won't do that.

b. Matt Jones suggested scythe, which I gather scrapes other sources.

c. I also wonder since "Beaufort Lagoon Ecosystems LTER" appears amongst author names for every dataset, if we could just search once for that manually, and then have some code to parse the results.  It should be a partial match, since we also have "Beaufort Lagoon Ecosystems LTER, Core Program" as an author.

d. Or we could just manually search Google Scholar for every DOI associated with every revision of every BLE dataset. Ugh. This is the baseline result, which we'll use to evaluate the effectiveness of other approaches.

How to get every DOI associated with every revision of every BLE dataset: one of counter's two result spreadsheets will give you this, see below. 

### Data downloads

From discussion with EDI and other IMs, it seems data download counts are most likely inflated measures of data usage. Several factors confound these numbers: robots, repository routines (e.g. checksum checks), etc. 

Bits of wisdom:
- Download counts overcount but citations undercount (and lag behind data publication), so the truth of data reuse is somewhere in between.
- Impossible to at the same time have data be entirely public and require no credentials to download, and have accurate reporting of how many people have downloaded it and who they are. Trade-off.

I've been getting data downloads from the PASTA counter library: https://github.com/PASTAplus/counter. Without custom params, the time period would be from 2013 (when PASTA started and way before BLE) to today (the date you run the program).

The counter library reports download counts by data entities, and sums of all entities for a package. For reporting purposes, these are the numbers we'll use if needed. The Arctic Data Center reports that their downloads are the same as PASTA's and the same as DataONE, so there is no need to add up numbers.

<a id="presentations"></a>
## Presentations

### BLE powerpoint template

By request from PIs in the 2020 BLE meeting, we created a BLE powerpoint template for use by all project members. There were a number of issues I didn't foresee that came up when this template was first distributed and used by many during the lead-up to our 2021 meeting. 

- Fonts: older versions of PowerPoint on Mac cannot read PowerPoint files made on Windows with embedded fonts, which we did use to include the Libre Franklin family of fonts. Yvette Spitz reported that even updating PP didn't solve this issue. To circumvent this, I swapped text in Libre Franklin to Arial, which is available most everywhere. An easy way to do this (which I only found out after the fact) was to go to Replace/Replace Fonts in PP.
- Color usage: Yvette Spitz brought up that colors used in the presentation should be tested for color-blind user friendliness. It wasn't a big issue in this particular instance, since we didn't have colors next to each other that needed to be interpreted, but we also switched out the blue and green to be darker to enable more contrast.
- Aspect ratio: Ken Dunton brought up that some projectors are in 4:3 ratio while the template is 16:9. Tim clarified that this will only mean black bars above and below. 

