---
title: BLE LTER Information Management Handbook
subtitle: Everything, including the kitchen sink
author: An T. Nguyen and Tim Whiteaker -- BLE-LTER Information Managers
date: 2020-03-20
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
- [Metadata database](#metadata-database)
	- [Installation and admin](#installation-and-admin)
	- [Our metabase implementation](#our-metabase-implementation)
	- [Regular tasks](#regular-tasks)
- [Metadata template](#metadata-template)
	- [How to update template](#how-to-update-template)
- [Data processing](#data-processing)
	- [How to initiate a new data package](#how-to-initiate-a-new-data-package)
	- [Processing](#processing)
- [EML](#eml)
- [Data archiving](#data-archiving)
	- [Where we archive](#where-we-archive)
	- [Who does the archiving](#who-does-the-archiving)
	- [How we archive at EDI](#how-we-archive-at-edi)
- [Core Program quirks](#core-program-quirks)
	- [Personnel / Responsible Parties](#personnel--responsible-parties)
	- [Stations](#stations)
- [Data and metadata styling guide or style rules](#data-and-metadata-styling-guide-or-style-rules)
	- [Core Program](#core-program)
	- [Other datasets \(PI-driven datasets in BLE terminology\)](#other-datasets-pi-driven-datasets-in-ble-terminology)
- [Website](#website)
	- [Our website technologies](#our-website-technologies)
	- [How to update website](#how-to-update-website)
	- [Branding](#branding)
	- [Miscellaneous website notes](#miscellaneous-website-notes)
- [Bibliographic management](#bibliographic-management)
	- [Zotero best practices](#zotero-best-practices)
	- [Misc. biblio notes](#misc-biblio-notes)
- [Personnel management](#personnel-management)
	- [Mailing list admin](#mailing-list-admin)
- [Resources](#resources)

<!-- /MarkdownTOC -->


<a id="front-matter-issues"></a>
# Front matter issues

<a id="introduction-to-ble-lter-information-management"></a>
## Introduction to BLE LTER Information Management

Beaufort Lagoon Ecosystems (BLE LTER) is a new site and member of the Long Term Ecological Research Network. The project was first funded in 2017 as one of three sites newest to the network. 

Information management was integral to the project from the start; our NSF proposal included a detailed section on the data types we will produce and how each of them will be treated. The information management team has been important project members ever since.

Tim Whiteaker (Tim after) was first recruited as project data/information manager by lead project PI Ken Dunton from the 2017 beginnings. An T. Nguyen (An after) was recruited by team in November 2018 and officially started in March 2019.

<a id="our-philosophies"></a>
## Our philosophies

We use modular components in our IM system and workflow -- as opposed to a comprehensive solution like [DEIMS](https://deims.org/). We try to use existing solutions whenever possible and not modify them willy nilly; we've found that there's almost always a tool somewhere suited to our purposes even in its vanilla form.

See our website summary on our information management system here at https://ble.lternet.edu/ims.

<a id="preamble"></a>
## Preamble

I speak in first person throughout this handbook. Writing in third person, passive, or imperative voice is tiring.

<a id="tools"></a>
# Tools

<a id="tools-we-use"></a>
## Tools we use

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

a.k.a. primitive personnel handover action plan

We use many, many tools that will need logins, some needing certain privilege levels. A new person on BLE's IM team will need to make sure they have access to:

- Stache `*`
- UTBox (shared drived with BLE team as a whole, we also use this for  sharable file links) `+`
- Austin Disk (more day-to-day IM working directories) `*`
- Access to the official IM email BLE-IM@utexas.edu address `+`
- Access to our copy of metabase `*`
- Netlify (static website host) `$`
- Collaborator to the BLE-LTER Github organization
- Editor on Zotero group library
- EDI's three portals: production, staging, and development
- UTLists (Sympa mailing list management software) `+`
- Slack groups for LTER IMs (at https://lter.slack.com). Optional: EDI/NCEAS groups. 
- Subscribe to the im@lternet.edu mailing list, plus imc@lternet.edu if main IM
- Taskade (project management app, we're trying it out as of Feb 2020)

Legend:

`*` UT Austin service, requires affiliation to UT (UT EID)

`+` UT Austin service, does not require affiliation to UT

`$` Tim has it

Most of these are individual accounts and each IM team member manage their own, however some accounts are shared between the BLE IM team as a whole. The most important is the PASTA 'BLE' account under 'LTER' affiliation. Only this account can upload new or revised data packages with the "knb-lter-ble" scope. All three EDI portals (production, staging, and development), plus the corresponding LTER ones, share the same authentication system, and so we log on to all of them with the same credentials. EDI will eventually roll out 'identity mapping', i.e. allowing IM team members from sites to log on to EDI portal(s) with their own Google/Github/ORCID account. Until then, BLE has one account.

Tim and An have their own individual accounts to metabase. However there are accounts set to do certain things (e.g. 'backup_user' has read-only access to be able to dump database contents everyday). 

Stache (UT service) contains the passwords to these shared accounts. 
For other things that are individual-based, a nem IM team member will need to be granted access and/or admin rights. 

#### Getting remote access

March 18th, 2020. UT has shut down for five days. Austin is on the verge of an imminent lockdown. BLE IM team has been stuck at home for five days. We set down these words to commemorate these times.

How to remote access into your desktop from 

<a href="#header">Back to top</a>
<a id="metadata-database"></a>
# Metadata database

See https://github.com/LTER/lter-core-metabase for a first stop documentation on LTER-core-metabase as a product and a project. This section in the handbook primarly concerns usage of metabase at BLE and certain issues I've encountered.

<a id="installation-and-admin"></a>
## Installation and admin

### Postgres woes and how to overcome them

Very verbose -- for complete newbs to the DB admin world. Windows specific, but I think once you get an idea of how the pieces get together, operating system doesn't matter as much.

Assuming a vanilla installation from executable (.exe) on Windows. Some assumptions might not apply in other scenarios (e.g. where the default data directory is). 

**NOTE:** A good chunk of trouble might be avoided if PostgreSQL is _not_ installed in C:\Program Files. This folder is write-protected in many work PC systems where you are not the admin, and generally quite inaccessible in many ways. Change the directory during the installation process. 

<a id="issues-ive-run-into"></a>
### Issues I've run into

<a id="serverservice-not-running"></a>
#### Server/service not running
One day as fine as any other, you log on to your computer and open up DBeaver ready to do some ecological data management. The database refuse to connect, citing "Connection to localhost:5432 refused. Check that the hostname and port are correct and that the postmaster is accepting TCP/IP connections." Boom. What's happening? 

This normally means the server associated with the Postgres instance aka cluster (see below) that your database lives on is not running. In my experience, the default cluster is normally set to auto-start its server at system startup; this is not true for other clusters.

How to start a Postgres server:

Go to Command Prompt. Navigate with `cd` to the directory with all the nifty Postgres programs, generally under <directory you installed Postgres into>\PostgreSQL\<version number>\bin. Now call `pg_ctl` with option `- D <path to your directory>` then `start`. Similarly you can also call `stop`. 

What if this doesn't work:

Does it say permission denied anywhere in the cmd log? Is your data directory in Program Files? It's time to change it. 

Follow these directions since it is fairly comprehensive (while everything else here is bits and pieces from stackoverflow): [see here.](https://radumas.info/blog/tutorial/2016/08/08/Migrating-PostgreSQL-Data-Directory-Windows.html)

Do all of the clusters fail to start? I have at least two clusters on my computer thatr 

<a id="how-to-set-up-remote-connection-to-locally-hosted-postgres-database-on-windows"></a>
### How to set up remote connection to locally hosted Postgres database on Windows

<a id="1-general-things-you-need"></a>
#### 1. General things you need
You need:
- To know the IP addresses of both the server and client machines, aka the PCs hosting the database and the PC trying to access it. This might mean a public-facing address or an internal one. Consult whoever is the network admin, since you'll need to talk to them by the end of this guide anyway. 
- To have set up a user and password with at minimum CONNECT rights to the database in question.

<a id="2-on-the-server-pc"></a>
#### 2. On the server PC

##### Figure out where the data "cluster" is

A Postgres data cluster is a separate instance of Postgres. There can be multiple clusters on the same server/machine. Each cluster lives in its own data directory, can be configured differently, contain separate sets of databases, and uses a different "server" and port. Note that the Postgres "server" is different from the machine server, and I lack the understanding to elaborate further.  

When you install Postgres on Windows, the default cluster is located in C:\Program Files\PostgreSQL\<pg version number>\data. Look there. This location changes depend on where you installed PostgreSQL for the first time. This default cluster will use the port 5432.

You might want to either change the default cluster directory, or create a new cluster in a different directory (via the command line , for these reasons:

- You might not have write access in C:\Program Files. This is the case with me.
- You might want to host it somewhere, of course. I briefly looked into hosting a cluster on the UT-Austin network file server, but decided against this route because (1) this seems to be a BAD IDEA(tm) reliability-wise in the DB admin world, and (2) it is unclear to me what the host to the cluster would then be. 

Proceed only once you know where the cluster in which your database resides is, and what is the port the cluster uses.

##### Change the cluster configuration
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

##### Change firewall rules to open port
Now that we're done telling Postgres to expect and allow connection, we need to tell the operating system the same. Create a Windows Defender Firewall inbound rule to open up port TCP 5432, or whatever port your cluster uses. Enable this rule. Contact your network admin if you can't do this or don't have the right to do so. This is likely the case if you see anything that says "group policy".

<a id="on-the-client-pc"></a>
#### On the client PC
Use this connection information:

Host: <server IP address>
Port: <cluster port>
Database: <your database name>
User: <your username>
Password: <your password>

<a id="our-metabase-implementation"></a>
## Our metabase implementation

We're using a Postgres instance on An's machine (IP address 10.157.18.129, computer number for UT-IT purposes CRWR-D08182).

To connect:
Host: 10.157.18.129
Port: 5432
Database: ble_metabase
User:
Password:

To enable Tim to connect, we had to work with ITG. They set up a firewall policy
for An's computer which opens TCP port 5432 for just the CWE general network
(10.157.18.0/24). They then ran a gpupdate on An's computer.

### Roles: Users/Groups || Permissions

Postgres has a somewhat confusing (to me) permission management scheme. To minimize confusion and make it easy, I am making a hard-and-fast distinction:

1. LOGIN ROLES (i.e. users):

- can login: you have to use a login role's credentials to initially connect to a database. Login roles need to be created with passwords.
- are associated conceptually with ACTUAL PEOPLE or TASKS to be performed on the database.
- to be able to perform said tasks, login roles _inherit_ permissions from the groups they are a member of.
- if other people joins the team, or webapps that use the database are developed, a new login role should be created for their use, with membership to the appropriate groups.

2. GROUP ROLES:

- cannot login: you can not use a group credential to make the initial connection to a database. It follows that group roles do not have passwords. To grant membership to a group role, the logged in user has to be an admin of the group role, so this is not a security loophole. 
- are associated conceptually with PERMISSIONS on the database. Permissions to the database are granted on a group basis for easy management.
- there are three groups corresponding with three broad levels of permissions. I do not foresee needing another group role.
  - `ble_group_readonly` has CONNECT, USAGE, and SELECT
  - `ble_group_readwrite` has all of the above, plus INSERT and UPDATE
  - `ble_group_owner` has all of the above, plus (1) ability to GRANT membership in group roles

#### Existing structures

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

**NOTE**: postgres is the superuser on the entire cluster on An's machine. Do not use for mundane tasks, especially creating new objects (tables/roles/databases), since it then becomes the default owner and it's quite a hard task to revoke ownership from its clutches.

### User privileges needed to connect to and edit the database

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

<a id="add-ons-to-vanilla-metabase-that-are-specific-to-ble"></a>
### Add-ons to vanilla metabase that are specific to BLE

1. Addition of two year columns to DataSetPersonnel

After deciding to eschew listing people as creators in core program datasets, we settled on a solution to include a separate data table (a separate data entity in EML terms) listing personnel and their years associated with a dataset, while still listing the same list, only sans year, as associated parties in EML. This practice now requires a few modifications to our instance of LTER-core-metabase. Normally we refrain from deviating from the vanilla version of LTER-core-metabase, since the "vanilla" version of the schema archived at https://github.com/LTER/lter-core-metabase. Here we archive the SQL code we used, in case we ever need to restart our metabase from an install of the vanilla. The file `add_yearspan_to_DSpersonnel.sql` contains the SQL and also reproduced below.

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
## Regular tasks

### Data sets

### Backups

#### Backups

A scheduled task on An's computer backs up the database to the **daily_backups**
folder once per day and logs the standard output and error (stdout & stderr) in **daily_backups/logs**. The task also copies the backups to An's Box Sync folder, which gets auto-synced to the cloud, wherever that is. Yay for multiple backups to multiple servers!

Reminders for a smooth backup experience: disconnect from the database (in DBeaver: right-click database name/Disconnect) and quit DBeaver when not using it.

#### Restore

Backups are made in plain-text SQL format. This means we can open it in a text editor and just, you know, look at it. This also means we cannot use the pg_restore tool or restore via right-click on a database in DBeaver/Tools/Restore. To restore from plain-text format, either right-click on a newly created database in DBeaver/Tools/Execute script, or run the file on a newly created and connected to database in command-line psql.

Existing users must be created prior to running the SQL to restore into another
server that's not the original host. It is less work to create new users than make a backup
without user privileges then assign them.

``` sql
CREATE USER ble_group_owner;
CREATE USER read_write_user;
CREATE USER read_only_user;
CREATE USER backup_user;
CREATE USER tim;
CREATE USER an;
```


### Applying new features or patches

Remember to log in with a user in group ble_group_owner when changing the schema. This simplifies permission issues downstream, such as when granting default privileges for new tables to other users.

Keep an eye on the LTER-core-metabase Github repository. "watching" the repo will trigger email updates. An currently develops for this project, so by default keeps up with new patches and in fact wrote a lot of them. The "migration" branch will contain the latest sequentially numbered patches, see documentation on that repo for information on this system. Check the table `pkg_mgmt.version_tracker_metabase` for information on past applied patches. Note that occasionally new "one big file/OBF" or essentially a schema dump with all patches incorporated. If BLE instance of metabase has fallen too far behind, instead of applying a whole lot of patches, you might want to consider setting up a new instance from the latest OBF, dump out data from the old metabase, and insert into the new. 

Once you've determined that a patch needs to be applied:

- inspect it. If there are new GRANT statements involved, these changes are necessary: `%db_owner%` to `ble_group_owner`, `read_write_user` to `ble_group_readwrite`, and `read_only_user` to `ble_group_owner`. 
- either:
	- download the .sql patch, make changes, make sure the BLE metabase is the active DB in DBeaver (right click > make active), then right click > execute script.
	- copy the raw SQL code into a new SQL editor window in DBeaver, make changes, then execute line by line or Ctrl+A > Ctrl+Enter to execute the whole thing.
 
<a href="#header">Back to top</a>
<a id="metadata-template"></a>
# Metadata template

We use a metadata template to collect information about datasets from scientists. It resides at, well, several places. 

On Box, we keep a zip and publishes it on a stable link https://utexas.box.com/v/ble-metadata-template. This zip should always be updated to the latest canon version.

Austin Disk is where we keep the canon version: under BLE LTER > Data-notes > BLE practices > metadata_template > canon. This itself is a git repo at https://github.com/BLE-LTER/ble-metadata-template for version control purposes.

<a id="how-to-update-template"></a>
## How to update template
This is a copy of the README on the git repo with a tiny bit more.

### Template Excel

1. Open file `metadata_template.xlsx`
2. Make changes. Make changes to sample package if applicable. Make changes to instructions if applicable.
3. Save file(s)
4. See common steps.

### PDF instructions

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
### Common steps after editing

After any updates, be sure to:
- Git commit and push changes
- Zip template package up, be sure to include:
	- Excel
	- PDF
	- sample package
- Save to Box > Beaufort LTER > Website > FileLinks > "metadata_template.zip". Using that exact archive name will ensure links and version control work.

<a href="#header">Back to top</a>
<a id="data-processing"></a>
# Data processing

<a id="how-to-initiate-a-new-data-package"></a>
## How to initiate a new data package

Run `bleutils::init_datapkg(*insert dataset_id*, *insert dataset nickname*)` in any R console. This will (1) create a folder named datasetid_nickname under our Austin disk Data folder, with sub-folders called FromPI and Clean > EML_generation, and (2) create a R script named datasetid.R from template with the appropriate IDs subbed into function calls. The parent folder defaults to "K:/Data" on my machine. Modify the `base_path` argument in `init_datapkg()` if needed.

- Our dataset IDs increment from 1. `init_datapkg()` will return error if you attempt to use an ID already existing within that folder, and tell you the next available ID (i.e. the largest existing ID + 1). I don't see any reason right now to skip numbers, so this should work. 

- I do this fairly early on in the process: normally, as soon as PI have sent us a file somewhere, even if it's a sample with no metadata, since we know there's data coming at some point. I do not enter any information into metabase until we receive complete good quality metadata.

- Create a new R project under EML_generation for easy project management. I looked into how to automate this with `init_datapkg()`, no dice so far.

<a id="processing"></a>
## Processing

All data processing should be performed in scripts for transparency and reproducibility, and also for our convenience: PIs often re-send data, and all changes by us made manually in Excel will be lost. I use R and therefore a lot of our workflows and helper functions are centered around R, but there's no reason another scripting language would not work. 

The R script created by `init_datapkg()` has pre laid-out sections (but no code, can't template processing code) for light data processing. For tasks beyond renaming columns or fixing small typos, I would create a new script.

### netCDF

#### When to use

Gridded data with lots of observations can be packaged a lot smaller in netCDF than CSV form. Generally, we do this when a CSV would exceed circa 20 million rows and 5/6 columns in long table form, resulting in a CSV file > 1 GB. Remember that lat/lon/time/site codes already take up 3-4 columns.

netCDF cannot be checked for data-metadata congruency by PASTA's ECC.

#### How to generate netCDFs

This of course depends on the source format. We have done and attempted to do this twice as of March 2020 for datasets 5 (hydrology model by Mike Rawlins) and 7 (moorings by Jeremy Kasper) and have some insights.

- R and Python can both handle these tasks. Use package `ncdf4` in R and module `netCDF4` in Python. In our folder for dataset 7, see merge_nc.py for an example python routine and 
netcdf.R for an example R routine. 

- Execute the conversion on local storage, not Austin disk. A network drive dramatically slows these packages down by as much as 100 times. Our python routine that takes 6 seconds on local disk takes 650 seconds on Austin disk. The equivalent R routine that takes 5 minutes on local disk takes, well, I never stuck around long enough to see if it can even execute to completion, but at least 2 hours. Yes, R is quite a bit slower than python. I still use it.

- Mike's dataset used the EASE-grid, on a Lambert azimuthal projection. We had a lot of trouble configuring the netCDF file so that ArcGIS would pick up the EASE-grid. For more documentation on what we did, see folder Data > 5_rawlins > netcdf.

### Metadata 

#### in netCDF

We strive to make the netCDFs self-contained with complete metadata on their own. This might mean duplicating metadata already in EML, even if the netCDF will be packaged with EML. 

Our goal for netCDFs:

- Compliance with CF conventions

- Compliance with the applicable NCEI netCDF template. See list of templates [here](https://www.nodc.noaa.gov/data/formats/netcdf/v2.0/). 

- Opens in ArcGIS with correct projection and correct location (i.e. ArcGIS recognizes the CRS plus the lat/lon values).

Possible metadata duplication between EML and netCDF global attributes:

- title: use overall dataset title
- summary: use overall dataset abstract
- keywords: use keywords applicable to data in netCDF form (assuming there are other data entities packaged alongside netCDF)

#### in EML

Document the netCDF as otherEntity. Metabase already has netCDF as a file type that would fill in the correct metadata.

<a href="#header">Back to top</a>
<a id="eml"></a>
# EML

<a href="#header">Back to top</a>
<a id="data-archiving"></a>
# Data archiving

<a id="where-we-archive"></a>
## Where we archive

We archive most data packages at the Environmental Data Initiative (EDI).  The
exception is for entities for which a more suitable archive already exists, such
as GenBank for genomics data.

Because we use EDI as the sole source of our online data catalog, we still
archive in EDI at least a summary table for externally archived datasets such as
genomics data.

<a id="which-member-node-are-we"></a>
### Which member node are we

When signing in to the EDI data portal and asked for a member node, we're urn:node:LTER.  EDI filters on the package identifier (knb-lter-ble): any of the "knb-lter-[site acronym]" packages go through urn:node:LTER, while the rest go through urn:node:EDI.

<a id="replication"></a>
### Replication

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

<a id="why-we-archive-at-edi"></a>
### Why we archive at EDI

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
## Who does the archiving

The BLE information manager archives data packages at EDI. For entities that are
not archived at EDI, such as genomics data going to GenBank, the individual
researcher typically archives that entity, since they probably are already
familiar with the archives for their field.

<a id="how-we-archive-at-edi"></a>
## How we archive at EDI

We currently submit data and EML metadata manually via the [EDI data portal](https://portal.edirepository.org/nis/harvester.jsp).

<a id="handling-large-files"></a>
### Handling large files

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

<a href="#header">Back to top</a>
<a id="core-program-quirks"></a>
# Core Program quirks

<a id="personnel--responsible-parties"></a>
## Personnel / Responsible Parties

<a id="creator"></a>
### Creator

Core Program packages only have one creator with only a surname "Beaufort Lagoon Ecosystems LTER, Core Program". See the entry in metabase with NameID "blecreator-core". This is in order to generate citations in this form: 

> Beaufort Lagoon Ecosystems LTER, Core Program. 2019. Stable oxygen isotope ratios of water (H2O-d18O) from coastal river, lagoon, and open ocean sites along the Beaufort Sea, Alaska, 2019-ongoing. Environmental Data Initiative. https://doi.org/DOI_PLACE_HOLDER. Dataset accessed 12/04/2019.

So that they are analogous to this citation from a PI-driven dataset (see comm. with Ken/Jim October/November 2019):

> Beaufort Lagoon Ecosystems LTER, V. Lougheed. 2019. Carbon flux from aquatic ecosystems of the Arctic Coastal Plain along the Beaufort Sea, Alaska, 2010-2018. Environmental Data Initiative. https://doi.org/DOI_PLACE_HOLDER. Dataset accessed 12/04/2019.

<a id="other-people"></a>
### Other people

Other people involved in the dataset will be credited as an associated party in the EML record. The order might still matter, so order as the PI have written them down in the template. To be listed as an associated party, a person has to have handled/been responsible for the data at some point, so as to be able to answer questions if necessary. The PI supplies this list normally, so not an action item for us, just FYI. 

In addition to listing people as associated parties in EML, we will include a personnel table as a data entity. This table will essentially have the same information as the EML entries, but also include years of involvement in this role with the dataset so that data users can track down appropriate people to ask about specific periods in the dataset. We use an add-on to vanilla metabase to keep track of people and years (see section BLE add-ons to vanilla metabase). 

To generate a CSV table once metabase is populated, use the R function 

`bleutils::export_personnel` 

This function takes care of querying metabase for the specified dataset ID, and spits out a ready made personnel CSV. Rough naming convention is `BLE_LTER_[dataset nickname]_personnel.csv`. 

I call this function from inside the directory with other data files. I list the personnel entity last in metabase: e.g. if there are five actual data entities, the EntitySortOrder for the personnel table is 6. Note that due to a MetaEgress quirk, all dataTables will be listed before all otherEntities. 

Remember to list the seven columns of the personnel CSV in DataSetAttributes. Easiest way to duplicating the same set of attributes from a previous Core Program dataset. 

<a id="stations"></a>
## Stations

Core Program sampling makes use of a certain number of fixed stations. Normal practice for PIs in their data is to include station codes (e.g. KALD1). For Core Program datasets and most other datasets where this is applicable, I make it a practice to include contextualizing columns in the same data table. These include: station name (KALD1 is Kaktovik Lagoon Deep Station 1), lat/lon coordinates, habitat type (river/ocean/lagoon).

Use the function `add_cp_cols` from the R package `bleutils` to do this quickly on a R data.frame, assuming that it contains a column containing station codes.

Example usage: 

```r
# df is a R data.frame with "station" column containing station codes
df <- bleutils::add_cp_cols(df, "station")
```

<a href="#header">Back to top</a>
<a id="data-and-metadata-styling-guide-or-style-rules"></a>
# Data and metadata styling guide or style rules

Refer to BLE as either "Beaufort Lagoon Ecosystems LTER" or "BLE LTER". Avoid using just "BLE" except when talking to other LTER people, as it's without context, and avoid the hyphenated form "BLE-LTER". 

<a id="core-program"></a>
## Core Program

- Column names
	- lowercase (station not Station)
	- capitalized only when denoting standard acronyms (PAR for photosynthetically active radiation) or when it's part of the variable name (pH)
	- underscores between words (date_time not date.time)

Some standard columns
	- station: station codes or IDs (KALD2)
	- date_time: date and time in YYYY-MM-DD hh:mm:ss or YYYY-MM-DD hh:mm format. Normally applies to instrument data. Exception is when archiving raw data (see dataset ID 3, hydrography), then another date time format might be ok.
	- date: date in YYYY-MM-DD format. Normally applies for sampling trips. 
	- water_column_position: surface/mid-column/bottom/not_applicable where not_applicable is a missing value code and used in river or other non-stratified stations.

Entity names
	- Include variables in data
	- Include timeframe to year resolution
	- Do not include "BLE LTER"
	- Example: Dissolved organic carbon and total dissolved nitrogen, 2018-ongoing

Data table entity descriptions
	- Include variables in data
	- Include timeframe to year or month resolution
	- End with some variation to the effect of "from BLE LTER Core Program, [month and year this dataset starts]-ongoing"
	- Example: Dissolved organic carbon and total dissolved nitrogen from BLE LTER Core Program sampling, Aug 2018-ongoing
	- If raw data or some other variation of data, prepend designation to description of finished data. E.g. Raw data: Dissolved organic carbon and total dissolved nitrogen from BLE LTER Core Program sampling, Aug 2018-ongoing

Other entity descriptions:
	- State clearly what the other entity is and how it relates in the context of the package. No need for month and year, I think.
	- Example: Annotated RMarkdown script to process, calibrate, and flag raw TCM data.

File names:
	- underscored
	- Prepend with "BLE_LTER"
	- Then one or two word descriptive moniker for data
	- Example: "BLE_LTER_CTD.csv"
	- I used to add the timeframe to filenames, e.g. "BLE_LTER_CTD_2018_ongoing.csv" but on reflection I do not think this is necessary. 

<a id="other-datasets-pi-driven-datasets-in-ble-terminology"></a>
## Other datasets (PI-driven datasets in BLE terminology)

Follow conventions set out by PI and edit sparingly when needed and when feasible.

<a href="#header">Back to top</a>
<a id="website"></a>
# Website

<a id="our-website-technologies"></a>
## Our website technologies

Our website is built from static HTML pages and hosted with Netlify. There is no content management system (e.g. Drupal, Wordpress). In fact, there is no static website generator (e.g. Hugo, Jekyll) involved either. 

Somewhat exhaustive list of website technologies we use: 
- Netlify for hosting and deployment
- A Github repo as both production and development source code at https://github.com/BLE-LTER/LTER-website
- Bootstrap 4 for pre cooked CSS and Javascript
- FontAwesome for icons
- Leaflet for maps
- Google Fonts for webfonts (Libre Franklin)
- Google Analytics for tracking usage
- Twitter embedded timeline
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

To add a new page:

To change footer/header/common HTML `<header>` element: 
- Edit `template.html`. Run `public/js/apply_template.js` with NodeJS to apply the change to all HTML files in the `public` folder. I do this in Windows' Command Prompt:

Assuming NodeJS is installed and in the system PATH. First we navigate to the `public/js` folder then simply
```
node apply_template.js
```

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

- Job postings need to be include a diversity statement. See email communication from Ken circa Dec 2019. Example: Our BLE LTER program benefits from nurturing a culture of diversity. We encourage applications from potential students that are traditionally underrepresented to help us connect our research to the broader global community.

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
- Update the BLE website (a cached copy of the bibliography harvested from Zotero is used for the website, so the cache must be updated each time an item is updated in our bibliography)

<a id="misc-biblio-notes"></a>
## Misc. biblio notes

### Linking data and pubs

On the journal site: PIs would normally cite data packages. Not IM's job.

On our site bibliography: put each data DOI on its own line in the Extra field in Zotero. You must include the `https://doi.org/` part in order for the DOI to show up at as a data link on the website.

On EDI: use the portal "Journal citations" tool to manually add journal pubs to dataset landing page. Currently (2020-03-23) you must do this for each dataset revision on which you want the journal link to appear.

<a href="#header">Back to top</a>
<a id="personnel-management"></a>
# Personnel management

We do not yet have a dedicated tool for centrally personnel management beyond 

1. Tracking who's involved with which datasets in what role (so far for all datasets) during what years (Core Program only). This takes place mostly in our metadata database (metabase). See section on Core Program personnel.

2. What's under "People" or "Team" on our website. This is edited manually when called for.

3. A Box spreadsheet for purposes of (I surmise) LTER/NSF reporting requirements. 

<a id="mailing-list-admin"></a>
## Mailing list admin

We maintain several mailing lists for BLE LTER. Distribution and management are
based on [UTLists](utlists.utexas.edu), which in turn is based on Sympa
software. 

We have settled on these settings. However, see config section below if you ever wanna change.

Only list members can send messages. Messages are not moderated. Replies to messages from others will be sent to the entire list, i.e., default reply behavior is reply-all. Email the original poster directly for tangential thoughts, specific questions, etc. 

List members can invite others to join, but a list owner must approve once a
person has been invited. An Nguyen, Tim Whiteaker, Christina Bonsell, and Nathan McTigue own/admin the lists. No moderators are set, so mods are the same as owners. Note that owners are not necessarily subscribers. Owners/mods can always post to a group, but if they are not themselves subscribed, will not be included on conversations they didn't initiate. 

There are three lists as of Feb 2020:

1. [ble-lter-all@utlists.utexas.edu](ble-lter-all@utlists.utexas.edu)

Includes everybody: PIs, PMs, IMs, students, postdocs. Excludes affiliates on a
case by case basis. 2020 PI meeting in Anchorage agreed on using a listserv like
this for potential paper and project discussions. Since potential works could be
discussed, this list is limited to BLE people only.

2. [ble-lter-pi@utlists.utexas.edu](ble-lter-pi@utlists.utexas.edu)

Includes all PIs, IMs, and project managers.

3. [ble-lter-student@utlists.utexas.edu](ble-lter-student@utlists.utexas.edu)

Includes all officially affiliated students. PIs/PMs/IMs can post messages to the list but would not see regular conversations. This is so that PIs can post e.g. papers reading group or forwarded job ads, etc.

<a id="list-maintenance"></a>
### List maintenance

These tasks need to be done periodically:

- Review membership and subscribe/un-subscribe people manually as they join/leave the project. We might want to ask graduating students if they want to remain subscribed. In the future we might want to give people DIY instructions instead. E.g. point people to the UTlists webpage to subscribe or give them instructions how to subscribe via emailing sympa@utlists.utexas.edu. 

- Review for bouncing (invalid) addresses. 

- Check if messages are getting past spam filters. We'll assume the best and look  into this as issues come up. 

<a id="list-config"></a>
### List config

Most of this is done at initial setup. Adjust as needed. Note that An also created and is admin on another list called [ble-lter-test@utlists.utexas.edu](ble-lter-test@utlists.utexas.edu) for config testing purposes; e.g. all subscribers are just me. 

For documentation, I've found that [this article collection from UChicago](https://uchicago.service-now.com/it?id=kb_article&kb=KB00016472) is more helpful that what UT offers. Both unis seem to have similar Sympa instances; the admin config options are named similarly. The UChicago articles expand on how different options behave. 

config options of note: 

- Who can post? "Restricted to subscribers". We mostly want only members of any given list posting. Owners/admins/mods can always post. Exception for the student list: "Private, moderated for subscribers". Essentially means anyone who knows this address can post, but an admin needs to approve. Only other BLE people are really meant to post. 

- Who can see the list? "No conceal". Essentially this means our lists show up on the UTLists website, and there are web interfaces for each one people can go to (even w/o an account) to subscribe. 

- Who can (un)subscribe? "Owners approval". Admin needs to approve (un)sub requests.

- Include a footer message under "message templates". I go with variations on "Distribution list for BLE LTER *insert audience*. Replies will be sent to the whole group. Email *insert list email* to send a message to the group."

<a id="resources"></a>
# Resources
