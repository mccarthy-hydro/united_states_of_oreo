# United States of Oreo

## Summary

This Repository exists to document methods used to calculate the number of Oreo 
Cookies it will take to completely cover the US. This is an attempt at winning 
the Oreo Sweepstakes in the year 2026. 


The "Quick Math" Method (Theoretical Maximum)

If you don't care about the items overlapping or fitting perfectly into corners, you can do a simple area-to-area division.

    Find the Area of the US: In a GIS, use a layer of the CONUS (Continental US) projected in an Equal Area Projection (like USA Contiguous Albers Equal Area Conic). This ensures the square footage is accurate across the whole country.

    Find the Area of your Item: Calculate the area of one item in the same units (e.g., square meters).

    The Formula:
    Total Items=Area of One ItemArea of Continental US​

2. The "Tessellation" Method (The Real-World Fit)

In reality, shapes don't always fit perfectly. If you have a rectangular item, you’ll have "dead space" at the jagged borders of the US coastline. To simulate this, we use Tessellation (Gridding).

    Generate Tessellation: Most GIS software has a tool called "Generate Tessellation" or "Create Fishnet." You tell the tool the dimensions of your item (e.g., 100m×50m), and it creates a grid of those shapes across the map.

    Spatial Join / Intersect: You then run an Intersect between your new grid and the US boundary.

    Counting: You open the attribute table and see the count of all shapes that are 100% contained within the US boundary.

3. The Packing Problem (The Precise Way)

If your item isn't a simple square (like a circular stadium or an irregular shape), you run into the Packing Problem.

    Hexagonal Grids: If your items are roughly circular, a Hexagonal Tessellation is mathematically the most efficient way to "pack" them into an area with the least amount of wasted space.

    Centroid Check: To get a "realistic" count of how many items could physically sit inside the US without hanging over the ocean, you would filter your grid to only keep shapes whose Centroid (center point) is within the US boundary.

Critical Step: Choosing the Right Projection

When dealing with the entire US, projections matter more than ever. > Warning: If you use a standard web map projection (like Web Mercator), the North (near Montana) will look much larger than the South (near Texas). If you calculate your "item count" using this, your numbers will be wildly inflated in the North.

Always use: USA Contiguous Albers Equal Area Conic (SRID: 102003) for this specific calculation.
Example Calculation:

If the Continental US is roughly 8,080,000 km2:

    Football Fields: You could fit about 1.5 billion football fields.

    Pennies: You could fit roughly 2.8 quadrillion pennies.

Are you trying to visualize a specific "grid" of items on a map, or are you just looking for the final massive number for a report?
