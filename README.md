# 🧠 GRU PROJECT: League of Legends Minion Wave Collision Analysis

📄 **Detailed Article** → [Read the the full documentation here](docs/full_analysis.md)

This project leverages computer vision to detect minions in professional League of Legends matches and identify **wave collision points** in each lane. Ideal for strategists, analysts, and curious minds.

---

## 🏆 Goal

Understand **lane dynamics** in pro play by detecting and analyzing **minion wave behavior**, a type of data not provided by Riot nor GRID.  
This pipeline takes raw video and turns it into actionable insights.  

---

## 🔍 How It Works

### 1️⃣ Label Minions  
### 2️⃣ Train YOLOv8  
### 3️⃣ Get Pro Matches  
### 4️⃣ Detect Minions in Video  
### 5️⃣ Enrich the Dataset  
### 6️⃣ Find Clash Points  

---

## 🧾 Available Resources

- `/data/minion_detections.csv` → Detected minion positions per second.  
- `/data/waves_clash.csv` → Wave clash coordinates.
- Training examples, prediction outputs, PR curves, and detection videos.

---

## 📌 Applications

- Analyze wave behavior in pro play  
- Study wave state during teamfights  
- Optimize macro strategy  
- Explore jungle pressure and lane control

---

## 💬 Contact & Contribute

If you’ve got ideas, improvements, or questions, feel free to:  
- 📬 Email: [jperezlafuente@hotmail.com](mailto:jperezlafuente@hotmail.com)  
- 🐦 Twitter: [@jperezlafuente](https://twitter.com/jperezlafuente)
