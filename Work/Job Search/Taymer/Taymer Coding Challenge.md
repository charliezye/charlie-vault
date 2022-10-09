# Taymer Coding Challenge

#### Width Detection
1. Could check difference between wire color and background
	1. Convert to grayscale first?
	2. Threshold value to go to white vs. black to make more clear edge?
2. Could use an edge detection algorithm
	1. See furthest left/right edges on same y-value
3. Obstructions towards edge?

#### Defect Detection
1. Search between edges only so use width detection algorithm in tandem
2. Could find patches within where color changes
3. Edge detection is probably best here as well
	1. Use to find edges of pinhole/cut
2. Obstructions?
	1. Water droplet
	2. Dust
	3. Dirt
	4. Flies

So far:

-   Image thresholding basics
-   Canny edge detection basics
-   Class implementation with file name input
-   Visual representation and sliders for image threshold and edge detection

Next:

-   Find default thresholds for wire edges and holes/scratches
-   Find better way to display edges on top of original image
-   Find how to measure width between edges
-   Create method to measure diameter of defect for drawing
-   Evenly measured at 3 different spots
-   Create method to detect if defect present differentiate between pinhole, tear, scratch
	- Check average of rows/columns and pick largest averages 
-   All defects tend to have very bright white around edge of defect, can use image thresholding for this
-   Alternatively check for corners/edges not horizontal
-   Scratches in particular have only white
-   Tears have large horizontal section of black/white
-   Pinhole has distinct circular shape
-   Figure out how to display wire width and circles around defects on screen
-   Add buttons for running methods for defect detection, width detection
-   Probably just want to have general defect detection that automatically differentiates
-   Documentation for each method
-   Separate documentation document with images to explain methods etc.
-   Consider other edge detection algorithms better at horizontal edges
-   Write implementation tips for dust/dirt detection