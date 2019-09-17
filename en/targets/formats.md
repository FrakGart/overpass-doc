Data formats
============

There are different data formats for transporting OpenStreetMap data.
We introduce all those that have an immediate application purpose.

<a name="scope"/>
## Delimitation

The data types have already been introduced in the [appropriate section of the introduction](../preface/osm_data_model.md).
So you should already be familiar with nodes, ways and relations.

This section explains output formats.
On the other hand the different possible degrees of detail are introduced.
Which tool needs which output format is explained in the section about the tool.

The common problem of completing the geometry of OpenStreetMap objects,
is dedicated to [the section on geometries](../full_data/osm_types.md) in the chapter [Spatial data selection](../full_data/index.md).

<a name="faithful"/>
## Traditional degrees of detail

First to the degrees of detail:
While the output formats are controlled by a global setting for each query,
the levels of detail for each output command are controlled by its parameters.
This makes it possible to mix different file grades in one query;
this ability is required for the optimal amount of data [of some geometry variants](../full_data/osm_types.md#full).
This is noted for the [Applications](index.md).

We also give an example of the degrees of detail around the London suburb of Greenwich.
The example is mainly chosen in such a way that it provides only a small number of nodes, ways and relations,
to have a good look at the data in the tab _Data_ of Overpass Turbo.

For the original OpenStreetMap detail grades there is a hierarchy to enable them:

The command _out ids_ [get](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20ids%3B):

    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out ids;

* the IDs of the objects

The command _out skel_ [returns](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20skel%3B) additionally provides the necessary information,
to build the geometry:

    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out skel;
    
* at nodes their coordinate
* at Ways and Relations the list of members

The command _out_ (without additions) [returns](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%3B) the complete geodata, i.e. additionally:

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

Finally, the _out attribution_ command returns the following data:

* the Changeset-Id
* the user ID
* the username for this user ID

However, this last level of detail concerns data which, according to the prevailing opinion, fall under data protection.
Therefore an [increased effort](../analysis/index.md) is necessary.
Since this data is not required for any of the applications discussed in this chapter, we will dispense with an example here.

<a name="extras"/>
## Variants

It is possible to add three degrees of detail to additional geometry. All combinations between the degrees of detail just presented and the additional degrees of geometry detail are possible.

The flag _center_ activates a single coordinate for each object. This has no special mathematical meaning,but lies simply in the middle of the bounding box enclosing the object: [Example 1](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20ids%20center%3B)

    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out ids center;

[Example 2](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20center%3B)

    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out center;

The flag _bb_ (for _Bounding-Box_) activates the enclosing Bounding-Box for each object: [Example](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20ids%20bb%3B)

    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out ids bb;

The flag _geom_ (for _geometry_) completes the full coordinates. The minimum level of detail required for this is _skel_, so it works up to and including _attribution_: [Example](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20skel%20geom%3B)

    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out skel geom;

But now we have not only a few hundred meters in a park of Greenwich but also several hundred kilometres of footpath in the east of England. This is a general problem of Relations. As a remedy there is a bounding box also for the output command, [see there](../full_data/bbox.md#crop).

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
    
CSV itself originally stood for _comma seaprated value_. However, the numerous programs using it have developed different expectations of separators. Therefore the separator can be configured as well as the heading [on and off](https://overpass-turbo.eu/?lat=51.4775&lon=0.0&zoom=16&Q=%5Bout%3Acsv%28%3A%3Atype%2C%3A%3Aid%2Cname%3Bfalse%3B%22%7C%22%29%5D%3B%0A%28%20way%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%5Bname%3D%22Blackheath%20Avenue%22%5D%3B%0A%20%20node%28w%29%3B%0A%20%20relation%2851%2E477%2C%2D0%2E001%2C51%2E478%2C0%2E001%29%3B%20%29%3B%0Aout%20center%3B):

    [out:csv(::type,::id,name;false;"|")];
    ( way(51.477,-0.001,51.478,0.001)[name="Blackheath Avenue"];
      node(w);
      relation(51.477,-0.001,51.478,0.001); );
    out center;

The [respective applications](index.md) indicate which variant is suitable.