#this document is not up to date!



### copy()

Copies the track and return the copied track. The name of the new track will be suffixed with '_copy'. You can set your own name by assigning it: `track.name = 'your_track_name';`



### addPart(Part, ticks)

Adds part to track with an offset of the provided number of ticks. If ticks is omitted, the offset will be 0.



###copyPartTo()
Copies the part and adds it to the same track of the original part at the specified position and return the newly created part. If the part hasn't been added to a track, this method behaves like `copy()`.


### movePart(ticks)
If the part is added to a track: moves the part inside its track by the number of ticks provided. Both positive and negative values are accepted.

### movePartTo()
If the part is added to a track: moves the part to the specified position. If the position exceeds the length of the track, the track will be enlarged.

You can provide the position in the same formats as [`setPosition()`](position).



### moveParts(ticks | millis)
Move all parts


### movePartTo(Part, position)

### copyPartTo(Part, position)


### deletePart(Part)
can be used to delete more than 1 part at the time

### deleteParts()
delete all parts


### getPart(index | name | id)
can be use to get more than 1 part at the time


### getParts()
get all parts