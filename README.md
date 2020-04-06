# HatBox

*A user-space spatial add-on for Apache Derby and H2 databases*

![hatbox](hatbox.jpg)

'user-space add-on' what does that mean? It means that HatBox employs user visible tables, procedures, functions and triggers to implement spatial functionality on top of standard Derby/JavaDB and H2. The upside is that when you use HatBox you are not tied to a special version of Derby or H2, you can upgrade Derby and H2 independently of HatBox. The down side is that feature geometry must be created and manipulated outside the database and the tables, procedures, functions and triggers that make up HatBox may be corrupted by inadvertent user action. This approach was taken to avoid deep modification of the Derby and H2 code bases, and to avoid sticky source licensing issues, particularly in respect of the JTS Topology Suite. JTS is a critical library for Hatbox, supplying all the secondary filtering functionality. It is licensed under the LGPL, which is incompatible with the licences of Apache Derby (ASL 2.0) and H2 (MPL 1.1 and EPL 1.0)

HatBox has the following key features:

* Open source, published under the [GNU Lesser General Public License (LGPL) version 2.1](LICENSE.md)
* Core rtree functionality of Hatbox is available to be published under multiple FOSS licenses (eg ASL, MPL, EPL)
* Written in 100% Java™
* Hatbox Derby relies on Table Functions first introduced in Derby / JavaDB version 10.4
* Supports a single geometry column per spatial table with persistent RTree indexing
* Stores table meta-data and index nodes in a separate new table for each spatial table related by table name eg NAT.ROADS will have a new table NAT.ROADS_HATBOX created to store its meta-data and index.
* Relies on the LocationTech [JTS Topology Suite](https://github.com/locationtech/jts) for the implementation of all geometry functions. Consequently HatBox is limited to 2D spatial operations, although geometry may be stored as 3D.
* Geometry is stored in OGC Well Known Binary (WKB) format. JTS is used to read and write WKB internally, so HatBox is currently limited to the WKB format of the OpenGIS® Simple Features Implementation Specification for SQL ([99-049](http://www.opengeospatial.org/standards/sfs)). This does not include recent additions such as PolyhedralSurface and TIN.
* Supports the full range of OGC spatial filters, including Distance Within (DWithin) and Beyond.
* Fully integrated into the [GeoTools](http://geotools.codehaus.org/) framework with a HatBox DataStore.
* SRIDs are assumed to be EPSG codes when used with Geotools.

## Project Information

The original project (http://hatbox.sourceforge.net) by Peter Yuill is available on Source Forge.

This fork is maintained as a temporary measure by Jody Garnett to facilitate compatibility with JTS, GeoTools and Java 8.