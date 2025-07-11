🎯 Objective
The goal of this project is to track football players across two video feeds (broadcast and tacticam) using object detection, tracking, and feature matching techniques. The final output includes videos with annotated tracking IDs and a mapping of corresponding players between views.

🧠 Approach & Methodology
1. Detection & Tracking
  Model: YOLO Ultralytics (best.pt) trained on a custom dataset.
  
  Tracking: Used BoT-SORT to assign unique IDs to players.
  
  Condition: Only track class 2 (player class) as detected by YOLO.

2. Feature Extraction
Histogram (Hist):
  
  Used color histograms in the RGB space (8x8x8 bins).
  
  Good for color-based differentiation.
  
HOG (Histogram of Oriented Gradients):
  
  Captures the shape and edge orientation within player crops.
  
  Resized each crop to a fixed size before applying HOG.

Combined Approach:

  Concatenated normalized color histogram with HOG descriptors.
  
  Provided better robustness against illumination and camera angle variation.

3. Feature Aggregation
  For each track_id, features were averaged across all frames where the player appeared.
  
  Resulted in a compact representation per player per video.

4. Matching Across Feeds
  Used cosine similarity to compare each player in the tacticam video with all players in the broadcast video.
  
  Assigned the most similar match if similarity score > 0.7.

🧪 Techniques Tried and Their Outcomes
Technique	Outcome
  Only Histogram	Fast, but poor in matching players with similar kits.
  Only HOG	Sensitive to scale and orientation changes.
  Histogram + HOG	Best performance, achieved decent matching in varied conditions.
  Deep features (ReID)	Planned, implemented but the running time was too high due to this time constraints I discarded the code.

⚠️ Challenges Encountered
  Detection Instability: YOLO failed to consistently detect all players, especially when occluded.
  
  ID Switching: BoT-SORT sometimes switched IDs for overlapping players.
  
  Camera Differences: Broadcast and tacticam had large perspective and zoom shifts, making matching harder.
  
  Low Resolution Crops: Players occupy very few pixels, reducing feature reliability, even can't sort using jersey number because it wasn't always visible.

🧩 Remaining Work / Future Directions
  Improve Detector:
  
  Train on more varied datasets or fine-tune on multi-view game footage.
  
  Better Re-ID Embeddings:
  
  Use a pretrained ReID model for robust identity features, with better modelling for faster runs.
  
  Temporal Consistency:
  
  Apply temporal smoothing or LSTM on features for better cross-view matching.
  
  UI/Visualization:
  
  Build an interface to review matches interactively.

✅ Conclusion
  The current pipeline demonstrates end-to-end multi-view player tracking using classical and ML-based vision tools. Although performance is limited by detection and feature fidelity, combining histogram and HOG showed a clear improvement. With better detectors and learned ReID features, this system could scale effectively to real-world sports analytics.

