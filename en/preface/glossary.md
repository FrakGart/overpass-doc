Glossary
========

For OpenStreetMap as well as for the Overpass API, a couple of notions are explained.

### Bounding Box

A bounding box is defined by two values for a latitude and two values for a longitude.
It consists of all coordinates
that have a latitude that is between the two supplied latitude values
and that have a longitude that is between the two supplied longitude values.

### Derived

_Deriveds_ are a special type of object within the Overpass API.
The _deriveds_ are not part of the OpenStreetMap data opposed to _nodes_, _ways_, and _relations_,
but are generated during the runtime of a request.
Using _deriveds_ makes it possible to rewrite tags and to simplify geometries.

### Evaluator

This is one of the building blocks of a request.
An _evaluator_ is called in the context of a statement, block statement, or the special filter _if_.
Depending on its type, it either operates on the whole set of objects chosen in a _variable_ or individually on each object.
Again, depending on its type, it returns a number, a string, or a geometry.

### Filter

This is one of the building blocks of a request.
A _filter_ always belongs to a _query_ statement and filters for the objects to be selected there.
The multiple filters of a query statement are connected by conjunction,
i.e. there are always found only those objects that match all filters of the respective _query_ statement.

### Key

A _key_ is a part of a _tag_.
It is the leading string.

### Node

A specific type of object in the data model of OpenStreetMap.
It represents a single coordinate.
With tags it is a distinguishable object,
without tags it almost always is just a part of a way to equip it with coordinates.

### Request

The text in the formal query language
that the client (e.g. from the front-end _Overpass Turbo_) sends to the server.
The content of the request exclusively controls
what out of the OpenStreetMap data is fetched.

### Relation

A specific type of object in the data model of OpenStreetMap.
It models all things that are beyond the scope of nodes and ways.

### Set

See at Variable

### Statement

This is one of the building blocks of a request.
Statements are those parts that can be independently executed.
Statements can be classified as block statements or simple statements.
The two most important statements are
_query_ to select objects from the OpenStreetMap database
and _print_ to append selected objects to the response.

### Tag

A _tag_ is a data structure in both OpenStreetMap and the Overpass API to store textual data.
Every tag consists of a _key_ and a _value_
and is part of an object, i.e. a node, a way, a relation or a derived.

### Value

A _key_ is a part of a _tag_.
It is the trailing string.

### Variable

A variable in the Overpass API is always a set variable.
Set variables serve during the execution of a request
to convey object selections from statement to statement.

### Way

A specific type of object in the data model of OpenStreetMap.
It represents a polyline.
If the polyline is closed, then it can be an area.