# conky.arcs

<p align="center"><img width="300" src="logo/conky.arcs-logo_small.png"></p>

## Content
Package *conky.arcs* consists of 3 files:
 - *conky.conf*: basic configuration, defines window and history graphs
 - *conky.arcs.lua*: script to create all graphic elements
 - *config.lua*: definition of all graphic elements

### Intro
Files *conky.conf* and *conky.arcs.lua* could be considered as read only.
So if you like to change things, *config.lua* is the right place.

All graphic elements are held in a big definition table.
In lua language, a *table* is noted as "{ ... }", with elements in the form
  **name = value**
Tables may be nested. Then *value* is again "{ ... }"

**config.lua** is coded as a standalone module, therefore the table is coded
in a function, which is called at the beginning of *conky.arcs.lua* script.

### Conky
The [GitHub Wiki](https://github.com/brndnmtthws/conky/wiki) serves as a
central hub for all of Conky's documentation.

### Details
Each set of concentric arcs is treaten as a group of informations. Each group
is noted as a *lua-*table.
These are the groups:
 - **cpu**: shows the load of a processor / core
 - **io**: shows the read-/write-load of the system
 - **mem**: shows the usage of memory
 - **hdd**: show the wasted space of harddisks
 - **temp**: shows the temperature of cpu/gpu and harddisks
Groups defined before group **cpu** are so called 'static texts', which means,
that variables in that groups are evaluated once per hour. All other variables
are evaluated every time the script gets executed. See "update_interval" of
conky.conf file.

Each group starts with *x/y* - the offset of the arcs group, *w/h* the dimension
of the arcs group followed by a table **main**, which contains the prominent
text definitions, a table **sub**, which contains texts of lower importance
and a table **rings**, which contains the definitions of the arcs.
All positions and sizes are in fontsize units, which means, base unit for
width and height are calculated by determining the size of some letters using
given fontsize (*fs*) and font-definition '*font*'.

Each text definition consists of a position *x/y* an alignment info *a* and
the text itself. Alignment means, the text can start at given position, which
means, the text is on the right side (value **R**) or the text can end at
given position, which means, the text is at the left side (value **L**).
This way we don't have jumping texts no matter how many text segments are
in one line.
Texts of the table **main** are rendered using color definition *color* from
the very beginning. Texts of the table **sub** are rendered using
color definition *col3*

Text can be static text like **'Uptime'** or it may be a placeholder for
values, that conky provides like **'${uptime_short}'**.
See [Conky Variables](http://conky.sourceforge.net/variables.html)

**Rings** have these properties:
 - x/y: position (in fontsize units)
 - r: radius (the middle of the arc)
 - h: the height of an arc (between 0.1 and 1)
 - d: direction cw = clockwise, or ccw = counterclockwise
 - name: name of a conky variable
 - arg: argument of that conky variable (may be empty string)
 - max: max. value, so the actual value is always a percent factor of max.
 - sa: start angle in degrees, 0° is 12 o clock, 180° 6 o clock
 - ea: end angle in degrees (should always be bigger than sa
                             - add 360 on smaller values)
 - ba: is alpha value of the background (0 .. 1)
 - fg: foreground color (in hex notation without leading '#')


