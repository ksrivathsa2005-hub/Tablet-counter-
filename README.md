# Automated Tablet Inspection System

A computer vision-based system for automated tablet detection, counting, and quality inspection using classical image processing techniques. This project leverages OpenCV and Gradio to provide an interactive web interface for tablet quality control.

## 🎯 Features

- **Tablet Detection**: Automatically detects and counts tablets in images using watershed segmentation
- **Shape Classification**: Classifies tablets into three categories:
  - **Round**: Circular tablets with high circularity and aspect ratio close to 1
  - **Oval**: Elongated tablets with aspect ratio > 1.25
  - **Irregular**: Tablets that don't fit the above categories
- **Defect Detection**: Identifies defective tablets based on:
  - Low circularity (< 0.60)
  - Low solidity (< 0.80) indicating concave/broken shapes
  - High texture variance indicating cracks or surface anomalies
- **Interactive Web Interface**: User-friendly Gradio dashboard for real-time processing
- **Visual Feedback**: Annotated output images with color-coded classifications

## 📋 Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Methodology](#methodology)
- [Project Structure](#project-structure)
- [Technical Details](#technical-details)
- [Results](#results)
- [Future Improvements](#future-improvements)

## 🚀 Installation

### Prerequisites

- Python 3.7 or higher
- pip package manager

### Dependencies

Install the required packages:

```bash
pip install opencv-python numpy matplotlib gradio
```

Or install from requirements file (if available):

```bash
pip install -r requirements.txt
```

## 💻 Usage

### Running the Jupyter Notebook

1. Open `CV_mini_proj.ipynb` in Jupyter Notebook or Google Colab
2. Upload an image of tablets (supports common image formats: JPG, PNG, etc.)
3. Run all cells sequentially
4. The final cell will launch a Gradio web interface

### Using the Gradio Interface

1. Once the interface is launched, you'll receive a local or public URL
2. Upload a tablet image using the interface
3. View the processed results:
   - Annotated image with detected tablets
   - Summary statistics (Total, Round, Oval, Irregular, Defective counts)

### Color Coding

- 🟢 **Green**: Round tablets
- 🔵 **Blue**: Oval tablets
- 🟠 **Orange**: Irregular tablets
- 🔴 **Red**: Defective tablets

## 🔬 Methodology

The system employs a multi-stage image processing pipeline:

### 1. Preprocessing
- **Grayscale Conversion**: Converts input image to grayscale
- **Gaussian Blur**: Reduces noise using a 5×5 kernel
- **Otsu's Thresholding**: Automatic binary thresholding for segmentation

### 2. Segmentation
- **Morphological Operations**: Opening and dilation to separate touching objects
- **Distance Transform**: Identifies object centers
- **Watershed Algorithm**: Segments individual tablets, even when touching

### 3. Feature Extraction
For each detected tablet:
- **Circularity**: Measures how circular the shape is (4π × area / perimeter²)
- **Aspect Ratio**: Width to height ratio
- **Solidity**: Ratio of contour area to convex hull area
- **Texture Variance**: Local variance in pixel intensity

### 4. Classification
- **Adaptive Thresholding**: Uses statistical analysis of detected objects
- **Rule-Based Classification**: Combines multiple features for robust classification
- **Defect Detection**: Multi-criteria approach for identifying defects

## 📁 Project Structure

```
cv-mp/
│
├── CV_mini_proj.ipynb    # Main Jupyter notebook with implementation
├── README.md              # Project documentation
└── requirements.txt       # Python dependencies (optional)
```

## 🔧 Technical Details

### Key Algorithms

1. **Watershed Segmentation**: Separates touching or overlapping tablets
2. **Connected Components**: Identifies individual objects
3. **Contour Analysis**: Extracts shape features
4. **Distance Transform**: Locates object centers for segmentation

### Classification Thresholds

- **Round Tablets**: 
  - Circularity > 0.80
  - Aspect Ratio: 0.9 - 1.1
  
- **Oval Tablets**:
  - Aspect Ratio > 1.25
  - Circularity > 0.45
  
- **Defective Tablets**:
  - Circularity < 0.60 OR
  - Solidity < 0.80 OR
  - Texture Variance > mean + 1.5 × std

### Parameters

The system uses adaptive thresholds that adjust based on the input image:
- Minimum area threshold: `max(100, 0.15 × mean_area)`
- Texture variance threshold: `mean + 1.5 × standard_deviation`

## 📊 Results

The system successfully:
- Detects tablets even when they are touching or overlapping
- Classifies tablets by shape with high accuracy
- Identifies defective tablets using multiple criteria
- Provides real-time processing through a web interface

### Example Output

```
Total: 44
Round: 1
Oval: 8
Irregular: 20
Defective: 15
```

## 🎓 Use Cases

- **Pharmaceutical Quality Control**: Automated inspection of tablet batches
- **Manufacturing**: Real-time quality assurance on production lines
- **Research**: Analysis of tablet shape distribution
- **Education**: Learning computer vision and image processing techniques

## 🔮 Future Improvements

- [ ] Deep learning-based classification for improved accuracy
- [ ] Support for video input and real-time processing
- [ ] Batch processing for multiple images
- [ ] Export results to CSV/JSON format
- [ ] Customizable classification thresholds
- [ ] Additional defect types (cracks, chips, color variations)
- [ ] Integration with database for tracking and analytics
- [ ] Mobile app for on-the-go inspection

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 License

This project is open source and available under the MIT License.

## 👨‍💻 Author

Created as part of a Computer Vision mini-project.

## 🙏 Acknowledgments

- OpenCV community for excellent documentation
- Gradio for the intuitive web interface framework
- NumPy and Matplotlib for numerical computing and visualization

## 📧 Contact

For questions or suggestions, please open an issue on the repository.

---

**Note**: This project is designed for educational and research purposes. For production use in pharmaceutical or medical applications, additional validation and regulatory compliance may be required.

