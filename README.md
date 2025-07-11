# Quadrilateral Detection Script

This Python script detects **quadrilaterals** (especially square- or rectangle-like shapes) within an image using computer vision techniques. It leverages **grayscale conversion**, **adaptive thresholding**, **HSV color filtering**, and **contour approximation** to identify and visualize rectangular shapes.

---

## ✨ Features

- 🖼 **Image Loading**: Reads an image from a file (default: `vhod.png`).
- 🌗 **Grayscale Conversion**: Converts input to grayscale for preprocessing.
- 🎚 **Adaptive Thresholding**: Highlights regions of interest based on local contrast.
- 🔁 **Morphological Operations**: Cleans and connects thresholded regions using closing.
- 🎨 **HSV Color Filtering**: Targets specific color ranges for refined detection.
- 🧩 **Contour Detection & Approximation**:
  - Approximates contours to polygons.
  - Filters shapes with **4 vertices** that are **convex**.
- 🧮 **Area Sorting**: Keeps the **top 6 largest** detected quadrilaterals.
- 🖍 **Visualization**:
  - Original image with numbered blue quadrilaterals.
  - Intermediate grayscale and thresholded stages.
- 🖨 **Output Coordinates**: Prints the vertices of detected quadrilaterals.

---

## 🧰 Prerequisites

Install the required Python packages:

```bash
pip install numpy opencv-python matplotlib
```

---

## 📂 Project Structure

```
your_project/
├── main.py
└── vhod.png         # Input image to analyze
```

---

## 🚀 How to Run

1. **Prepare Input Image**  
   Place your input image in the same folder as `main.py` and name it `vhod.png`.

2. **Run the Script**

   ```bash
   python main.py
   ```

3. **View the Results**
   - A `matplotlib` window will open with 4 subplots:
     - Original Image
     - Grayscale Image
     - Thresholded Image
     - Detected Quadrilaterals
   - Quadrilaterals are drawn in **blue** and labeled with numbers.
   - Their coordinates will be printed in the terminal.

---

## 🧠 Script Overview

### `iskalnik(slika: np.ndarray) -> list[np.ndarray]`

The main quadrilateral detection function.

**Steps:**

1. Converts the input image to grayscale and applies Gaussian blur.
2. Applies **adaptive thresholding** using `cv2.ADAPTIVE_THRESH_GAUSSIAN_C`.
3. Performs a **morphological closing** to clean up noise.
4. Converts the original image to **HSV color space**.
5. Applies an **HSV filter** using adjustable color bounds.
6. Combines threshold and HSV masks with bitwise OR.
7. Finds **external contours** in the combined mask.
8. Approximates contours using `cv2.approxPolyDP`.
9. Filters for polygons that:
   - Have **exactly 4 vertices**.
   - Are **convex**.
10. Returns a list of valid quadrilateral corner points.

---

## 🔧 Customization

- **Input Image**  
  Change `input_image_path` in `main.py` to your desired image path.

- **HSV Color Range**  
  Edit `lower_hsv` and `upper_hsv` in the `iskalnik()` function to match the color of the rectangles you're targeting.

- **Number of Quadrilaterals to Show**  
  Adjust:
  ```python
  top_squares = detected_quadrilaterals_improved[:6]
  ```
  to keep more or fewer detected shapes.

---

## 🖼 Example Output

- `Detected Quadrilaterals`: Displays up to 6 largest convex 4-sided contours in blue.
- `Thresholded Image`: Shows the binary image used for contour detection.
- `Console Output`: Lists corner coordinates of the detected quadrilaterals.
