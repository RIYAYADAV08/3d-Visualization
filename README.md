# 🔍 3D Forensic Scene Visualization

An interactive **3D forensic scene reconstruction workspace** built with **React, TypeScript and Three.js (React Three Fiber)**. Investigators can explore a reconstructed scene, inspect evidence markers, view the floor plan, replay the investigation timeline and export reports, all in the browser.

> Built as part of a hackathon project focused on 3D visualization and forensic scene reconstruction (visualization module).

---

## 📌 Overview

Crime scene investigation depends on understanding space and sequence: where objects were, what evidence was found and when events happened. This project turns scene data (JSON) into an interactive 3D environment, with a timeline that is synchronized to the objects in the scene and clear visual cues for **uncertain or low-confidence** reconstructions.

---

## ✨ Features

**3D Scene**
- Interactive 3D viewer with orbit, zoom and damped camera controls
- Preset viewpoints: **Perspective, Top and Front**
- Object rendering for furniture, structures, evidence and unknown items
- Optional **GLTF/GLB model loading** per object (`modelUrl`), with a wireframe fallback while loading
- Lighting and room environment

**Evidence & Inspection**
- Evidence markers placed in the scene
- **Evidence register** with confidence percentage for each item
- Object inspector with details, ID and confidence
- **Uncertainty overlay** to highlight low-confidence objects (toggleable)

**Editing & Measuring**
- **Transform gizmos** (translate, rotate, scale) plus numeric X/Y/Z transform inputs
- **3D distance measurement** between two selected points

**Timeline**
- Investigation timeline synced with scene objects
- **Play/Pause, scrubber and playback speed** (0.5×, 1×, 2×, 4×)

**Floor Plan**
- Top-down room map; click a marker to focus the object in 3D

**Export**
- **Snapshot** of the 3D view
- **JSON** export of the scene
- **PDF report** (printable) with objects, positions, confidence and timeline

**Data & Reliability**
- Loads scene JSON from an API (`VITE_SCENE_API_URL`) or falls back to built-in demo data
- **Schema validation** (`isSceneData`) that rejects invalid dimensions, duplicate object IDs and evidence pointing to missing objects
- Unit tests with Vitest

---

## 🛠️ Tech Stack

| Area | Technology |
|------|------------|
| UI | React 18, TypeScript |
| 3D | Three.js, React Three Fiber, Drei |
| Build tool | Vite |
| Icons | Lucide React |
| Testing | Vitest |
| Styling | CSS |

---

## 📂 Project Structure

```text
3d-Visualization/
├── src/
│   ├── camera/            # CameraController, Viewpoints
│   ├── floor_plan/        # FloorPlanRenderer
│   ├── interactions/      # EvidenceInteraction, ObjectSelection, SceneNavigation
│   ├── objects/           # ObjectRenderer, EvidenceMarker, UncertaintyOverlay
│   ├── scene/             # Environment, Lighting, SceneLoader, SceneRenderer
│   ├── services/          # sceneApi.ts (load + schema validation)
│   ├── timeline/          # TimelineSceneSync
│   ├── types/             # scene.ts (SceneData types)
│   ├── utils/             # mockScene.ts (demo data)
│   ├── App.tsx
│   ├── main.tsx
│   └── styles.css
├── tests/
│   └── sceneApi.test.ts
├── .env.example
├── package.json
├── tsconfig.json
└── vite.config.ts
```

---

## 🧾 Scene Data Format

The viewer expects a JSON scene matching `src/types/scene.ts`:

```json
{
  "id": "scene-001",
  "title": "Demo Scene",
  "units": "m",
  "room": { "width": 8, "depth": 6, "height": 3 },
  "objects": [
    {
      "id": "obj-1",
      "name": "Table",
      "kind": "furniture",
      "position": [0, 0.5, 0],
      "confidence": 0.9
    }
  ],
  "evidence": [
    {
      "id": "ev-1",
      "label": "Fingerprint",
      "objectId": "obj-1",
      "description": "Partial print on table edge",
      "confidence": 0.8,
      "timestamp": "10:42"
    }
  ],
  "timeline": [
    {
      "id": "t-1",
      "time": "10:40",
      "title": "Entry",
      "description": "Subject enters the room",
      "objectIds": ["obj-1"]
    }
  ]
}
```

`kind` can be `furniture`, `structure`, `evidence` or `unknown`. Optional object fields: `rotation`, `scale`, `color`, `confidence` (0 to 1), `description`, `modelUrl`.

---

## ⚙️ Getting Started

### Prerequisites

- Node.js 18 or higher
- npm

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/RIYAYADAV08/3d-Visualization.git
cd 3d-Visualization

# 2. Install dependencies
npm install

# 3. (Optional) Configure a scene API
cp .env.example .env
# then set VITE_SCENE_API_URL=https://your-api/scene.json

# 4. Start the development server
npm run dev
```

Open **http://localhost:5173**. Without an API URL, the app loads the built-in demo scene.

### Scripts

```bash
npm run dev       # Start dev server
npm run build     # Type-check and create production build
npm run preview   # Preview the production build
npm test          # Run unit tests (Vitest)
```

---

## 🎮 How to Use

1. **Drag** to orbit, **scroll** to zoom, **click** an object to select it.
2. Use the viewpoint buttons to switch between Perspective, Top and Front views.
3. Toggle **Uncertainty** to highlight low-confidence objects.
4. Use **Measure** and click two points to get the distance.
5. Use the **Gizmo** (translate / rotate / scale) or the numeric inputs to adjust an object.
6. Press **Play** on the timeline, or drag the scrubber, to see events and linked objects.
7. Switch to the **Floor plan** tab for a top-down view.
8. Export a **Snapshot**, **JSON** or **PDF report**.

---

## ⚠️ Disclaimer

The demo scene and its confidence values are **illustrative sample data**, not verified forensic conclusions. This project is for educational, research and hackathon purposes.

---

## 🚀 Future Improvements

- Smooth animated camera transitions between viewpoints
- Import scenes from photogrammetry / LiDAR scans
- Multi-scene support and scene comparison
- Annotations and investigator notes
- Authentication and role-based access
- Automated UI tests

---

## 👩‍💻 Author

**Riya Yadav**

🔗 [LinkedIn](https://www.linkedin.com/in/riyayadav0803) | 💻 [GitHub](https://github.com/RIYAYADAV08)

---

## ⭐ Support

If you found this project helpful, please consider giving it a **star**!
