![![alt text](image-1.png)](image.png)# 🪼 Aura Jellyfish Simulator

A high-fidelity, real-time 3D simulation of bioluminescent deep-sea life. Built with **Next.js 15**, **Three.js (WebGL)**, and custom **GLSL Shaders**, this simulation blends mathematical physics with aesthetic graphics to recreate the hypnotic, fluid movement of a jellyfish in the abyssal ocean.

---

## 🌟 Key Visual Highlights

- **Bioluminescent Shaders**: Custom WebGL shaders simulating organic Fresnel translucency, light absorption, and dynamic subsurface scattering.
- **Procedural Anatomy**: Realistic rendering of radial canals, clover-shaped gonads, and flowing, ruffled oral arms.
- **Dynamic Post-Processing**: Selective `UnrealBloomPass` bloom shading to mimic the glow of abyssal organisms in pitch-black waters.

---

## 🚀 Key Features

### 1. Advanced Locomotion & Verlet Physics
- **Soft-Body Tentacles**: Simulated using a multi-node Verlet integration chain with distance constraints, reacting dynamically to movement, gravity, and water currents.
- **Interactive Repulsion**: Tentacles dynamically deflect away from the user's cursor via a quadratic distance repulsion field.
- **Bell Contraction**: The dome contracting animation applies physical forward thrust to the body, driving it forward with drag forces stabilizing its velocity.

### 2. Immersive Environmental Simulation
- **Marine Snow**: Custom particle system simulating organic particulate matter drifting in the water column with randomized 3D turbulence.
- **Volumetric God Rays**: Shifting shafts of sunlight refracting from the surface, procedurally rendered using custom cylinder-projected shaders.
- **Abyssal Fog**: Exponential depth fog to isolate the glowing organism and provide a true sense of scale and deep-water immersion.

### 3. Glassmorphic User Interface
- Real-time adjustment of parameters: color presets (Neon Cyan, Bioluminescent Pink, Abyssal Violet, etc.), glow intensity, thrust power, and jellyfish scale.
- **Performance Mode**: Instantly scales down particle counts, disables the bloom post-processing pass, and turns off god rays to maintain high frame rates on low-end hardware.

---

## 🛠️ Architecture & Tech Stack

The application is structured for high frame-rates and smooth user interaction:

* **Next.js (App Router) & TypeScript**: Modern react framework ensuring modular component structures.
* **Three.js**: Direct control over WebGL camera, scene, lighting, geometries, and rendering loop.
* **Custom Shaders (GLSL)**: Custom Vertex and Fragment shaders for the bell dome, membrane, and god rays.
* **Verlet Physics (`simulator/`)**: Pure TypeScript-based particle-spring simulation decoupled from rendering to ensure stability.

### Project Directory Structure

```text
├── app/
│   ├── globals.css          # Styling for the canvas and UI overlays
│   ├── layout.tsx           # Main application shell
│   └── page.tsx             # Application page managing control panel state
├── components/
│   └── JellyfishSimulator.tsx # React wrapper initializing WebGL and the loop
├── simulator/
│   ├── Environment.ts       # Lights, fog, background sphere, marine snow, god rays
│   ├── Jellyfish.ts         # Core jellyfish model, tentacle physics, and materials
│   └── MouseController.ts   # Raycasting & coordinate conversion for user interaction
└── public/
    └── jellyfish.jpg        # Shared texture asset for shaders
```

---

## 🚀 Getting Started

Follow these steps to run the simulation locally:

### 1. Clone & Install Dependencies
Navigate to the project root and install package dependencies:
```bash
npm install
```

### 2. Run the Development Server
Launch the development server:
```bash
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) in your web browser to interact with the simulator.

### 3. Build for Production
To build a highly-optimized production version:
```bash
npm run build
npm run start
```

---

## 🎮 Interaction Guide

| Interaction | Control | Description |
| :--- | :--- | :--- |
| **Left Click + Drag** | Mouse / Trackpad | Grabs and drags the jellyfish, creating realistic lag and inertia on the tentacles. |
| **Mouse Hover** | Movement | Moving the mouse near the tentacles creates a gentle repulsion force, pushing them away. |
| **Contract Bell** | Button | Manually triggers a muscular contraction to propel the jellyfish upwards. |
| **Reset Settings** | Button | Restores physics and rendering properties back to default values. |

---

## ⚡ Performance Optimization

To ensure a smooth experience across a wide range of devices:
- **Tone Mapping**: Uses `ACESFilmicToneMapping` to blend bright bioluminescent colors without overexposing the colors.
- **Render Optimization**: The post-processing pipeline is bypassed entirely in **Performance Mode**, rendering directly to the canvas to eliminate GPU overhead on integrated graphics.
- **Resource Lifecycle**: All geometries, textures, and custom shaders are manually disposed of on component unmount, preventing memory leaks during hot-reloads.
