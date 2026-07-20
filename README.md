#  Satellite Images Water Segmentation

A deep learning pipeline built in PyTorch for high-precision water body segmentation using multi-spectral satellite imagery. This project processes 12-band GeoTIFF images to train and evaluate a segmentation model, tracking performance across various learning rates to optimize precision, recall, F1-Score, and Intersection over Union (IoU).

## Dataset

The dataset consists of multi-channel GeoTIFF images (`.tif`), each containing 12 distinct bands encompassing spectral reflectance, digital elevation models (DEM), and quality assessment data.

### Image Specifications
*   **Dimensions:** All input images are uniformly pre-processed to a strict `(12, 128, 128)` dimensional shape.
*   **Data Type:** `float32`.

### The 12 Channels Include
1. Coastal Aerosol
2. Blue
3. Green
4. Red
5. Near-Infrared (NIR)
6. Shortwave Infrared 1 (SWIR 1)
7. Shortwave Infrared 2 (SWIR 2)
8. QA Band
9. Merit DEM
10. Copernicus DEM
11. ESA World Cover
12. Water Occurrence Probability

> **Note:** Raw satellite values can contain negative values (e.g., Coastal Aerosol and Blue bands), which are preserved in the raw matrices but normalized dynamically for visual rendering.

---

## Installation & Requirements

Ensure you have Python 3.12+ installed. Clone this repository and install the required dependencies:

```bash
git clone https://github.com/your-username/water-segmentation.git
cd water-segmentation
pip install -r requirements.txt
```

### Core Dependencies
*   `torch` (PyTorch)
*   `tifffile`
*   `numpy`
*   `matplotlib`
*   `opencv-python` (`cv2`)
*   `scikit-learn`

---

##  Usage

### 1. Data Visualization
To inspect the 12 individual bands of a specific `.tif` sample, a visualization function is provided. It automatically applies Min-Max scaling to handle the high dynamic ranges of satellite bit-depths and displays them in a 3x4 grid.

```python
from utils import visualize_12_bands

# Visualize a single sample
visualize_12_bands("data/images/105.tif")
```

![Band_representation](/images/image_bands.png)

### 2. Training the Model
Run the main Jupyter Notebook (`water_segmentation.ipynb`) or the extracted Python script to initialize the training loop.

The pipeline includes automatic dataset splitting (`train_test_split`) and loads data via PyTorch `DataLoader`.

---

## 📈 Training Metrics & Evaluation

The model was evaluated over 150 epochs using different learning rates to test stability and convergence. The following metrics were monitored:
*   Loss (Training vs. Validation)
*   Precision & Recall
*   F1-Score
*   IoU (Intersection over Union)

### Learning Rate Comparisons
*   **LR = 1e-5:** Demonstrates highly stable and uniform convergence. The training and validation curves track closely together, showcasing excellent generalization with minimal overfitting.
*   **LR = 1e-4:** Exhibits significantly faster initial optimization, reaching high performance benchmarks earlier in the training lifecycle, though with higher early-epoch volatility.

### Visual Results

| Learning Rate: 1e-5 | Learning Rate: 1e-4 |
| :---: | :---: |
| ![Metrics 1e-5](/images/Metrics_1e-5.png) | ![Metrics 1e-4](/images/Metrics_1e-4.png) |

---
