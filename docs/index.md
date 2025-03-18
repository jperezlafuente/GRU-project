# League of Legends Minion Wave Collision Analysis

## 📌 Project Overview
This project analyzes minion wave behavior in League of Legends by detecting minions in video footage and identifying the collision points of red and blue minion waves in each lane. The goal is to provide insights into wave control and lane dynamics.

## 🏆 Objective
The primary focus of this project is to gather information on **wave positions in professional League of Legends matches** since it is not provided by Riot nor its official data partner GRID. To achieve this, the following process is followed:

1. **Labeling images of minions on the minimap to develop a CV model**
2. **Developing a Computer Vision model (YOLOv8) for detection**
3. **Extracting videos of professional matches**
4. **Processing videos to detect minions in real game time**
5. **Enhancing the dataset with additional game data**
6. **Calculating the final wave positions per lane**

## 🔬 Step 1: Labeling Images for Training
To train a computer vision model, the first thing that should be done is labeling images. In this process, you have to gather as much images as possible from your topic and manually tag them whenever you see what you need to find. In my case, I need to label images from LOL games looking for minions dots in minimap. Funny part here is that I used my own SoloQ matches for this process since that was enough and easier to gather, but it is important to do it in the same quality that you should expect to gather real images later.

In order to tag them, I used **LabelImg**. It's a simple environment designed for this purpose, free and easy to use. You just need to:

- Upload your own images to the platform (I chopped my games videos to images and selected random moments from them)
- Annotating manually each minion’s position as **bounding boxes**.
- Ensuring the labels correctly distinguish between the level of granularity you need. In my case, I just went for distinguishing red and blue minions.

📷 *Example of labeled image:*
![Labeled Minimap Example](visuals/labeled_minimap.png)

## 🤖 Step 2: Training the Detection Model
Once I had the images labeled, I just downloaded them from LabelImg in yolo format in order to train a Computer Vision model on them. Yolo format is just a repository where you have two folders: images and labels (where you have plain text docs for every image with the position of the bounding boxes and its class).

A **YOLOv8-based** computer vision model was trained using the labeled images to accurately detect minions. Training setup:

- **Dataset:** 300 labeled frames
- **Training epochs:** 100

I was not fully confident on uploading this numbers since I am aware that this is not an ideal environment to CV developing. Wherever you read, 300 frames are surely a low number of images to train a model. 100 epochs is cool, even you could go for more. However, since we had a lot of minions in every frame and we are dealing with really similar images and things to look for (small blue-red dots, almost always in the same part of the images), I gave it a try and results where promising. And yes, labeling time was also an issue to stop at 300 manually tagged images.

- **Accuracy Results:**
  - **Precision-Recall Score:** 97.1%
  - **Mean Average Precision (mAP):** 95.3%

📊 *Precision-Recall Curve:*
![PR Curve](visuals/PR_curve.png)

*Additional tests included evaluating detection performance on unseen games.*

## 🎥 Step 3: Extracting Match Videos
As a data analyst, once I had developed a reliable CV model I thought that toughest part had already gone. What an idiot I was.

Next step of the process involved gathering official competitive LOL games in order to look for minions in its frames. And since I am a part of ZETA Gaming, I had easy access to the videos via Riot's GRID platform. But League of Legends matches are stored as **ROFL replay files**. However, **Riot does not provide an official method to watch them or extract them as videos once its patch is not live patch anymore** (WTF).

Since live patches are constantly updated, pro games were 99% outdated and unavailable to be reproduced. I did even ask GRID if they had an official statement on how to do this, but they said NO. Thankfully, LOL community is one of the strongest I've ever seen and they gave me the help I needed (thanks Pablo, Julia and Fire). So i used:
- **ReplayBook** to play the replays.
- **Replays.xyz** to get older LOL clients.
- The full matches were recorded (x8 speed, max quality) and stored in the highlights folder for processing.

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
