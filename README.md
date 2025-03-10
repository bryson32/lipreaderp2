# Lip Reader
![Demo](demo.gif)
 
## Lip-Reading Computer Vision: A Proof of Concept for Deaf Communication Assistance
Project Overview: 
This project is a real-time lip-reading AI designed as a proof of concept to assist deaf and hard-of-hearing individuals in understanding spoken words by analyzing lip movements. Using computer vision and deep learning, the system captures, preprocesses, and classifies lip movements to predict spoken words without relying on audio input.

By leveraging a 3D Convolutional Neural Network (3D CNN), the model learns temporal and spatial patterns in lip movements, enabling real-time predictions. This project explores the intersection of AI and accessibility, demonstrating the potential of lip-reading technology for assistive communication.

### [Training Logs & Notes (Please Read)](./TRAINING_LOGS.md)

<img src="validations.png" alt="chart" height="600"/>
<img src="P-R-F-Scores.png" alt="chart" height="700"/>

## Key Features
- Custom Lip-Reading Model: A 3D CNN trained on real-world lip movement data.
- Real-Time Prediction: Uses a webcam for live lip-tracking and word recognition.
- Automated Data Collection: Efficient frame extraction and storage for training.
- Advanced Preprocessing: Multi-step image processing for enhanced model accuracy.
- Optimized Training Pipeline: Uses Adam optimization and categorical cross-entropy loss.

## Source Code Architecture
```
├── collection.py          Captures lip images for a specified word using a webcam.
├── preprocess.py          Processes and normalizes recorded frames for training.
├── train_model.py         Builds and trains a 3D CNN on the preprocessed data.
├── predict.py             Runs a live lip-reading demo using the trained model.
```
## Implementation Breakdown
### 1. Data Collection
- Uses Dlib for face and landmark detection to extract the lip region.
- Records 22 frames per word per take, ensuring consistent input dimensions.
- Saves each take in a structured format for easier training.

### 2. Data Preprocessing
To improve recognition accuracy, each lip sequence undergoes:

- Grayscale conversion (reduces unnecessary color data).
- Gaussian blurring (removes noise while preserving important features).
- Contrast stretching (enhances lip visibility).
- Bilateral filtering (smooths noise while keeping edges).
- Edge sharpening (enhances clarity of lip movements).
- Normalization (scales pixel values between 0 and 1 for stable training).
- Preprocessed data is stored in .npy format, ensuring efficient model input.

### 3. 3D CNN Architecture
- 3D Convolutional layers to extract spatial and temporal features from the lip movement sequences.
- Max-Pooling layers to reduce feature dimensions.
- Fully connected layers for classification.
- Softmax activation for multi-class word prediction.
- Input Shape: (22, 80, 112, 1) (22 frames, 80x112 pixel grayscale images, 1 channel).

### 4. Model Training
- Dataset: Custom-recorded words with 80/20 train-validation split.
- Loss Function: Sparse Categorical Cross-Entropy (for multi-class classification).
- Optimizer: Adam (learning rate = 0.0003) for efficient convergence.
- Training Strategy: Batch size = 16, trained for 20 epochs.

### 5. Real-Time Prediction
- Uses a webcam feed to detect and track lip movements.
- Captures a 22-frame sequence before making a prediction.
- Matches prediction to the closest trained word.
- Displays the predicted word on screen in real time.

### Why This Project Matters
- Accessibility & Inclusion: Bridges communication gaps for deaf and hard-of-hearing individuals.
- AI & Human Interaction: Demonstrates practical applications of deep learning in assistive technology.
- Computer Vision & NLP Fusion: A step towards integrating lip reading with voice-to-text systems.
- Real-World Deployment Potential: Could be extended into speech-to-text apps, smart glasses, or AR interfaces.

## Usage
- **Data Collection:** Run `python collection.py`
- **Preprocessing:** Run `python preprocess.py`
- **Model Training:** Run `python train_model.py`
- **Live Prediction:** Run `python predict.py`

## Future Improvements
- Automated triggering of data collection based on lip movement.
- Improved model generalization with a diverse dataset.
- Enhanced real-world deployment (e.g., integration with AR devices).

# NOTE
- If you try to use my weights, it will SURELY not work, as my weights are trained to my lips and my lips only. The data collection method is also not incredible as it requires extreme precision when you click l -> recording. I plan on rewriting the data collection to be automated, and start at the exact moment your lips start moving, to remove this need for extreme precision.
