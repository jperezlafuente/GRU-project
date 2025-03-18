# League of Legends Minion Wave Collision Analysis

## 📌 Project Overview
This project analyzes minion wave behavior in League of Legends by detecting minions in video footage and identifying the collision points of red and blue minion waves in each lane. The goal is to provide insights into wave control and lane dynamics without revealing the full implementation details.

## 🏆 Objective
The primary goal of this project is to gather information on **wave positions in professional League of Legends matches**, data that is not provided by Riot’s official partner GRID. To achieve this, the following process is followed:

1. **Labeling images of minions on the minimap**
2. **Developing a computer vision model (YOLOv8) for detection**
3. **Extracting videos of professional matches**
4. **Processing videos to detect minions in real-time**
5. **Enhancing the dataset with additional game data**
6. **Calculating the final wave positions per lane**

## 🔬 Step 1: Labeling Images for Training
To train a computer vision model, I first manually labeled images of minions on the minimap using **LabelImg**. This step involves:

- Capturing minimap snapshots from recorded games.
- Annotating each minion’s position as **bounding boxes**.
- Ensuring the labels correctly distinguish between red and blue minions.

📷 *Example of labeled image:*
![Labeled Minimap Example](visuals/labeled_minimap.png)

## 🤖 Step 2: Training the Detection Model
A **YOLOv8-based** computer vision model was trained using the labeled images to accurately detect minions. Training setup:

- **Dataset:** 5000 labeled frames
- **Training epochs:** 300
- **Accuracy Results:**
  - **Precision-Recall Score:** 97.1%
  - **Mean Average Precision (mAP):** 95.3%

📊 *Precision-Recall Curve:*
![PR Curve](visuals/PR_curve.png)

*Additional tests included evaluating detection performance on unseen games.*

## 🎥 Step 3: Extracting Match Videos
Professional League of Legends matches are stored as **ROFL replay files** via Riot’s **GRID platform**. However, **Riot does not provide an official method to extract them as videos**.

To overcome this:
- **ReplayBook** was used to play the replays.
- **Replays.xyz** was used to convert them into standard video format.
- The full matches were recorded and stored for processing.

## 🛠️ Step 4: Processing Videos for Minion Detection
With the trained YOLOv8 model, the next step was **processing the match footage to extract minion positions**:

- **Splitting video frames** at regular intervals.
- **Running YOLOv8 detection** on each frame.
- **Mapping detected minimap coordinates** to real in-game map positions (**X: 0-14750, Y: 0-14850**).
- **Extracting timestamps** using OCR to synchronize data with game time.

## 📊 Step 5: Enhancing Data with Additional Game Information
To improve the dataset and clean potential inaccuracies, I incorporated:

- **GRID data** on **champion attacks on minions** (useful when champions obscure minions on the minimap).
- **Turret locations & destruction state**, since **turrets stop minion waves when they are alive**.
- **Lane coordinates**, helping structure minion movement into distinct lanes.

## 🌊 Step 6: Determining the Wave Position at Each Timestamp
Using the cleaned dataset, the final step was identifying **wave positions per lane**:

1. **Grouping minions into waves** based on proximity.
2. **Finding the wave closest to the enemy nexus**.
3. **Calculating the average position of all minions in the wave**.

## 📊 Data and Results
This repository contains processed data and visualizations derived from the analysis. The following resources are available:

### 📁 Data (`/data/`)
- **`game_replay.rofl`** → Raw League of Legends replay file.
- **`processed_video.webm`** → Converted video file used for minion detection.
- **`minion_detections.csv`** → CSV containing detected minion positions per second.
- **`wave_collisions_2025.csv`** → Coordinates of wave collision points for analyzed games.

### 📁 Visuals (`/visuals/`)
- **`heatmap_example.png`** → Heatmap showing minion wave collision zones.
- **`wave_movement_analysis.png`** → Visual representation of wave movements over time.

### 📁 Reports (`/reports/`)
- **`wave_collision_analysis.ipynb`** → Jupyter Notebook with insights and analysis using the processed data (without revealing the detection method).

## 🔍 Insights and Applications
This dataset and visualization can be useful for:
- Understanding how minion waves interact in different lanes.
- Evaluating how external factors (jungle pressure, player intervention) influence wave collisions.
- Optimizing macro strategy based on wave dynamics.
- Analyzing **wave positioning in teamfights and objective control**.
- Studying **post-wave push decisions** and their impact on lane management.

## 👀 Community Involvement
I invite the community to explore the results and help find new ways to leverage this data. Some possible areas of interest include:
- **Wave positioning during teamfights**
- **Impact of wave state on objective fights** (dragons, baron, turrets)
- **Best actions after pushing a wave** (roaming, invading, resetting, etc.)

## ❗ Limitations
- **No raw video data included**: To maintain processing confidentiality, only processed results are provided.
- **No implementation details**: The minion detection method and exact process are not shared to preserve proprietary methods.

## 📢 Contact & Contributions
This project is shared for analytical and discussion purposes. If you have insights or ideas to expand the analysis, feel free to open a discussion or reach out!

---
