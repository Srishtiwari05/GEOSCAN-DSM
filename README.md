# GeoScan

A geospatial image analysis application that performs change detection and image segmentation on satellite/aerial imagery using deep learning.

## Overview

GeoScan is a web-based application that uses machine learning to detect environmental changes and segment regions in satellite or aerial images. The system combines a Python Flask backend with TensorFlow for image processing and a modern web frontend.

Live Demo / Deployed: https://geo-scan-lake.vercel.app/

## Features

- **Change Detection**: Identify changes between two satellite images
- **Image Segmentation**: Segment specific regions (A, B) and masks from imagery
- **TIFF Image Support**: Process GIS-standard raster formats using rasterio
- **Real-time Processing**: Web API for on-demand image analysis
- **Deep Learning Model**: Pre-trained TensorFlow model for accurate detection
- **Web Interface**: Interactive UI for uploading and analyzing images

## Project Structure

```
GeoScan/
├── backend/                  # Flask backend server
│   ├── app.py               # Main Flask application
│   ├── test_post.py         # Testing file
│   ├── train.py             # Model training script
│   ├── model/               # ML model components
│   │   ├── model_architecture.py
│   │   ├── train_model.py
│   │   └── weights/
│   │       └── best_model.h5   # Pre-trained model weights
│   ├── utils/               # Utility modules
│   │   ├── data_loader.py
│   │   └── tiff_processor.py
│   ├── datasets/            # Training/sample datasets
│   │   └── images/
│   │       ├── A/           # Category A images
│   │       ├── B/           # Category B images
│   │       └── mask/        # Segmentation masks
│   └── tmp_dataset/         # Temporary dataset storage
├── frontend/                # Web interface
│   ├── index.html
│   ├── region-development.html
│   ├── script.js            # Client-side logic
│   ├── style.css            # Styling
│   └── media/               # Frontend media assets
├── datasets/                # Additional datasets
│   └── images/
│       ├── A/
│       ├── B/
│       └── mask/
└── requirements.txt         # Python dependencies
```

## Tech Stack

**Backend:**
- Python 3.x
- Flask - Web framework
- TensorFlow - Deep learning
- OpenCV - Computer vision
- Rasterio - GIS raster processing
- NumPy, Pandas - Data processing

**Frontend:**
- HTML5
- CSS3
- JavaScript

**Tools & Libraries:**
- scikit-image - Image processing algorithms
- scikit-learn - Machine learning utilities
- Pillow - Image manipulation
- Matplotlib - Visualization

## Installation

### Prerequisites
- Python 3.8 or higher
- pip package manager

### Setup

1. **Clone the repository**
   ```bash
   cd GeoScan
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Verify model weights**
   - Ensure `backend/model/weights/best_model.h5` exists
   - If missing, train a new model using `backend/train.py`

## Usage

### Running the Backend Server

```bash
cd backend
python app.py
```

The Flask server will start and be available at `http://localhost:5000`

### API Endpoints

#### Change Detection
- **Endpoint**: `POST /detect-changes`
- **Request Format**:
  ```json
  {
    "image1": "base64_encoded_image_data",
    "image2": "base64_encoded_image_data"
  }
  ```
- **Response**: Detection results with change masks and confidence scores

### Web Interface

1. Open `frontend/index.html` in a web browser
2. Upload two satellite images
3. Click "Detect Changes" to analyze
4. View results and download segmentation masks

## Training the Model

To train a new model on your dataset:

```bash
cd backend
python train.py
```

The training script will:
- Load images from `datasets/images/A/`, `datasets/images/B/`, and `datasets/images/mask/`
- Train a TensorFlow model on change detection
- Save weights to `model/weights/best_model.h5`

## Data Format

### Input Images
- **Format**: PNG, JPG, or TIFF
- **Size**: Flexible (automatically resized to 256×256 for processing)
- **Channels**: RGB or Grayscale

### Masks
- **Format**: Binary or multi-class segmentation masks
- **Convention**: Same spatial dimensions as corresponding images

## Testing

Run the test suite:

```bash
cd backend
python test_post.py
```

## Configuration

Key settings in `backend/app.py`:
- **Model Path**: `backend/model/weights/best_model.h5`
- **Input Size**: 256×256 pixels
- **CORS**: Enabled for cross-origin requests

## Performance

- **Inference Time**: ~100ms per image pair (GPU)
- **Supported Resolution**: Up to 4K images (automatically downsampled)
- **Concurrent Requests**: Handled by Flask thread pool

## Troubleshooting

### Model Not Loading
```
Issue: "Model file not found" warning at startup
Solution: Train a new model or provide best_model.h5 file
```

### CORS Errors
```
Issue: Frontend cannot reach backend
Solution: Ensure CORS is enabled in app.py and backend is running
```

### Out of Memory
```
Issue: Processing large images crashes
Solution: Adjust batch size in preprocessing or use GPU acceleration
```

## Future Enhancements

- [ ] Real-time WebSocket updates for large files
- [ ] Support for multi-temporal analysis (3+ images)
- [ ] Cloud storage integration (AWS S3, Google Cloud)
- [ ] Advanced visualizations and heatmaps
- [ ] Model deployment to cloud platforms
- [ ] Batch processing API
- [ ] Mobile-responsive frontend

## Dependencies Management

Update dependencies periodically:
```bash
pip install --upgrade -r requirements.txt
```

For CPU-only systems, replace `tensorflow` with `tensorflow-cpu` in requirements.txt.

## License

[Add your license here]

## Contact

For issues, questions, or contributions, please contact the development team.

---

**Last Updated**: April 2026
