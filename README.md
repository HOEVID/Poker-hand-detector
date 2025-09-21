# Real-Time Poker Hand Detector

![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)
![OpenCV](https://img.shields.io/badge/library-OpenCV-green.svg)
![NumPy](https://img.shields.io/badge/library-NumPy-blue.svg)

A computer vision project designed to identify playing cards from a live video stream or a static image and determine the best possible poker hand. This project was developed as an exercise to apply and enhance my skills in image processing and real-time object detection.

## Features

- **Real-Time Detection:** Identifies cards directly from a webcam feed.
- **Image-Based Detection:** Can also process static image files.
- **Card Recognition:** Detects both the rank (Ace, King, 7, etc.) and the suit (Hearts, Spades, etc.) of each card.
- **Hand Evaluation:** Analyzes the detected cards and prints the best poker hand (e.g., "Full House", "Straight", "Two Pair").

## How It Works

The detection pipeline follows several key computer vision steps to move from a raw image to a fully evaluated poker hand:

1.  **Image Pre-processing:** The input image is converted to grayscale, blurred to reduce noise, and then an adaptive threshold is applied. This isolates the cards, making them stand out as white objects on a black background.
2.  **Contour Detection:** The script finds all the objects (contours) in the processed image. It then filters these contours based on their size to identify plausible card-like shapes.
3.  **Perspective Transformation:** For each identified card, the corners are located. A perspective transform is then applied to "warp" the card into a flat, top-down view. This standardized view is crucial for accurate identification.
4.  **Rank and Suit Identification:** The warped card image is split into two regions of interest (ROIs): the top-left corner for the rank and the area just below it for the suit. A **template matching** algorithm compares these ROIs against a library of pre-saved template images (A, 2, 3,..., K and ♥, ♦, ♣, ♠) to find the best match.
5.  **Hand Evaluation:** Once all cards are identified, a set of logical rules evaluates them to determine the highest-ranking poker hand.

## Tech Stack

- **Python 3.8+**
- **OpenCV:** For all core computer vision tasks like image processing, contour detection, and transformations.
- **NumPy:** Used for numerical operations and handling image data as matrices.

## Setup and Installation

Follow these steps to get the project running on your local machine.

**1. Prerequisites:**
* Python 3.8 or newer
* pip package manager

**2. Clone the Repository:**
```bash
# Replace YourUsername and YourRepositoryName with your actual details
git clone [https://github.com/YourUsername/YourRepositoryName.git](https://github.com/YourUsername/YourRepositoryName.git)
cd YourRepositoryName/poker-hand-detector
```

**3. Install Dependencies:**
A `requirements.txt` file is included to manage dependencies. Run the following command in the project directory:
```bash
pip install -r requirements.txt
```

## Usage

You can run the detector on a live webcam feed or provide a path to an image file.

**To use your webcam:**
```bash
python main.py 
```
*(Note: You might need to change the file name if the main script is not `main.py`)*

**To use a static image file:**
*(This is a potential feature, you may need to check the code to see if it's supported or add it yourself)*
```bash
python main.py --image path/to/your/image.jpg
```

Press the 'q' key to exit the live feed window.

## Challenges and What I Learned

This project was a fantastic learning experience. Some of the key challenges included:

-   **Lighting Invariance:** Making the card detection robust under different lighting conditions was difficult. I overcame this by using adaptive thresholding instead of a simple global threshold.
-   **Template Matching Accuracy:** Getting the template matching to work reliably required careful tuning of the template images and the comparison logic.

Through this project, I gained significant practical experience in the entire computer vision pipeline—from low-level image manipulation and filtering to higher-level object detection and recognition logic.

## Future Improvements

-   **Improve Model Robustness:** Replace template matching with a lightweight Convolutional Neural Network (CNN) trained on card ranks and suits to improve accuracy with different fonts and lighting.
-   **Develop a GUI:** Build a simple graphical user interface using Tkinter or PyQt to make the application more user-friendly.
-   **Code Optimization:** Profile the code to identify and optimize bottlenecks for smoother real-time performance.
