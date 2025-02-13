import cv2
import os
from ultralytics import YOLO

# Create a directory to save detected objects
save_dir = "detected_objects"
os.makedirs(save_dir, exist_ok=True)

# Load YOLOv8 model
model = YOLO("yolov8n.pt")

# Open Webcam
cap = cv2.VideoCapture(0)

frame_count = 0  # Counter for naming saved images
photo_count = 0  # Counter for photos captured in the session

# Ask user to start the detection process
while True:
    user_input = input("Do you want to start object detection? (Yes/No): ").strip().lower()
    if user_input == "yes":
        break
    elif user_input == "no":
        print("Exiting program.")
        exit()
    else:
        print("Invalid input. Please enter 'Yes' or 'No'.")

while True:
    ret, frame = cap.read()
    if not ret:
        break

    results = model(frame)  # Perform detection

    # Display detection results and draw bounding boxes
    for result in results:
        for i, box in enumerate(result.boxes):
            x1, y1, x2, y2 = map(int, box.xyxy[0])  # Bounding box coordinates
            label = model.names[int(box.cls)]  # Get class label
            confidence = box.conf[0].item()  # Get confidence score

            # Draw bounding box
            cv2.rectangle(frame, (x1, y1), (x2, y2), (0, 255, 0), 2)
            cv2.putText(frame, f"{label} {confidence:.2f}", (x1, y1 - 10),
                        cv2.FONT_HERSHEY_SIMPLEX, 0.5, (0, 255, 0), 2)

            # Save detected object as an image (if photo_count < 2)
            if photo_count < 2:
                object_img = frame[y1:y2, x1:x2]
                object_filename = f"{save_dir}/{label}_{frame_count}_{i}.jpg"
                cv2.imwrite(object_filename, object_img)
                photo_count += 1  # Increment photo count

    frame_count += 1

    # Display the detection frame
    cv2.imshow("Detection", frame)

    # Stop after 2 photos and show final output
    if photo_count >= 2:
        cv2.putText(frame, "2 photos captured! Press 'q' to quit.", (10, 30),
                    cv2.FONT_HERSHEY_SIMPLEX, 0.8, (0, 255, 0), 2)
        cv2.imshow("Detection", frame)

        key = cv2.waitKey(1) & 0xFF
        if key == ord('q'):  # If 'q' is pressed, quit the program
            break

    cv2.waitKey(1)

cap.release()
cv2.destroyAllWindows()

# Display the final output after capturing 2 photos
print(f"Detected images are saved in the directory: {save_dir}")
print("Program has finished. Exiting.")

