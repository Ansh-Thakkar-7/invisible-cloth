# invisible-cloth
<br>
<b>Import Libraries:</b>

cv2: Used for computer vision tasks (OpenCV library).
numpy: Used for numerical operations (NumPy library).
Trackbar Setup:

**Creates a window named "Trackbars" for user interaction.**
Defines trackbars for adjusting the upper and lower bounds of Hue, Saturation, and Value in the HSV color space. These values control the color range to be isolated.
An empty function nothing is assigned to the trackbar callbacks (it does nothing but allows trackbar creation).
Initialization:

Opens the default video capture device .
Reads the first frame from the video stream and stores it for later use.
Video Processing Loop:

Continuously reads a frame from the video stream.
Converts the frame from BGR color space (used by OpenCV) to HSV color space (easier to isolate colors).
Reads the current positions of the trackbars to get the user-defined color range (upper and lower HSV bounds).
Color Isolation:

Creates a mask using cv2.inRange to identify pixels within the specified color range (based on trackbar positions).
Applies a median blur to the mask to reduce noise in the color detection.
Inverts the mask to create a black background where the color object isn't present.
(Optional) Applies dilation to the mask to slightly enlarge the object boundaries (might be helpful depending on lighting conditions).

Extracting Object and Background:

Extracts individual color channels (Blue, Green, Red) from the original frame.

Performs bitwise AND operation on each channel with the inverted mask. This makes the background black in the original frame.

Merges the modified channels back into a color image, creating a black background area (representing the "sheet").

Extracts individual color channels from the initial frame (read at the beginning).

Performs bitwise AND operation on each channel with the original mask. This extracts the color object from the frame.

Merges the modified channels back into a color image, creating the object area (the "sheet" itself).

Combining Results:

Uses bitwise OR to combine the object area and black background area into a final image.
Display and User Input:

Resizes the final image and displays it in a window named "final result".
Resizes the original frame and displays it in a window named "org" for comparison.
Waits for a key press. Pressing 'q' quits the program.
**Cleanup:
**
Releases the video capture object.
Closes all open windows.
