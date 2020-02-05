---
title: BLE LTER Information Management Handbook
subtitle: Everything, including the kitchen sink
author: An T. Nguyen and Tim Whiteaker -- BLE-LTER Information Managers
date: 2019-12-04
---

<!-- MarkdownTOC -->

- [Front matter issues](#front-matter-issues)
	- [Introduction to BLE LTER Information Management](#introduction-to-ble-lter-information-management)
	- [Our philosophies](#our-philosophies)
	- [Preamble](#preamble)
- [Tools](#tools)
	- [Tools we use](#tools-we-use)
	- [Tools we develop and maintain](#tools-we-develop-and-maintain)
		- [Javascript apps](#javascript-apps)
		- [R packages](#r-packages)
- [Metadata database](#metadata-database)
	- [Installation and admin](#installation-and-admin)
		- [Issues I've run into](#issues-ive-run-into)
			- [Server/service not running](#serverservice-not-running)
		- [How to set up remote connection to locally hosted Postgres database on Windows](#how-to-set-up-remote-connection-to-locally-hosted-postgres-database-on-windows)
			- [1. General things you need](#1-general-things-you-need)
			- [2. On the server PC](#2-on-the-server-pc)
			- [On the client PC](#on-the-client-pc)
	- [Add-ons to vanilla metabase that are specific to BLE](#add-ons-to-vanilla-metabase-that-are-specific-to-ble)
		- [Addition of two year columns to DataSetPersonnel](#addition-of-two-year-columns-to-datasetpersonnel)
- [Metadata template](#metadata-template)
- [Data processing](#data-processing)
- [EML](#eml)
- [Data archiving](#data-archiving)
	- [Where we archive](#where-we-archive)
		- [Which member node are we](#which-member-node-are-we)
		- [Replication](#replication)
		- [Why we archive at EDI](#why-we-archive-at-edi)
	- [Who does the archiving](#who-does-the-archiving)
	- [How we archive at EDI](#how-we-archive-at-edi)
		- [Handling large files](#handling-large-files)
- [Core Program quirks](#core-program-quirks)
	- [Personnel / Responsible Parties](#personnel--responsible-parties)
		- [Creator](#creator)
		- [Other people](#other-people)
	- [Stations](#stations)
- [Data and metadata styling guide or style rules](#data-and-metadata-styling-guide-or-style-rules)
	- [Core Program](#core-program)
	- [Other datasets \(PI-driven datasets in BLE terminology\)](#other-datasets-pi-driven-datasets-in-ble-terminology)
- [Website](#website)
	- [Our website technologies](#our-website-technologies)
	- [How to update website](#how-to-update-website)
		- [Minor content updates](#minor-content-updates)
		- [Less minor updates](#less-minor-updates)
	- [Branding](#branding)
		- [Logo color reference](#logo-color-reference)
			- [Where we use these colors:](#where-we-use-these-colors)
	- [Miscellaneous website notes](#miscellaneous-website-notes)
- [Bibliographic management](#bibliographic-management)
	- [Zotero best practices](#zotero-best-practices)
		- [How to add a new item](#how-to-add-a-new-item)
	- [Misc. Zotero notes](#misc-zotero-notes)
- [Personnel management](#personnel-management)
	- [Mailing List Admin](#mailing-list-admin)
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

We use modular components in our IM system and workflow -- as opposed to a comprehensive solution like DEIMS. We try to use existing solutions whenever possible and not modify them willy nilly; we've found that there's almost always a tool somewhere suited to our purposes even in its vanilla form.

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

<a id="metadata-database"></a>
# Metadata database

See https://github.com/LTER/lter-core-metabase for a first stop documentation on LTER-core-metabase as a product and a project. This section in the handbook primarly concerns usage of metabase at BLE and certain issues I've encountered.

<a id="installation-and-admin"></a>
## Installation and admin
Postgres woes and how to overcome them

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

<a id="add-ons-to-vanilla-metabase-that-are-specific-to-ble"></a>
## Add-ons to vanilla metabase that are specific to BLE

<a id="addition-of-two-year-columns-to-datasetpersonnel"></a>
### Addition of two year columns to DataSetPersonnel

After deciding to eschew listing people as creators in core program datasets, we settled on a solution to include a separate data table (a separate data entity in EML terms) listing personnel and their years associated with a dataset, while still listing the same list, only sans year, as associated parties in EML. This practice now requires a few modifications to our instance of LTER-core-metabase. Normally we refrain from deviating from the vanilla version of LTER-core-metabase, since the "vanilla" version of the schema archived at https://github.com/LTER/lter-core-metabase. Here we archive the SQL code we used, in case we ever need to restart our metabase from an install of the vanilla. The file `add_yearspan_to_DSpersonnel.sql` contains the SQL. 

<a id="metadata-template"></a>
# Metadata template

<a id="data-processing"></a>
# Data processing

<a id="eml"></a>
# EML

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

When signing in to the EDI data portal and asked for a member node, we're urn:node:LTER.  EDI filters on the package identifier (knb-lter-ble): any of the "knb-lter-*" packages go through urn:node:LTER, while the rest go through urn:node:EDI.

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


<a id="data-and-metadata-styling-guide-or-style-rules"></a>
# Data and metadata styling guide or style rules

Refer to BLE as either "Beaufort Lagoon Ecosystems LTER" or "BLE LTER". Avoid using just "BLE" as it's without context and avoid the hyphenated form "BLE-LTER". 

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
	- Zotero search interface
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

<a id="miscellaneous-website-notes"></a>
## Miscellaneous website notes

- Job postings need to be include a diversity statement. See email communication from Ken circa Dec 2019. Example: Our BLE LTER program benefits from nurturing a culture of diversity. We encourage applications from potential students that are traditionally underrepresented to help us connect our research to the broader global community.

<a id="bibliographic-management"></a>
# Bibliographic management

We use Zotero to manage our non-data publications. 

<a id="zotero-best-practices"></a>
## Zotero best practices
See Zotero best practices here https://environmentaldatainitiative.files.wordpress.com/2019/04/zotero_best_practices.pdf.

<a id="how-to-add-a-new-item"></a>
### How to add a new item

Easiest way is to use the Zotero connector, browser add-on for Chrome/Firefox/etc. Navigate to the web page for the journal article (or book chapter, or what have you) with the Zotero desktop app open and the LTER-BLE group library open. (Zotero Connector will always save items to whatever library/collections you have open and have write access to.) Click on the Zotero Connector button on the browser toolbar. Zotero will pick up existing metadata from the publisher, and save you a lot of trouble. For journal articles in most cases there won't be any need to go in and edit anything. 

Make sure to: 
- add item to appropriate sub-collection under the LTER-BLE group library:
	- "For Website" if item is to appear on publication page
	- "For Network" if item is to appear in the broad LTER network group library
- add appropriate custom tags (via Tags tab, right hand pane on Zotero desktop): 
	- LTER-Funded for work funded by BLE
	- Foundational for work we are building our work on
	- LTER-BLE for everything
- add data URL if applicable to "Extra" field. URL needs to have "https://doi.org" format
- edit metadata fields as needed if Zotero wasnt able to fill them out

<a id="misc-zotero-notes"></a>
## Misc. Zotero notes

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

### List maintenance

These tasks need to be done periodically:

- Review membership and subscribe/un-subscribe people manually as they join/leave the project. We might want to ask graduating students if they want to remain subscribed. In the future we might want to give people DIY instructions instead. E.g. point people to the UTlists webpage to subscribe or give them instructions how to subscribe via emailing sympa@utlists.utexas.edu. 

- Review for bouncing (invalid) addresses. 

- Check if messages are getting past spam filters. We'll assume the best and look  into this as issues come up. 

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
