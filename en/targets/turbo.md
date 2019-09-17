Overpass Turbo
==============

The standard tool for developing queries.

<a name="overview"/>
## Overview

Overpass Turbo is a website, to execute overpass API requests and see the result on a map.

Many examples of this manual link to Overpass Turbo with an appropriate predefined query.

A public instance is available at [https://overpass-turbo.eu](https://overpass-turbo.eu). The source code is located on [Github](https://github.com/tyrasd/overpass-turbo) as well as on the Overpass API. Martin Raifer has developed Overpass Turbo; at this point I would like to express my thanks to him.

Almost all output formats, which are available at the Overpass API, can also be understood by Overpass Turbo. There are difficulties with queries with very large result sets; Even today, the JavaScript engines of the browsers used reach the limits of their memory management. Therefore Overpass Turbo asks, if it has received a large result set, whether the end user wants to take the risk of freezing the browser.

There are many popular and useful features, but which go beyond the scope of this manual. Please refer to the [Documentation](https://wiki.openstreetmap.org/wiki/DE:Overpass_turbo) on Overpass Turbo. This is especially true for _Styles_ and the query generator _Wizard_. This manual is limited to the direct interaction with the query language.

<a name="basics"/>
## Basics

The view of the website is divided into several parts; they differ in the arrangement between desktop and mobile versions. Open [them](https://overpass-turbo.eu) best now in a separate tab.

In the desktop version, there is a large text box on the left; Here you should enter your query. On the right is a map section. Via the two tabs _Map_ and _Data_ you can choose between the map section and a text field for the received data.

In the mobile version, the text field stands for the query above the map section. The second text field for the received data is below the map section; Instead of the tabs, you can scroll back and forth between the two parts by courageous scrolling.

We practice the standard use case:
Type:

    nwr[name="Canary Wharf"];
    out geom;

in the text field (or use [this link](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=18&Q=nwr%5Bname%3D%22Canary%20Wharf%22%5D%3B%0Aout%20geom%3B))!

Now click on _Run_. A progress message appears briefly, you will see almost the same picture as before.

Now click on the magnifying glass. This is the third symbol from above on the left side of the map section, below the plus/minus buttons. The map view now jumps to the finest resolution, which still shows all results.

The selected objects in the map section are now exactly the objects, that found the query.

Often it is useful, to look directly at the data actually delivered. This can be done with the tab _Data_ in the upper right corner above the map view or with scrolling down in the mobile version.

All objects highlighted on the map are clickable and then show, depending on the scope of their data, their ID, their tags or their metadata.

At some point you will encounter the message, that not all objects were supplied with the geodetic system. You can then test the query change for automatic completion. Or you can replace all occurrences of ``out`` by their counterparts with geometry ``out geom``.

If you expect a great result or want to process the data with another program anyway, you can also export the data directly for saving without displaying it: Go to _Export_, remain in the appearing window in the tab _Data_ and select ``raw data directly from Overpass API``. For long-running queries it is normal, that after the click nothing seems to happen.

Two useful extras should be noted:

- At the bottom right of the map are counters, how many objects of which type were returned in the last query.
- At the top left of the map section there is a search field. This has a lower performance than [Nominatim on openstreetmap.org](../criteria/nominatim.md), but the available search for place names is usually sufficient, to quickly place the map section in the right place.

<a name="symbols"/>
## Legend

The [Documentation](https://wiki.openstreetmap.org/wiki/EN:Overpass_turbo) already explains the colors. We are therefore concentrating more on the interplay here: You have an idea of a concrete object or object type, whether it is a point, line, surface, a composition of it, something abstract or something with blurred boundaries. In the OpenStreetMap data structures it is modeled in some way; it can, but does not necessarily, match its expectation.

The Overpass API provides [Tools](formats.md#extras), to switch from OpenStreetMap modeling to one, that fits better to the representation; either by obtaining the coordinates or geometric simplification or [Cut](../full_data/bbox.md#crop). Overpass Turbo must now deliver the best possible representation in any case, no matter whether the modeling in OpenStreetMap is still obvious, and regardless of whether the output format selected in the query matches the data sensibly.

This section explains which then finally comes out in the map display and how this relates to the query and the data.

Point objects can have a yellow or red interior. With a yellow interior they are real _Nodes_, with a red interior it's _Ways_.

Ways can become points either because of their small length, otherwise they'd be too inconspicuous: Please zoom out in [this example](https://overpass-turbo.eu/?lat=51.477&lon=0.0&zoom=19&Q=way%28%7B%7Bbbox%7D%7D%29%5Bbuilding%5D%3B%0Aout%20geom%3B) and watch buildings and streets become points!

    way({{bbox}})[building];
    out geom;

If that interferes with a specific query, you can disable it under _Settings_, _Map_, _Small Features_ as POIs.

Or they can be displayed as points, because [the query](https://overpass-turbo.eu/?lat=51.477&lon=0.0&zoom=19&Q=way%28%7B%7Bbbox%7D%7D%29%5Bbuilding%5D%3B%0Aout%20center%3B) output via ``out center``:

    way({{bbox}})[building];
    out center;

Point objects can have a blue or purple border; This also applies to objects drawn as a polyline or area. In all such cases, _Relations_ [are involved](https://overpass-turbo.eu/?lat=51.5045&lon=-0.0195&zoom=17&Q=rel%5Bname%3D%22Canary%20Wharf%22%5D%3B%0Aout%20geom%3B):

    rel[name="Canary Wharf"];
    out geom;

In contrast to _Nodes_ or _Ways_, the details of the _Relation_ are not available by clicking on the object, but in the bubble there is only a link to the _Relation_ on the main server. Under normal circumstances this is not a problem.

But if you specifically asked for an old version, then the data from the main page is different than the data obtained via Overpass API. Then there is no way around it, to look into the returned data itself via the _Data_ tab.

If, on the other hand, the line or border of the area is dashed, the geometry of the object is incomplete. This is usually a desired effect of the [Output limit](../full_data/bbox.md#crop) ([Example](https://overpass-turbo.eu/?lat=51.4765&lon=0.0&zoom=16&Q=%28%0A%20%20way%2851%2E475%2C%2D0%2E002%2C51%2E478%2C0%2E003%29%5Bhighway%3Dunclassified%5D%3B%0A%20%20rel%28bw%29%3B%0A%29%3B%0Aout%20geom%2851%2E475%2C%2D0%2E002%2C51%2E478%2C0%2E003%29%3B)):

    (
      way(51.475,-0.002,51.478,0.003)[highway=unclassified];
      rel(bw);
    );
    out geom(51.475,-0.002,51.478,0.003);

However, it can also be the result of a query, that has loaded some _Ways_, but not all _Nodes_ to _Ways_. Here we loaded _Ways_ based on _Nodes_, but [forget](https://overpass-turbo.eu/?lat=51.4765&lon=0.0&zoom=17&Q=%28%0A%20%20node%2851%2E475%2C%2D0%2E003%2C51%2E478%2C0%2E003%29%3B%0A%20%20way%28bn%29%3B%0A%29%3B%0Aout%3B) to load the missing nodes directly or indirectly:

    (
      node(51.475,-0.003,51.478,0.003);
      way(bn);
    );
    out;
    
The query can be repaired by [``out geom``](https://overpass-turbo.eu/?lat=51.4765&lon=0.0&zoom=17&Q=%28%0A%20%20node%2851%2E475%2C%2D0%2E003%2C51%2E478%2C0%2E003%29%3B%0A%20%20way%28bn%29%3B%0A%29%3B%0Aout%20geom%3B); more possibilities are explained in the section on [Geometries](../full_data/osm_types.md#nodes_ways):    

    (
      node(51.475,-0.003,51.478,0.003);
      way(bn);
    );
    out geom;

<a name="convenience"/>
