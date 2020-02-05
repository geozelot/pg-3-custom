### PostGIS customized source, used by me.

##### This is a rebased clone of the latest stable ([stable-3.0](https://github.com/postgis/postgis/tree/stable-3.0)) of the [PostGIS GitHub mirror](https://github.com/postgis/postgis/), where I add custom functions and experiment with.

##### All credits go to the original source [authors](https://github.com/postgis/postgis/authors.git)!
____

### Custom AddOns

Stable versions of this source are in [master](https://github.com/geozelot/pg-custom/tree/master), experiments in dev branches.
Stable functions are also available as source files [here](https://github.com/geozelot/pg-addons).


* #### function set `LWGEOM_dump_segments`: <br>
  ##### `GEOMETRY_DUMP ST_DumpSegments(geom GEOMETRY)`<br>
  Dumps the linear component(s) of the given geometry `geom` into the minimal (two-vertice) segments.<br>
  Returns a `GEOMETRY_DUMP` having a `path INT[]` and `geometry GEOMETRY` member.
  
* #### function set `LWGEOM_dump_substrings`: <br>
  ##### `GEOMETRY_DUMP ST_LineSubstringsByLength(geom GEOMETRY, seg_len FLOAT8)` <br>
  ##### `GEOMETRY_DUMP ST_LineSubstringsByLength(geog GEOGRAPHY, seg_len FLOAT8)`
  Creates substrings of the linear component of the given geometry `geom` having a length of `seg_len` each;
  segments will be created starting with the `ST_StartPoint`, and last segment may be shorter than `seg_len`.<br>
  Returns a `GEOMETRY_DUMP` having a `path INT[]` and `geometry GEOMETRY` member.
  <br>
  ##### `GEOMETRY_DUMP ST_LineSubstringsBySegment(geom GEOMETRY, seg_cnt INT)`
  Creates `seg_cnt` equal length substrings of the linear component of the given geometry `geom`.<br>
  Returns a `GEOMETRY_DUMP` having a `path INT[]` and `geometry GEOMETRY` member.
  <br>
  <br>
  ##### `SETOF GEOMETRY_DUMP _ST_DumpSubstrings(geom GEOMETRY, len_frac FLOAT)`
  Utility C function to create segments from the linear component of `geom` using a fraction (`len_frac`) in sequence. Get's called by `ST_LineSubstringsByLength` & `ST_LineSubstringBySegments`.

___

### Build (Linux)

Follows the standard procedure for installing PostGIS from repository source; make sure you have the following libs installed:

* libtool
* autotools-dev
* automake

Clone this repo and install:

```
$ git clone https://github.com/geozelot/pg-custom.git

$ cd pg-custom

$ ./autogen.sh
$ ./configure

$ make && make install
```