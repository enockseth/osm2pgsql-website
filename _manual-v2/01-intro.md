---
chapter: 1
title: Introduction
---

This is the manual for version <b>2.x.y</b> of osm2pgsql. If you are running an
older version of osm2pgsql, refer to the [manual v1]({% link doc/manual-v1.html
%}).
{:.note}

Osm2pgsql is used to import OSM data into a PostgreSQL/PostGIS database for
rendering into maps and many other uses. Usually it is only part of a
toolchain, for instance other software is needed for the actual rendering
(i.e. turning the data into a map) or delivery of the maps to the user etc.

Osm2pgsql is a fairly complex piece of software and it interacts with the
database system and other pieces of the toolchain in complex ways. It will take
a while until you get some experience with it. It is strongly recommended that
you try out osm2pgsql with small extracts of the OSM data, for instance the
data for your city. Do not start with importing data for the whole planet, it
is easy to get something wrong and it will break after processing the data for
hours or days. You can save yourself a lot of trouble doing some trial runs
starting with small extracts and working your way up, observing memory and disk
usage along the way.

It helps to be familiar with the
[PostgreSQL](https://www.postgresql.org/){:.extlink} database system and the
[PostGIS](https://postgis.net/){:.extlink} extension to it as well as the
[SQL](https://en.wikipedia.org/wiki/SQL){:.extlink} database query language.
Some knowledge of the [Lua language](https://www.lua.org/){:.extlink} is also
useful.

This manual always documents the current version of osm2pgsql. If same
information is only valid in [certain versions]({% link releases/index.md %}),
the section will have a note like this: *Version >= 1.4.0*{: .version}

Sections labelled *Experimental*{:.experimental} describe new features which
might change at any point without notice. We encourage you to experiment with
them and report how they work for you, but don't rely on them for production
use.

It is recommended that you always use the newest [released version]({% link
releases/index.md %}) of osm2pgsql. Earlier versions sometimes contain bugs
that have long since been fixed.

