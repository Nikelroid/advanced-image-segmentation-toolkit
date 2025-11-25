# Advanced Image Processing & Segmentation Toolkit

![Python](https://img.shields.io/badge/python-3.8%2B-blue?logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-1.24%2B-013243?logo=numpy&logoColor=white)
![OpenCV](https://img.shields.io/badge/opencv-4.5%2B-green?logo=opencv&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Data_Viz-orange?logo=matplotlib&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-Optimization-8CAAE6?logo=scipy&logoColor=white)

## Description

This repository contains the implementation of five distinct computer vision and image processing tasks. The project focuses on solving fundamental problems such as data clustering, image segmentation, and contour detection using both classical and statistical approaches.

The algorithms are largely implemented **from scratch** to demonstrate a deep understanding of the underlying mathematics (e.g., coordinate transformations, energy minimization via Viterbi, and clustering logic) rather than relying solely on high-level library calls. The work is based on an academic curriculum (Image Processing Principles), tackling specific challenges like separating nested data clusters or detecting objects with complex boundaries.

## Features

  * **K-Means Clustering:** Custom implementation capable of handling non-linearly separable data (e.g., concentric circles) via coordinate transformation.
  * **Mean-Shift Segmentation:** Full implementation of the Mean-Shift algorithm using 3D color histograms and spatial kernels for image segmentation.
  * **SLIC Superpixels:** Simple Linear Iterative Clustering implementation for generating superpixels based on CIELAB color space and spatial proximity.
  * **Interactive Segmentation (GrabCut):** A GUI-based tool wrapping OpenCV's GrabCut, allowing users to define foreground and background using mouse strokes.
  * **Active Contours (Snakes):** Implementation of the Snake algorithm using the **Viterbi** dynamic programming approach to minimize internal and external energies for boundary detection.

## Installation

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/your-username/advanced-image-processing-algorithms.git
    cd advanced-image-processing-algorithms
    ```

2.  **Install dependencies:**
    The project relies on standard scientific Python libraries.

    ```bash
    pip install numpy opencv-python matplotlib scipy
    ```

3.  **Verify Data Files:**
    Ensure `Points.txt` and the required image files (`park.jpg`, `slic.jpg`, `birds.jpg`, `tasbih.jpg`) are in the same directory as the scripts.

## Usage & File Descriptions

Below is a detailed breakdown of each module and how to run it.

### 1\. K-Means Clustering (`q1.py`)

This script solves a clustering problem where standard K-Means fails (nested concentric circles).

  * **Methodology:** 1.  Reads 2D points from `Points.txt`.
    2\.  Runs standard K-Means (Fails to separate rings).
    3\.  **Transformation:** Converts Cartesian coordinates $(x, y)$ to Polar coordinates $(r, \theta)$.
    4\.  Runs K-Means on the transformed data.
    5\.  Maps results back to Cartesian space for visualization.
  * **Running the script:**
    ```bash
    python q1.py
    ```
  * **Output:** Generates plots `res01.jpg` (Raw data), `res02.jpg` (Failed Cartesian clustering), and `res04.jpg` (Successful Polar clustering).

### 2\. Mean-Shift Segmentation (`q2.py`)

Implements the Mean-Shift algorithm for segmentation without using the OpenCV built-in function for the core logic.

  * **Methodology:**
      * Converts input (`park.jpg`) to YCrCb color space.
      * Constructs a 3D histogram of pixel colors.
      * Iteratively shifts data points toward the mode (highest density) using a spherical kernel.
      * Clusters pixels that converge to the same mode.
  * **Running the script:**
    ```bash
    python q2.py
    ```
  * **Output:** Saves the segmented image as `res05.jpg`. *Note: This script is computationally intensive and may take time to run.*

### 3\. SLIC Superpixels (`q3.py`)

Generates superpixels (groups of perceptually similar pixels).

  * **Methodology:**
      * Converts image (`slic.jpg`) to CIELAB color space.
      * Initializes grid centers and perturbs them to the lowest gradient position in a $3\times3$ neighborhood.
      * Iteratively assigns pixels to the nearest center based on a weighted distance metric combining Color distance ($d_{lab}$) and Spatial distance ($d_{xy}$).
      * Post-processing enforces connectivity.
  * **Running the script:**
    ```bash
    python q3.py
    # When prompted for 'k', enter the desired number of superpixels (e.g., 64, 256, 1024).
    ```
  * **Output:** Saves the image with drawn contours as `res06.jpg` (or similar depending on $K$).

### 4\. Interactive Segmentation (`q4.py`)

Uses the GrabCut algorithm with a custom mouse-callback interface for user-guided segmentation.

  * **Methodology:**
      * Loads `birds.jpg`.
      * **Interaction:**
          * **Left Click & Drag:** Draws **Blue** lines (Foreground).
          * **Right Click:** Toggles drawing mode.
          * **Mouse Move (in Mode 2):** Draws **Red** lines (Background).
          * **Double Left Click:** Executes the segmentation.
  * **Running the script:**
    ```bash
    python q4.py
    ```
  * **Output:** Displays the result and saves the final segmented object as `res10.jpg`.

### 5\. Active Contours / Snakes (`q5.py`)

Detects the boundary of an object (specifically a rosary/tasbih) using energy minimization.

  * **Methodology:**
      * Loads `tasbih.jpg`.
      * Calculates image gradients using Sobel filters (Internal Energy).
      * **User Input:** Click center and drag to define the initial circular radius around the object.
      * **Optimization:** Uses the **Viterbi Algorithm** to iteratively minimize the total energy (Gradient + Elasticity + Curvature + Central Force).
  * **Running the script:**
    ```bash
    python q5.py
    ```
      * *Action:* Click on the center of the object, drag outward to create a circle enclosing the object, and release. The algorithm will animate the contour shrinking.
  * **Output:** Generates a video `contour.mp4` of the convergence and saves the final image as `res11.jpg`.

## Contributing

Contributions are welcome\!

1.  Fork the repository.
2.  Create a feature branch (`git checkout -b feature/AmazingFeature`).
3.  Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4.  Push to the branch (`git push origin feature/AmazingFeature`).
5.  Open a Pull Request.

## License

This project is open-source and available under the [MIT License](https://www.google.com/search?q=LICENSE).

## Contact

For questions regarding the algorithms or implementation details, please open an issue in this repository.
