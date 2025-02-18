# Convert an Image to a C Array for OLED Display with Python

## I.Overview

This repository provides a Python script that converts an image into a C array, which can be used to display graphics on an OLED screen. The script supports automatic thresholding, inversion, and formatted output for embedded applications.

## II. Features
- **Automatic Thresholding**: Uses Otsu's method to determine the best threshold for binarization.
- **Invert Colors Option**: Allows inversion of monochrome colors for compatibility with different displays.
- **C Array Formatting**: Generates a formatted C array ready for microcontroller projects.
- **Customizable Resolution**: Supports resizing to fit common display resolutions (e.g., 128x64, 64x64).

## III. Requirements
Ensure you have the following installed before running the script:

- **Python 3.x**
- **Pillow (PIL) library**
    ```bash
    pip install pillow
    ```

## IV. Usage

1. Modify the Code:

    - Open the script in your favorite code editor (e.g., Visual Studio Code).
    - Update the Image Path: Modify the image_path variable to point to the location of your image file.
    - Set the Output Resolution: Change the width and height variables to the desired dimensions for the output array (note that for SSD1306, the maximum width is 128 and maximum height is 64).

2. Run the Script via the Command Line:

    - Open a terminal or command prompt.
    - Navigate to the directory containing the script.
    - Execute the script using:
        ``` bash
        python ImageToCArray.py
        ```
    - The script will output:
        - A preview of the processed image.
        - The byte array in Python format for debugging.
        - A formatted C array printed to the console.

3. Using Visual Studio Code (VS Code):

    - Open VS Code and load the folder containing the script.
    - Open the integrated terminal by selecting Terminal > New Terminal or by pressing Ctrl+` .
    - Make sure you're in the correct directory, then run:
        ```bash
        python ImageToCArray.py
        ```
    - You will see a preview window displaying the processed image, and the terminal will show the byte array and formatted C array output.

## V. Function Descriptions

### `imageToByteArray`
Converts an image into a 2D byte array representation suitable for monochrome OLED displays.

**Parameters:**
- `image_path (str)`: Path to the image file.
- `width (int)`: Output image width (e.g., 128 for SSD1306).
- `height (int)`: Output image height (e.g., 64 for SSD1306).
- `invert (bool, optional)`: If True, inverts black and white in the output image. Default is False.
- `threshold (int, optional)`: Manually set binarization threshold (0-255). If None, Otsu's method is used.
- **Returns**: A 2D list of integers representing the image in byte form.

### `formatAsCArray`
Formats a 2D byte array into a C array string.

**Parameters:**
- `py_array (List[List[int]])`: The input 2D byte array.
- `c_array_name (str, optional)`: The name of the C array. Default is "img".
- `line_break (int, optional)`: Number of bytes per line in the output. Default is 16.
- **Returns**: A string representing the formatted C array.

### `printArray`
Visualizes a 2D byte array in the console, simulating an OLED display.

**Parameters:**
- `py_array (List[List[int]])`: The 2D byte array to visualize.
- **Returns**: None.

## VI. Example Code

```python
# Modify these variables before running the script:
image_path = r"C:\Path\to\your\image.png"
width, height = 64, 64

byte_array = imageToByteArray(image_path, width, height, invert=True)
c_array = formatAsCArray(byte_array)
printArray(byte_array)
print(c_array)
```