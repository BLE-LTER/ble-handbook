---
title: BLE LTER Information Management Handbook
subtitle: Everything, including the kitchen sink
author: An T. Nguyen and Tim Whiteaker -- BLE-LTER Information Managers
date: 2019-12-04
---

<!-- MarkdownTOC -->

- Front matter issues
	- Introduction
	- Preamble
- Tools
	- Tools we use
	- Tools we develop and maintain
		- R packages
- Metadata database
	- Installation and admin
		- Issues I've run into
			- Server/service not running
		- How to set up remote connection to locally hosted Postgres database on Windows
			- 1. General things you need
			- 2. On the server PC
				- Figure out where the data "cluster" is
				- Change the cluster configuration
				- Change firewall rules to open port
			- On the client PC
	- Add-ons to vanilla metabase that are specific to BLE
		- Addition of two year columns to DataSetPersonnel
- Metadata template
- Data processing
- EML
- Core Program quirks
	- Personnel / Responsible Parties
		- Creator
		- Other people
	- Stations
- Data and metadata styling guide or style rules
	- Core Program
	- Other datasets \(PI-driven datasets in BLE terminology\)
- Website
	- Our website technologies
	- How to update website
		- Minor content updates
		- Less minor updates
	- Miscellaneous website notes
- Bibliographic management
	- Zotero
	- Misc. Zotero notes
- Personnel management

<!-- /MarkdownTOC -->


# Front matter issues

## Introduction

## Preamble

I speak in first person throughout this handbook. Writing in passive or imperative voice is tiring.

# Tools

## Tools we use

## Tools we develop and maintain

### R packages

1. MetaEgress

2. insitu

3. bleutils

# Metadata database

See https://github.com/LTER/lter-core-metabase for primary documentation on LTER-core-metabase as a product and a project. This section in the handbook primarly concerns usage of metabase at BLE and certain issues I've encountered.

## Installation and admin



Postgres woes and how to overcome them

Very verbose -- for complete newbs to the DB admin world. Windows specific, but I think once you get an idea of how the pieces get together, operating system doesn't matter as much.

Assuming a vanilla installation from executable (.exe) on Windows. Some assumptions might not apply in other scenarios (e.g. where the default data directory is). 

**NOTE:** A good chunk of trouble might be avoided if PostgreSQL is _not_ installed in C:\Program Files. This folder is write-protected in many work PC systems where you are not the admin, and generally quite inaccessible in many ways. Change the directory during the installation process. 

### Issues I've run into

#### Server/service not running
One day as fine as any other, you log on to your computer and open up DBeaver ready to do some ecological data management. The database refuse to connect, citing "Connection to localhost:5432 refused. Check that the hostname and port are correct and that the postmaster is accepting TCP/IP connections." Boom. What's happening? 

This normally means the server associated with the Postgres instance aka cluster (see below) that your database lives on is not running. In my experience, the default cluster is normally set to auto-start its server at system startup; this is not true for other clusters.

How to start a Postgres server:

Go to Command Prompt. Navigate with `cd` to the directory with all the nifty Postgres programs, generally under <directory you installed Postgres into>\PostgreSQL\<version number>\bin. Now call `pg_ctl` with option `- D <path to your directory>` then `start`. Similarly you can also call `stop`. 

What if this doesn't work:

Does it say permission denied anywhere in the cmd log? Is your data directory in Program Files? It's time to change it. 

Follow these directions since it is fairly comprehensive (while everything else here is bits and pieces from stackoverflow): [see here.](https://radumas.info/blog/tutorial/2016/08/08/Migrating-PostgreSQL-Data-Directory-Windows.html)

Do all of the clusters fail to start? I have at least two clusters on my computer thatr 

### How to set up remote connection to locally hosted Postgres database on Windows

#### 1. General things you need
You need:
- To know the IP addresses of both the server and client machines, aka the PCs hosting the database and the PC trying to access it. This might mean a public-facing address or an internal one. Consult whoever is the network admin, since you'll need to talk to them by the end of this guide anyway. 
- To have set up a user and password with at minimum CONNECT rights to the database in question.

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

#### On the client PC
Use this connection information:

Host: <server IP address>
Port: <cluster port>
Database: <your database name>
User: <your username>
Password: <your password>

## Add-ons to vanilla metabase that are specific to BLE

### Addition of two year columns to DataSetPersonnel

After deciding to eschew listing people as creators in core program datasets, we settled on a solution to include a separate data table (a separate data entity in EML terms) listing personnel and their years associated with a dataset, while still listing the same list, only sans year, as associated parties in EML. This practice now requires a few modifications to our instance of LTER-core-metabase. Normally we refrain from deviating from the vanilla version of LTER-core-metabase, since the "vanilla" version of the schema archived at https://github.com/LTER/lter-core-metabase. Here we archive the SQL code we used, in case we ever need to restart our metabase from an install of the vanilla. The file `add_yearspan_to_DSpersonnel.sql` contains the SQL. 

# Metadata template

# Data processing

# EML

# Core Program quirks

## Personnel / Responsible Parties

### Creator

Core Program packages only have one creator with only a surname "Beaufort Lagoon Ecosystems LTER, Core Program". See the entry in metabase with NameID "blecreator-core". This is in order to generate citations in this form: 

> Beaufort Lagoon Ecosystems LTER, Core Program. 2019. Stable oxygen isotope ratios of water (H2O-d18O) from coastal river, lagoon, and open ocean sites along the Beaufort Sea, Alaska, 2019-ongoing. Environmental Data Initiative. https://doi.org/DOI_PLACE_HOLDER. Dataset accessed 12/04/2019.

So that they are analogous to this citation from a PI-driven dataset (see comm. with Ken/Jim October/November 2019):

> Beaufort Lagoon Ecosystems LTER, V. Lougheed. 2019. Carbon flux from aquatic ecosystems of the Arctic Coastal Plain along the Beaufort Sea, Alaska, 2010-2018. Environmental Data Initiative. https://doi.org/DOI_PLACE_HOLDER. Dataset accessed 12/04/2019.

### Other people

Other people involved in the dataset will be credited as an associated party in the EML record. The order might still matter, so order as the PI have written them down in the template. To be listed as an associated party, a person has to have handled/been responsible for the data at some point, so as to be able to answer questions if necessary. The PI supplies this list normally, so not an action item for us, just FYI. 

In addition to listing people as associated parties in EML, we will include a personnel table as a data entity. This table will essentially have the same information as the EML entries, but also include years of involvement in this role with the dataset so that data users can track down appropriate people to ask about specific periods in the dataset. We use an add-on to vanilla metabase to keep track of people and years (see section BLE add-ons to vanilla metabase). 

To generate a CSV table once metabase is populated, use the R function 

`bleutils::export_personnel` 

This function takes care of querying metabase for the specified dataset ID, and spits out a ready made personnel CSV. Rough naming convention is `BLE_LTER_[dataset nickname]_personnel.csv`. 

I call this function from inside the directory with other data files. I list the personnel entity last in metabase: e.g. if there are five actual data entities, the EntitySortOrder for the personnel table is 6. Note that due to a MetaEgress quirk, all dataTables will be listed before all otherEntities. 

Remember to list the seven columns of the personnel CSV in DataSetAttributes. Easiest way to duplicating the same set of attributes from a previous Core Program dataset. 

## Stations

Core Program sampling makes use of a certain number of fixed stations. Normal practice for PIs in their data is to include station codes (e.g. KALD1). I make it a practice to 

# Data and metadata styling guide or style rules

## Core Program

Rough conventions that frankly I made up some of the time. 

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
	- 

Data table entity descriptions
	- Include variables in data
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
	- Example: BLE_LTER_CTD.csv

## Other datasets (PI-driven datasets in BLE terminology)

Follow conventions set out by PI and edit sparingly when needed and when feasible.

# Website

## Our website technologies

Our website is built from static HTML pages and hosted with Netlify. There is no content management system (e.g. Drupal, Wordpress). In fact, there is no static website generator (e.g. Hugo, Jekyll) involved either. 

Somewhat exhaustive list of website technologies we use: 
- Netlify for hosting and deployment
- A Github repo as both production and development source code
- Bootstrap 4
- FontAwesome for icons
- Leaflet for map
- Custom apps: 
	- Data Catalog built on PASTA API
	- Zotero search interface
	- 

## How to update website 

### Minor content updates

I.e. adding text or images to existing pages.

### Less minor updates

## Miscellaneous website notes

- Job postings need to be include a diversity statement. See email communication from Ken circa Dec 2019. Example: Our BLE LTER program benefits from nurturing a culture of diversity. We encourage applications from potential students that are traditionally underrepresented to help us connect our research to the broader global community.

# Bibliographic management

## Zotero

## Misc. Zotero notes

# Personnel management