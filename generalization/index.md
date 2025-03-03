---
title: Generalization
---

# Generalization

[*Cartographic
generalization*](https://en.wikipedia.org/wiki/Cartographic_generalization){:.extlink}
is the process turning detailed geographic data into more general data for
smaller zoom levels or smaller scale maps. It is essential for generating
good-looking, easy to interpret, and fast rendering small scale maps.

Currently osm2pgsql has almost no built-in support for generalization, usually
it is done using lots of SQL magic after the initial import of the data with
osm2pgsql. From September 2022 to February 2023 we are running a
[project](https://prototypefund.de/project/generalisierung-von-openstreetmap-daten-mit-osm2pgsql/){:.extlink}
funded by the [Prototype Fund](https://prototypefund.de/){:.extlink} and the
[German Federal Ministry of Education and
Research](https://www.bmbf.de/){:.extlink} to add more support for
generalization to osm2pgsql. This will include adding some generalization
support directly to osm2pgsql but also using the capabilities of the PostgreSQL
database and especially the PostGIS extension in a more easy to use fashion.

<div id="sponsorlist">

<div>
<a href="https://prototypefund.de/"><img src="PrototypeFund-P-Logo.svg" height="140"/></a>
</div>

<div style="text-align: center;">
<a href="https://www.bmbf.de/"><img src="bmbf-logo.png" height="110"/></a>
<p>September 2022 bis Februar 2023<br/>FKZ 01IS22S29</p>
</div>

</div>

