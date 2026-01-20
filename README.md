# CNN MNIST TinyML Project

<div align="center">

[![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)](https://www.tensorflow.org/)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-F37626.svg?&style=for-the-badge&logo=Jupyter&logoColor=white)](https://jupyter.org/)
[![Raspberry Pi Pico](https://img.shields.io/badge/Raspberry%20Pi%20Pico-B0BD00?style=for-the-badge&logo=Raspberry-Pi&logoColor=white)](https://www.raspberrypi.com/products/raspberry-pi-pico/)
[![C](https://img.shields.io/badge/C-A8B9CC?style=for-the-badge&logo=c&logoColor=white)](https://en.wikipedia.org/wiki/C_(programming_language))

</div>

## Overview

This project implements a Convolutional Neural Network (CNN) for handwritten digit recognition using the MNIST dataset, specifically optimized for deployment on microcontrollers like the Raspberry Pi Pico. The model is trained using TensorFlow and converted to TensorFlow Lite (TFLite) format with INT8 quantization for efficient execution on resource-constrained devices.

## Features

- **Lightweight CNN Architecture**: Designed specifically for TinyML applications
- **TFLite Conversion**: Optimized INT8 quantization for microcontroller deployment
- **Complete Training Pipeline**: From data preprocessing to model evaluation
- **Performance Metrics**: Comprehensive evaluation with accuracy, confusion matrix, and classification reports
- **Hardware Ready**: Ready for deployment on Raspberry Pi Pico and similar microcontrollers

## Repository Structure

```
cnn_mnist_tinyML/
├── notebooks/                 # Jupyter notebooks for training
│   └── Model_Training.ipynb   # Main training notebook
├── firmware/                  # Microcontroller firmware
│   ├── cnn_mnist.c            # Main inference code
│   ├── tflm_wrapper.cpp       # TensorFlow Lite Micro wrapper
│   └── tflm_wrapper.h         # Header file for TFLM wrapper
├── models/                    # Trained models (TFLite format)
├── Images/                    # Generated plots and visualizations
├── test/                      # Test data and samples
├── pico-tflmicro/             # TensorFlow Lite Micro library
├── build/                     # Build artifacts
├── README.md                  # This file
└── CMakeLists.txt             # Build configuration
```

### Notebooks

Contains the main training notebook with comprehensive implementation:

- **Data Preprocessing**: Loading and preparing MNIST dataset
- **Model Architecture**: Lightweight CNN design optimized for TinyML
- **Training Process**: Complete training with validation
- **Evaluation**: Performance metrics and visualizations
- **Model Conversion**: TFLite conversion with INT8 quantization

<div align="center">
<img src="Images/mnist_sample_images_first_10.png" alt="MNIST Sample Images" width="600"/>
<p><em>Sample MNIST images used for training</em></p>
</div>

### Firmware

Microcontroller-side implementation:

- **CNN Inference**: Efficient inference engine for microcontrollers
- **TFLM Wrapper**: Interface with TensorFlow Lite Micro
- **Serial Communication**: Data transfer and result reporting

### Models

Contains the converted TFLite models:

- **Quantized Models**: INT8 quantized for efficient execution
- **Header Files**: C-compatible header files for embedding
- **Size Optimized**: Minimal memory footprint for microcontrollers

<div align="center">
<img src="Images/cnn_training_validation_curves.png" alt="Training Curves" width="600"/>
<p><em>Training and validation curves showing model performance</em></p>
</div>

### Images

Generated visualizations from the training process:

- **Sample Images**: Visualization of MNIST dataset samples
- **Training Curves**: Accuracy and loss over epochs
- **Confusion Matrix**: Detailed performance breakdown
- **Validation Results**: Model predictions on test samples

<div align="center">
<img src="Images/confusion_matrix_cnn_mnist.png" alt="Confusion Matrix" width="600"/>
<p><em>Confusion matrix showing model performance across all digit classes</em></p>
</div>

### Test

Test data and validation files:

- **Test Samples**: Preprocessed test data for validation
- **Validation Scripts**: Scripts to verify model performance
- **Performance Benchmarks**: Comparison metrics

### Build System

- **CMake Integration**: Cross-platform build system
- **Pico SDK**: Integration with Raspberry Pi Pico SDK
- **TFLM Integration**: TensorFlow Lite Micro integration

## Architecture

### Model Architecture
```
Input (28x28x1)
    ↓
Conv2D (8 filters, 3x3, stride=2) → 14x14x8
    ↓
Conv2D (16 filters, 3x3, stride=2) → 7x7x16
    ↓
Global Average Pooling → 16
    ↓
Dense (10 units, softmax) → 10 (digit classes)
```

### Key Features
- **Total Parameters**: ~1,418 (less than 6KB)
- **Quantization**: INT8 for memory efficiency
- **Layers**: 4 layers (2 conv + 1 pooling + 1 dense)
- **Operations**: Optimized for microcontroller execution

## Getting Started

### Prerequisites
- Python 3.7+
- TensorFlow 2.x
- Jupyter Notebook
- Raspberry Pi Pico SDK (for hardware deployment)

### Training the Model
1. Navigate to the `notebooks/` directory
2. Open `Model_Training.ipynb`
3. Run all cells to train and convert the model

### Deploying to Hardware
1. Convert model to header file format
2. Copy to `firmware/` directory
3. Build using CMake with Pico SDK
4. Flash to Raspberry Pi Pico

## Performance

- **Training Accuracy**: ~89%
- **Validation Accuracy**: ~88%
- **Test Accuracy**: ~88.8%
- **Model Size**: ~5KB (INT8 quantized)
- **Inference Time**: < 10ms on Pico

## Contributing

Contributions are welcome! Feel free to submit pull requests or open issues for bugs and feature requests.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- [TensorFlow Lite Micro](https://www.tensorflow.org/lite/microcontrollers) for enabling ML on microcontrollers
- [MNIST Dataset](http://yann.lecun.com/exdb/mnist/) for the handwritten digit dataset
- [Raspberry Pi Foundation](https://www.raspberrypi.org/) for the Pico platform