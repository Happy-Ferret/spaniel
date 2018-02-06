# Spaniel
*Time span handling for Go*


**Spaniel** contains functionality for timespan handling, specifically for merging overlapping timespans and finding the overlaps between multiple timespans.

## Install

This package is "go-gettable", just do:

    go get github.com/senseyeio/spaniel

## Examples

These examples are all available in the ``examples`` folder.

### Basics

Spaniel operates on lists of timespans, it has a built-in Empty timespan for convenience or you can use your own type, so long as it implements the timespan.T interface.

To create a new list of timespans:

	var now = time.Date(2018, 1, 30, 0, 0, 0, 0, time.UTC)

	input := timespan.List{
		timespan.NewEmpty(now, now.Add(1*time.Hour)),
		timespan.NewEmpty(now.Add(30*time.Minute), now.Add(90*time.Minute)),
	}

    
You can then use the Union function to merge the timestamps:

	union := input.Union()
	fmt.Println(union[0].Start(), union[0].End()) // 00:00 - 01:30

Or the Intersection function to find the overlaps:

	intersection := input.Intersection()
	fmt.Println(intersection[0].Start(), intersection[0].End()) // 00:30 - 01:00
 
 If you need to use a more complex object, you can call UnionWithHandler and IntersectionWithHandler. There is an
 example of this in ``examples/handlers.go``.