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