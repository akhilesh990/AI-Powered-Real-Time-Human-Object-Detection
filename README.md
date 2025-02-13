# AI-Powered-Real-Time-Human-Object-Detection
AI-Powered Real-Time Human &amp; Object Detection uses the YOLOv8 model for real-time detection of humans and objects via webcam. The program captures two images per session, saving them for analysis. After capturing, users can choose to continue or stop. Ideal for quick object detection applications.
Key Features:
Real-Time Detection: Detects humans and various objects using YOLOv8 (You Only Look Once) model.
Customizable Detection: The model is pre-trained on common object classes but can be customized to detect specific objects with additional training.
User-Friendly Interface: After capturing two photos, the user is prompted to either continue or stop the process.
Photo Capture: Automatically captures two images per session and saves them for further analysis.
Efficient and Fast: Designed for real-time object detection using a webcam, ensuring quick response times and minimal latency.
Requirements:
Python 3.x
OpenCV
ultralytics (for YOLOv8)
YOLOv8 model weights (yolov8n.pt)
Setup:
Clone the repository:

bash
Copy
Edit
git clone https://github.com/yourusername/AI-Powered-Real-Time-Human-Object-Detection.git
cd AI-Powered-Real-Time-Human-Object-Detection
Install required dependencies:

bash
Copy
Edit
pip install -r requirements.txt
Download the YOLOv8 model weights (yolov8n.pt) from Ultralytics and place them in the project directory.

Run the script:

bash
Copy
Edit
python detection.py
How it Works:
When the script starts, the user is prompted to press "Yes" to begin object detection or "No" to exit the program.
The program then activates the webcam, captures frames, and performs object detection using YOLOv8.
The first two detected objects are saved as images in the detected_objects/ directory.
After capturing the two images, the program prompts the user with an option to continue capturing or to stop and exit.
The final output will be saved, and the program will display a message with the location of the saved images.
Output:
The detected objects are saved as images in the detected_objects/ directory.
The program also displays the webcam feed with bounding boxes and labels around the detected objects in real-time.
Contributions:
Contributions are welcome! Feel free to fork this repository, submit issues, or create pull requests.
