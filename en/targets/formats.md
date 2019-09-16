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


