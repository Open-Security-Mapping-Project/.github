# Open Security Mapping Project

The Open Security Mapping Project (OSMP) aims to improve the visibility and scrutiny of security institutions and infrastructure.

*Launched August 24, 2025* 

# Short-term Goals

We are attempting to improve the free documentation and information available around the large network of detention facilities in the United States, territories and military bases, especially those
overseen by the Department of Homeland Security (DHS), Immigration & Customs Enforcement (ICE), Customs and Border Protection (CBP) and the Department of Defense. There are more than 100 facilities
directly overseen by ICE and around at least 1100-1200 facilities which are part of the overall US government immigration detention network, according to "Vera."

We want a contemporary, up-to-date family of data sources that makes this foggy network of control and confinement more "legible" and with better policy outcomes for everyone. All of these systems
remaining in obscurity and only receiving PR-style messaging from the government, and scattered social media posts, does not help long-term organizing around the subject. A well organized project
can enable civil society to "spin up" sets of data, web pages, campaigns and so on about each facility and the network as a whole.

We also want to provide better information for people with family and friends confined in these facilities. Serving them better can include contact info, URLs, multi-lingual information.

Other layers of this system, the larger 287(g) jail screening detention network, associated with physical jail locations, (as well as the web of contractors and transportation systems) is another
huge program area to factor in and provide better information about.

Anyone could participate in this project, under the Code of Conduct noted below. Please be aware each website like OSM, Wikidata etc have their own usage, conduct and copyright policies.

# Repositories

* ICE Detention Facilities Scraper - https://github.com/Open-Security-Mapping-Project/ice_detention_scraper - MIT license
* Example data sets - https://github.com/Open-Security-Mapping-Project/example-data-sets - CC0 Public Domain license

# Sources of information

* ICE.GOV main detention center index and subpages ( https://www.ice.gov/detention-facilities )
* The Global Detention Project information pages
(e.g. https://www.globaldetentionproject.org/countries/americas/united-states/detention-centres/664/krome-north-service-processing-center )
* the "Vera" project to track detention sites ( https://www.vera.org/ice-detention-trends )
* Vendor websites such as CoreCivic (formerly CCA) and Geo Group (formerly Wackenhut) that provide security services at the bulk of facilities
(e.g. https://web.archive.org/web/20160722020305/http://www.geogroup.com/maps/locationdetails/31 )
* SAM.gov contractor data & contracts
* Inspector General reports. Can disclose which contractors have which roles, and other operational major features.
* Legal and advocacy organizations like ACLU, NLG
* Job listings on USA.gov
* State level contractor data
* News media reports
* DOJ federal information pages on immigration court facilities (executive branch) which are often co-located at DHS detention facilities
* WatchIce ( https://watchice.org/ ) by Lockdown Systems collective ( https://lockdown.systems/ ) has a lot of data including updated
inmate counts at a large number of facilities (which we are not tracking).

# Places to improve data, add it, and increase quality

* OpenStreetMap - ( https://www.openstreetmap.org/ ) - the world's largest open license mapping project
* Wikidata ( https://www.wikidata.org/wiki/Wikidata:Main_Page ) - which provides relational, machine readable data, (including multi lingual link options). Awkward interface but
good for interconnecting 
* Wikipedia ( https://en.wikipedia.org )
* Wikimedia Commons for public domain photographs of facilities (ICE already publishes these in low resolution.)

# Goal: Data processing, scraping and automation

The data available is often badly formatted, scattered, dated and incomplete. Scraper scripts can make this easier, and could make it possible to confirm automatically when ICE
adds more facilities. Automation between data sources could reduce the workloads greatly.

A 1.0.0 version scraper in Python for the ICE "detention facilities" index has been created: https://github.com/Open-Security-Mapping-Project/ice_detention_scraper

## Goal: Internal site index

We probably want to have our own internal index with either its own unique key per facility or keying off another database like VERA. There should be a column for the VERA site
IDs in any case. This index would probably be in the form of a JSON file. 

It could also include dormant facilities, for example the one in Appleton, Minnesota that ICE may start using. (I recently updated this facility and marked it as dormant).

Additional logistical elements like contractor vendors, the aircraft operator and owner companies, and "ICE Air" airports involved, are also relevant to this. However it seems
like starting with the main detention facilities should be a higher priority within this project. A number of good research projects are mapping out the aircraft tier of the system as it quickly expands.

----

<img width="1920" height="2000" alt="osmp-example-osm-edit-exif" src="https://github.com/user-attachments/assets/5cc412e4-4efc-48fc-97b5-1b436d71e970" />

# Goal: Mapping on OpenStreetMap (OSM)

The primary entry point of this project was starting to work on the OSM representations and tags. We want all the known facilities to come up on the OSM search mechanism,
so the names and addresses must be connected. (Many are missing currently.)

It became clear that OSM alone is not the only data source that should get contributions, for best results. OSM would *not* be the place to add a half dozen links to news
reports about a detention facility, for example.

We are trying to follow community best practices, which includes Open Data Commons Open Database License (ODbL) and respecting copyright. (It is not okay to just copy
over material from Google Maps, for example.)

Improving the data and representation of these facilities on OpenStreetMap brings them more out of obscurity. A variety of tags can be used to improve accessibility
and visibility of these facilities as well as capturing a more clear sense of their nature.

For power users the JOSM app should be used (especially with frequently used tags) rather than the iD web interface.

* https://wiki.openstreetmap.org/wiki/How_to_contribute
* https://osmfoundation.org/wiki/Licence/Contributor_Terms
* Recent discussion gave pointers: https://www.reddit.com/r/openstreetmap/comments/1mwki1n/mapping_ice_and_immigration_related_facilities/
* Earlier discussion covers many tags, international side: https://community.openstreetmap.org/t/detention-centres-for-rejected-asylum-seekers/122453

## Searching for tagged facilities

If our primary key is `prison:for=migrant` then we can use the following in https://overpass-turbo.eu/ to instantly give a search view:

<img width="703" height="655" alt="image" src="https://github.com/user-attachments/assets/cf2ac386-0696-42b2-8106-4f593aa95771" />

One of our goals should be to **get all the main ICE detention facilities to appear in this search result**. Then we have a more easily managed set of locations to work with.

Simply pop this into the text area, "Run" it and scroll over to the United States. (it is centered on Europe by default.) Note that all the other tags come up when you
select one of the facilities. Also in the upper right, besides the "map" tab there is a "data" tab which has a machine-readable formatted JSON of the set of results.

```
/*
This has been generated by the overpass-turbo wizard.
The original search was:
“prison:for=migrant in "United States"”
*/
[out:json][timeout:25];
// fetch area “United States” to search in
{{geocodeArea:United States}}->.searchArea;
// gather results
nwr["prison:for"="migrant"](area.searchArea);
// print results
out geom;
```


## OSM Tags and Keys

OSM has an elaborate tagging and key system. For example this is consistent with existing data I was recommended to follow. In general adding "prison:for=migrant"
should let us give a search result of all the prisons in this.

Example tags I was recommended:

```
operator=CoreCivic
amenity=prison
prison:for=migrant
operator:wikidata=Q1135278    (corecivic)
```

It is also helpful to provide the phone number and address onto the area. "Alternate names" that tend to come up for those facilities are also very good to add. ICE
has been renaming "Detention Center" to "Processing Facility" so it is good to have one or the other as an alternate name. If someone gets a recent photo showing
the name on the facility on a physical sign, that should probably be the primary name.

The Q values kind of 'lock' fields in OSM web iD editor (eg if you add operator:wikidata it will stop you from typing in the operator field). Not clear to me
if operator should have a value anyway, or just operator:wikidata.

* https://wiki.openstreetmap.org/wiki/Key:prison
  * Prisons can also have "classifications" (eg medium security). I saw some of these on the CoreCivic website pages.
* https://taginfo.openstreetmap.org/
* https://taginfo.openstreetmap.org/search?q=prison
* https://taginfo.openstreetmap.org/tags/amenity=prison
* https://taginfo.openstreetmap.org/tags/prison%3Afor=migrant#overview
* https://taginfo.openstreetmap.org/tags/prison%3Afor=migrant#wiki - this wiki should be added. `prison:for=migrant`
* https://taginfo.openstreetmap.org/keys/prison%3Afor#combinations common tags found alongside `prison:for` values.
* https://taginfo.openstreetmap.org/keys/prison#combinations common tags alongside `prison` values
* https://taginfo.openstreetmap.org/tags/amenity=prison#combinations common tags alongside `amenity=prison`

Be aware that entries like "prison ground" areas in OSM may have ID numbers that change (aka 'areas' and 'ways') so we should *not* be tracking those entities
via their OSM area ID numbers at all.

Other attributes such as capacity (see Global Detention Project), the presence of immigration courts, Wikipedia links (including to the architect and operator, etc)
would be helpful. Each facility contractor for health care, custodial and maintenance may also be able to obtain verifiable info.

# Goal: Documenting on Wikipedia

Wikipedia is a world-leading source of information summaries with strong SEO (search engine optimization presence). Many facilities have Wikipedia pages but many do not.
Some are up to date and others are not. Wikipedia pages can link to OSM and to Wikidata "Q" numbers. A good description summary can be seen by millions of people at a
glance all over the internet.

Wikipedia is also multilingual so once there is an English page for a given site it is an easier prospect to add Spanish and other languages.

Wikipedia it seems is a *good location* to add news report links, if they are reliable sources in the internal policy (no Daily Mail!).

I am not familiar yet with adding OSM coordinates into Wikipedia but obviously that seems likely to be helpful.

* https://en.wikipedia.org/wiki/Wikipedia:Reliable_sources

# Goal: Documenting on Wikidata

Wikidata ( https://www.wikidata.org/wiki/Wikidata:Main_Page ) is a semantic database that gives each entity a "Q" number code. This can help by showing the "operator"
values, URLs and links to source info, including other databases about these facilities, and much more. If a facility exists on OSM it can have a Wikidata page as well.
Vendors like CoreCivic and Akima Global Services LLC also have Q pages and can be tagged as `operator:wikidata` keys in OSM.

Wikidata it seems is a *good location* to add news report links. Wikidata is also good for relational information like ownership between entities. ICE "Field Offices"
are also associated to each detention facility and should be represented on Wikidata.

I am not familiar yet with adding OSM coordinates into Wikidata but obviously that seems likely to be helpful.

# Goal: Documenting on Littlesis

Littlesis ( https://littlesis.org/ ) is designed for "power mapping" and includes a lot of people like executives, political donors, obscure board members and investors
as well as relational data like subsidiary businesses. It operates on a model similar to Wikipedia.

# Goal: Documenting on Wikimedia Commons

Wikimedia Commons is the appropriate place to upload photos that are public domain of the ICE facilities. ICE provides these at a low resolution. Once loaded there,
they can be used legally in places like Wikipedia, Wikidata and so on.

# Goal: Repos, project direction and task management

Repositories could be created for each major goal (e.g. Wikipedia, Wikidata, and OSM contributions). Individual tasks could be managed via the Github issue queue.
Other services may be better or spun off entirely. 

Later on we could have meetings about the project as well as a web survey for constituencies like people who have friends and family held in these facilities to
learn what they might find helpful instead of just making assumptions.

We do not have an internal chat platform but would likely land on a common vendor like Discord, RocketChat or Slack to deal with real time coordination and perhaps
virtual meetings. BigBlueButton would be a better vendor for meetings than a more public system.

# Language, visibility and accessibility

The primary language of the project is US English (en-us). However as the data gets collated better it should become more feasible to make sure multi lingual resources
are available.

Obviously the entire issue is "heated". This project is more limited in scope to improving information availability, semantic info, documentation and so on, so the
written materials should generally tend towards the "Wikipedia Neutrality" style (NPOV - https://en.wikipedia.org/wiki/Wikipedia:Neutral_point_of_view ) . Outside those specific contexts of materials, people should exercise their Freedom of Speech while it still exists!

A couple social media accounts e.g. on Bluesky and Mastodon would probably help with the visibility of the project. And could include "recently updated" type bulletin
updates. Even a bot could be watching for updates to OSM, Wikipedia or similar.

## Licensing

This is aimed at creating an *open access* system. So, we should follow the licenses for each service. In OSM this is Open Data Commons Open Database License (ODbL).
There are certain subtle problems between say, Wikidata and OSM so that one cannot auto scrape from the other.

## Code of Conduct (CoC)

We try to adhere to Contributor Covenant 3.0 Code of Conduct for a harassment free experience. ( https://www.contributor-covenant.org/version/3/0/code_of_conduct/ ) .
If needed contact hongpong AT hongpong dot com. In the future, if the project expands, someone should be named lead for code of conduct issues separately from the project lead, ideally.

## Additional notes about detention facilities

In the initial review of facilities I started finding odd patterns. For example Adams County Mississippi (Natchez) was apparently built on land donated by a company
that wanted to stay anonymous. It seems like an "entreprenurial" approach to this facility industry is a key underpinning and helps get counties to get involved.

Separate markdown files in a separate repository for interesting things about each facility would be good. (TBD: how to title these files. Could be like
`ms-adams-county-detention-facility.md` or similar with a 2 letter state code for its location.

## Authorship and credits

Initial version of this README.md

*Dan Feidt ( @hongpong ) - August 24, 2025*

Further credits for project tools and contributors helping move along the goals of this project should be added here (or later into a separate document).
