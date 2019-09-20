Data formats
============

There are different data formats for storing and transmitting OpenStreetMap data. We introduce all of those that have an immediate application purpose.

<a name="scope"/>
<!-- The title was translated to "demarcation" but from the context I think introduction may be better -->
## Introduction

The OpenStreetMap data types have already been introduced in the [introduction](../preface/osm_data_model.md). So you should already be familiar with nodes, ways and relations.

This section explains the different output formats and how the degree of detail returned can be adjusted. Which tool needs which output format is explained in the section about the tool.

How to retrieve complete OpenStreetMap object geometry is discussed in [the section on geometries](../full_data/osm_types.md) in the chapter [Spatial data selection](../full_data/index.md).

<a name="faithful"/>
## Specifying degree of detail

First to the degree of detail. While the output format is controlled by a global setting for each query, the level of detail for each output command is controlled by its parameter. This makes it possible to mix different levels of detail in one query; this ability is required for the optimal amount of data [for some geometry variants](../full_data/osm_types.md#full). This is noted for the [Applications](index.md).

To show the different levels of detail that you can ask for, we will use an example from the London suburb of Greenwich. The example is mainly chosen so that only a small number of nodes, ways and relations will be returned, and you can have a good look at the data in the _Data_ tab of Overpass Turbo.

The level of detail is specified by the out command combined with one or more parameters. There is a hierarchy of parameters to enable them:

<!--- Should there be an entry for out count ? --->

The command _out ids_ will [get](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20ids%3B) us:

    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out ids;

* the IDs of the objects

The command _out skel_ additionally [returns](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20skel%3B)  the information  necessary to build the geometry:

    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out skel;
    
* for nodes: their geographical coordinates
* for ways: an ordered list of node IDs
* for relations: an ordered the list of member types, IDs, and roles

The command _out_ (without additions or _out body_) [returns](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%3B) the complete geodata, i.e. in addition to the above:

    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out;
  
  * the tags of all objects
  
The command _out meta_ [returns](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20meta%3B) additionally:
   
    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out meta;

* the version per object
* the timestamp for each object
* the Changeset-Id
* the user ID
* the username for this user ID

<!--- Does the out attribution command exist or is it planned for a future version?

Finally, the _out attribution_ command returns the following data:

However, this last level of detail concerns data which, according to the prevailing opinion, fall under data protection. Therefore an [increased effort](../analysis/index.md) is necessary. Since this data is not required for any of the applications discussed in this chapter, we will dispense with an example here.
--->

<a name="extras"/>
## Extra detail

It is possible to add one of three additional geometry properties to the output. All combinations between the degrees of detail just presented and the additional degrees of geometry detail are possible.

The flag _center_ adds a single coordinate to each object. The coordinate is the middle of the bounding box enclosing the object. [Example 1](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20ids%20center%3B) return object IDs and centres: 

    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out ids center;

[Example 2](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20center%3B) centres combined with full data:

    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out center;

The flag _bb_ (for _Bounding-Box_) adds the enclosing bounding-box for each object: [Example](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20ids%20bb%3B)

    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out ids bb;

The flag _geom_ (for _geometry_) completes the full coordinates. The minimum level of detail required for this is _skel_, so it works up to and including _attribution_: [Example](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20skel%20geom%3B)

    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out skel geom;

But now we have not only a few hundred meters in a park of Greenwich but also several hundred kilometres of footpath in the east of England. This is a general problem of Relations. As a remedy there is a bounding box also for the output command, [see here](../full_data/bbox.md#crop).

Finally there is the output format _tags_. This is based on _ids_ and additionally displays tags, but no geometries or structures. It is especially useful if you don't need the coordinates in [the results](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20tags%3B):

    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out tags;

However, it can also be [combined](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20tags%20center%3B) with the two geometry levels _center_ and _bb_:

    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out tags center;

<a name="json"/>
## JSON und GeoJSON

Now to the data formats: While the level of detail can be selected for each output command, the output format is specified only once globally for each query. In addition, the choice of output format changes the form, but not the content.

Within JSON, the aim is to bridge the gap. On the one hand, there is a common format for geodata, so-called GeoJSON. On the other hand, the OpenStreetMap data should keep their structure, and it doesn't match GeoJSON's specifications.

As a solution there is the possibility, Create GeoJSON-compliant objects from the OpenStreetMap objects. However, the original OpenStreetMap objects are mapped true to the original in JSON and are not GeoJSON.

OpenStreetMap object [in JSON](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%5Bout%3Ajson%5D%3B%0A%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20geom%3B):

    [out:json];
    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out geom;
    
   Derived objects [in GeoJSON](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%5Bout%3Ajson%5D%3B%0A%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aconvert%20item%20%3A%3A%3D%3A%3A%2C%3A%3Ageom%3Dgeom%28%29%2C_osm_type%3Dtype%28%29%3B%0Aout%20geom%3B):

    [out:json];
    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    convert item ::=::,::geom=geom(),_osm_type=type();
    out geom;
The creation of derived objects is a big complex of topics with [own chapter](../counting/index.md).

<a name="csv"/>
## CSV

It is often useful to be able to organize data in tabular form. For OpenStreetMap data this means columns selected by the user and one line for each object found.

The selection of columns restricts the information available about the object for most objects. For example, tags that are not requested as columns are not output. More complex geometries than a simple coordinate cannot be displayed in this format either. This distinguishes this format from XML and JSON.

The standard case of a column is the key of a tag. The value of this tag is then output to the object for each object. If the object does not have the tag, an empty value is output. For the other properties of the object, there are special values that begin with `::`.

[Example](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%5Bout%3Acsv%28%3A%3Atype%2C%3A%3Aid%2Cname%29%5D%3B%0A%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20center%3B)

    [out:csv(::type,::id,name)];
    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out center;
    
CSV itself originally stood for _comma separated value_. However, the numerous programs using it have developed different expectations of separators. Therefore the separator can be configured as well as the heading [on and off](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%5Bout%3Acsv%28%3A%3Atype%2C%3A%3Aid%2Cname%3Bfalse%3B%22%7C%22%29%5D%3B%0A%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20center%3B):

    [out:csv(::type,::id,name;false;"|")];
    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out center;

The [respective applications](index.md) indicate which variant is suitable.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU5MjMwODY0MCwtMTIwMDM4NDgxOSwtMj
AxMTgxNDU5MSwxMDMzNTI3Mjc4LDEzNjY3MzE3NDcsLTU3MDI4
Njc0OSwxMzAwMjE1MjM5LC02NTI2ODIwNzIsMTc4MjkyNDY0Ny
wxNzg2MTUwMjc3LDcxODc3NDM3OF19
-->