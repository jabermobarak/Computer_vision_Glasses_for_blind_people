# Computer Vision Glasses for Blind People
### Object Detection and Text Reading with Spoken Feedback

An assistive vision prototype designed to support blind and visually impaired users through object recognition, text reading, and spoken feedback.

The Python application retrieves images from a network camera, processes them with computer vision, and announces recognized objects or text.

## Features

- Image capture from an HTTP camera endpoint.
- Object detection with bounding boxes using `cvlib`.
- English text recognition using EasyOCR.
- Spoken descriptions using `pyttsx3`.
- Keyboard controls to switch between object detection and text reading.
- A separate Arduino sketch demonstrating joystick input, a buzzer, an LED, and a seven-segment display.

## How It Works

1. Retrieve an image from the configured camera URL.
2. Decode and resize the image to 320 × 240 pixels.
3. Process the image using the selected mode:
   - **Object mode:** detect objects, draw bounding boxes, and announce their labels.
   - **Text mode:** recognize English text and read it aloud.
4. Display the camera image in an OpenCV window.

Object detection and text recognition run as separate modes.

## Controls

| Key | Action |
|---|---|
| `o` | Toggle object detection |
| `t` | Toggle text recognition |
| `q` | Quit the application |

Both recognition modes are initially disabled.

## Technology

| Component | Technology |
|---|---|
| Main application | Python |
| Image processing and display | OpenCV |
| Object detection | cvlib |
| Text recognition | EasyOCR |
| Spoken feedback | pyttsx3 |
| Image arrays | NumPy |
| Camera image retrieval | urllib |
| Hardware demonstration | Arduino / C++ |

The script also imports and initializes `googletrans`, but translation is not used in the current recognition workflow.

## Repository Structure

| Path | Purpose |
|---|---|
| `Computer_vision_Glass_for_blind_people-main/objecreco.py` | Camera capture, object detection, OCR, and speech |
| `Computer_vision_Glass_for_blind_people-main/sketch_apr3a/sketch_apr3a.ino` | Standalone Arduino hardware demonstration |
| `By_my_eyes_glasses_report.pdf` | Project report |

## Getting Started

### Requirements

- Python environment with the required packages.
- A network camera exposing a JPEG image through HTTP.
- A computer with a graphical display and audio output.
- Network access to the camera.
- Internet access for initial model downloads when required.

### Installation

Clone the repository:

```bash
git clone https://github.com/jabermobarak/Computer_vision_Glasses_for_blind_people.git
cd Computer_vision_Glasses_for_blind_people
```

Create and activate a virtual environment:

```bash
python -m venv .venv
```

On Windows:

```powershell
.venv\Scripts\activate
```

On Linux or macOS:

```bash
source .venv/bin/activate
```

Install the Python dependencies:

```bash
pip install opencv-python cvlib numpy pyttsx3 easyocr tensorflow googletrans
```

The repository does not provide pinned dependency versions. Package compatibility may require adjustments, particularly for the `googletrans` API used by the script.

### Configure the Camera

Open `Computer_vision_Glass_for_blind_people-main/objecreco.py` and replace the camera URL with your device’s HTTP image endpoint:

```python
url = 'http://YOUR_CAMERA_IP/cam-hi.jpg'
```

Ensure the computer can access this address.

### Configure Speech

The script selects the second available system voice:

```python
engine.setProperty('voice', voices[1].id)
```

If your system has only one voice, change `voices[1]` to `voices[0]`. A compatible system speech engine must be available.

### Run

```bash
python Computer_vision_Glass_for_blind_people-main/objecreco.py
```

Focus the OpenCV window and press `o` for object detection or `t` for text reading. Press `q` to exit.

## Arduino Demonstration

The included sketch demonstrates:

- A startup buzzer sound.
- Joystick-controlled counter changes.
- Counter reset through the joystick button.
- LED feedback during reset.
- Seven-segment display output.

| Component | Arduino pin |
|---|---|
| Buzzer | 11 |
| LED | 12 |
| Joystick button | 10 |
| Joystick X axis | A0 |
| Joystick Y axis | A1 |
| Display segments A–G | 2–8 |

Open `sketch_apr3a.ino` in the Arduino IDE, select the appropriate board and port, and upload it.

The sketch operates independently; the current code does not connect it to the Python recognition application.

## Current Limitations

- Text recognition is configured for English.
- Speech runs synchronously and can delay image processing.
- Camera connection failures are not handled explicitly.
- Recognition quality depends on lighting, image resolution, and camera positioning.
- The repository does not include accuracy, latency, or user evaluation results.
- The implementation is a prototype rather than a validated navigation system.

## Future Improvements

- Handle camera disconnections and invalid frames.
- Reduce repeated spoken announcements.
- Run speech asynchronously.
- Add configurable recognition thresholds.
- Support additional OCR languages.
- Connect hardware controls to recognition modes.
- Evaluate recognition accuracy, response time, and usability.

## Report

[Read the project report](By_my_eyes_glasses_report.pdf)

## Author

**Jaber Mobarak**

[GitHub](https://github.com/jabermobarak)

https://github.com/user-attachments/assets/5d9e2ac4-a973-4584-82b8-84411879be8f

