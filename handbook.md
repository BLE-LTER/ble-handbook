---
title: BLE LTER Information Management Handbook
subtitle: Everything, including the kitchen sink
author: An T. Nguyen and Tim Whiteaker -- BLE-LTER Information Managers
date: 2019-12-04
---

# Front matter issues

## Introduction

## Preamble

I speak in first person throughout this handbook. Writing in passive or imperative voice is tiring.

# Tools

## Tools we use

## Tools we develop and maintain

# Metabase

## Installation and admin

## Add-ons to vanilla metabase that are specific to BLE

# Metadata template

# Data processing

# EML

# Core Program quirks

## Personnel / Responsible Parties

Core Program packages only have one creator with only a surname "Beaufort Lagoon Ecosystems LTER, Core Program". See the entry in metabase with NameID "blecreator-core". This is in order to generate citations in this form: 

> Beaufort Lagoon Ecosystems LTER, Core Program. 2019. Stable oxygen isotope ratios of water (H2O-d18O) from coastal river, lagoon, and open ocean sites along the Beaufort Sea, Alaska, 2019-ongoing. Environmental Data Initiative. https://doi.org/DOI_PLACE_HOLDER. Dataset accessed 12/04/2019.

So that they are analogous to this citation from a PI-driven dataset (see comm. with Ken/Jim October/November 2019):

> Beaufort Lagoon Ecosystems LTER, V. Lougheed. 2019. Carbon flux from aquatic ecosystems of the Arctic Coastal Plain along the Beaufort Sea, Alaska, 2010-2018. Environmental Data Initiative. https://doi.org/DOI_PLACE_HOLDER. Dataset accessed 12/04/2019.

Other people involved in the dataset will be credited as an associated party in the EML record. The order might still matter, so order as the PI have written them down in the template. To be listed as an associated party, a person has to have handled/been responsible for the data at some point, so as to be able to answer questions if necessary. The PI supplies this list normally, so not an action item for us, just FYI. 

In addition to listing people as associated parties in EML, we will include a personnel table as a data entity. This table will essentially have the same information as the EML entries, but also include years of involvement in this role with the dataset so that data users can track down appropriate people to ask about specific periods in the dataset. We use an add-on to vanilla metabase to keep track of people and years. 

To generate a CSV table once metabase is populated, use the R function 

`bleutils::export_personnel` 

This function takes care of querying metabase for the specified dataset ID, and spits out a ready made personnel CSV. Rough naming convention is `BLE_LTER_[dataset nickname]_personnel.csv`. 

I call this function from inside the directory with other data files. I list the personnel entity last in metabase: e.g. if there are five actual data entities, the EntitySortOrder for the personnel table is 6. Note that due to a MetaEgress quirk, all dataTables will be listed before all otherEntities. 

Remember to list the seven columns of the personnel CSV in DataSetAttributes. Duplicating the same set of rows. 


## Stations

