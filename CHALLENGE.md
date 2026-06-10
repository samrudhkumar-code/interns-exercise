# Bonus Challenge — Find Nearby Riders with H3

## The problem

A customer has placed an order. The pickup point is in `pickup.json`.
There are 10 available riders in `drivers.json`.

**Find all riders within 1 H3 ring of the pickup point at resolution 9.**

Print their names. That's it.

## What is "1 ring"?

H3 divides the map into hexagonal cells. Every cell has 6 neighbours — those are
the cells in ring 1. `grid_disk(cell, 1)` returns the cell itself plus all 6
neighbours — 7 cells total. Any rider whose location falls inside those 7 cells
is considered "nearby".

```
      [ ][ ]
    [ ][X][ ]
      [ ][ ]

X = pickup cell, [ ] = ring-1 neighbours
```

## Steps

**1. Install the library**
```bash
pip install h3
```

**2. Convert a lat/lon to an H3 cell**
```python
import h3
cell = h3.latlng_to_cell(lat, lng, resolution=9)
```

**3. Get all cells within 1 ring**
```python
nearby_cells = h3.grid_disk(cell, 1)  # returns a set of 7 cells
```

**4. Check if a driver is in any of those cells**
Convert each driver's lat/lon to a cell and check if it's in `nearby_cells`.

**5. Print the matching drivers**

## How to submit

1. Create a branch: `feat/your-name-challenge`
2. Add your solution as `solution-your-name.py`
3. Raise a PR to this repo

## Hint

At resolution 9, each hexagon is roughly 170m across. Riders very close to the
pickup point will share the same cell or be one ring away. Check the result —
you should find a few drivers nearby and a few that are too far.
