# Cross_camera_tracking-YOLO
## Player Tracking and Matching Across Camera Feeds

This project uses basic fine-tuned version of Ultralytics YOLOv11 and traditional features (Histogram + HOG) to track and match players across different video feeds (broadcast and tacticam).

### Features
- Object detection and tracking using YOLO + BoT-SORT
- Feature extraction using color histograms and HOG
- Cosine similarity matching across feeds
- Saves annotated output videos

### Installation
- Open The NoteBook in Colab
- Connect to the T4 GPU runtime
- Upload the Best.pt, broadcast.mp4, tacticam.mp4 to the root directory
- Run all the cell
- Two videos will be downloaded and Output will be shown.
