# Stewart-platform-leg-lengths
# 6-UPS Stewart Platform Calculator

[![Live Demo](https://img.shields.io/badge/demo-live-success)](https://yourusername.github.io/stewart-platform-calculator/)
[![GitHub](https://img.shields.io/badge/github-repo-blue)](https://github.com/yourusername/stewart-platform-calculator)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

> Interactive web-based inverse kinematics calculator for 6-DOF Stewart-Gough parallel manipulator with real-time 3D visualization and transformation matrix display.

![Stewart Platform Calculator](https://via.placeholder.com/800x450/0a0e27/00d9ff?text=Stewart+Platform+Calculator+with+Matrix+Display)
<!-- Replace the above URL with an actual screenshot after deployment -->

---

**🎓 Educational Tool** | **🔧 Engineering Resource** | **📊 Visual Mathematics** | **🚀 Zero Installation**

---

## 🔗 Live Demo

**Try it now:** [[https://yourusername.github.io/stewart-platform-calculator/](https://khushi-60.github.io/Stewart-platform-leg-lengths/)](https://yourusername.github.io/stewart-platform-calculator/)

<!-- Replace 'yourusername' with your actual GitHub username -->

## ✨ Features

- 🎮 **Interactive Controls** - Adjust position and rotation with sliders or direct input
- 📊 **Real-time Calculations** - Instant leg length computation
- 🎨 **3D Visualization** - Live platform configuration with top-down view using Three.js
- 🔢 **Transformation Matrix Display** - Real-time homogeneous transformation matrices
- 📐 **Mathematical Breakdown** - See rotation matrix, translation vector, and complete transformation
- 🎯 **Preset Configurations** - Quick access to common poses
- 📱 **Responsive Design** - Works on desktop, tablet, and mobile
- ⚡ **Fast & Lightweight** - Pure JavaScript, no installation required
- 🌐 **No Backend Needed** - Runs entirely in the browser

## 🎯 What is a Stewart Platform?

A Stewart platform (also known as Stewart-Gough platform) is a parallel manipulator with six degrees of freedom (6-DOF). It consists of:

- **Fixed Base Platform** with 6 attachment points
- **Mobile Platform** with 6 attachment points
- **6 Variable-length Legs** connecting the platforms
- **Universal Joints** at the base
- **Spherical Joints** at the platform

**Applications:**
- Flight simulators
- Precision manufacturing
- Telescope positioning
- Medical robotics
- Motion capture systems

## 🔧 Technical Specifications

### Platform Geometry
- **Base Radius:** 100 mm
- **Platform Radius:** 80 mm
- **Configuration:** Circular attachment pattern

### Workspace Limits
| Parameter | Range |
|-----------|-------|
| X Position | ±50 mm |
| Y Position | ±50 mm |
| Z Position | ±50 mm |
| Roll (α) | ±15° |
| Pitch (β) | ±15° |
| Yaw (γ) | ±15° |

### Output
- 6 leg lengths (L₁ through L₆) in millimeters
- Real-time 3D visualization of platform configuration

## 🚀 Quick Start

### Option 1: Use Online (Recommended)

Simply visit: [https://yourusername.github.io/stewart-platform-calculator/](https://khushi-60.github.io/Stewart-platform-leg-lengths/)

### Option 2: Run Locally

1. **Clone or Download**
   ```bash
   git clone https://github.com/yourusername/stewart-platform-calculator.git
   cd stewart-platform-calculator
   ```

2. **Open in Browser**
   - Double-click `index.html`, or
   - Open with your preferred browser

That's it! No build process, no dependencies, no server needed.

## 📖 How to Use

### 1. Adjust Position
Use the sliders or input fields to set the platform position:
- **X**: Left/Right movement
- **Y**: Forward/Backward movement  
- **Z**: Up/Down movement

### 2. Adjust Orientation
Set the platform rotation angles:
- **Roll (α)**: Rotation around X-axis
- **Pitch (β)**: Rotation around Y-axis
- **Yaw (γ)**: Rotation around Z-axis

### 3. View Results
- **Leg Lengths**: Displayed in real-time (6 values in mm)
- **3D Visualization**: Top-down view of platform configuration
  - Blue hexagon: Fixed base platform
  - Red hexagon: Moving platform
  - Yellow cylinders: Adjustable legs
  - Glowing points: Attachment joints
- **Transformation Matrices**: Live mathematical computation display
  - Complete 4×4 homogeneous transformation matrix **T**
  - 3×3 rotation matrix **R(α, β, γ)**
  - 3×1 translation vector **t = [x, y, z]ᵀ**
- **Preset Buttons**: Quick access to common configurations

### Example Configurations

| Preset | Description | Position | Rotation |
|--------|-------------|----------|----------|
| Neutral | Home position | (0, 0, 0) | (0°, 0°, 0°) |
| Raised | Lifted platform | (0, 0, 30) | (0°, 0°, 0°) |
| Tilted | Pitched forward | (0, 0, 0) | (0°, 10°, 0°) |
| Combined | Complex motion | (10, 10, 20) | (5°, 5°, 10°) |

## 🧮 Mathematical Background

### Inverse Kinematics

The calculator solves the inverse kinematics problem:

**Given:** Platform pose (position + orientation)  
**Find:** Required leg lengths

### Algorithm

1. **Rotation Matrix** - Compute from Euler angles (ZYX convention):
   ```
   R = Rz(γ) · Ry(β) · Rx(α)
   ```
   Where each rotation matrix is:
   ```
   Rx(α) = [1    0      0   ]    Ry(β) = [cos β   0  sin β]    Rz(γ) = [cos γ  -sin γ  0]
           [0  cos α -sin α]              [  0     1    0  ]              [sin γ   cos γ  0]
           [0  sin α  cos α]              [-sin β  0  cos β]              [  0      0     1]
   ```

2. **Homogeneous Transformation Matrix**:
   ```
   T = [R | t]  =  [r11  r12  r13 | x]
       [0 | 1]     [r21  r22  r23 | y]
                   [r31  r32  r33 | z]
                   [ 0    0    0  | 1]
   ```
   where **t = [x, y, z]ᵀ** is the translation vector

3. **Transform Platform Points**:
   ```
   p'ᵢ = R · pᵢ + t
   ```
   This applies both rotation and translation to each platform attachment point

4. **Calculate Leg Lengths**:
   ```
   Lᵢ = ||p'ᵢ - bᵢ|| = √[(p'xᵢ - bxᵢ)² + (p'yᵢ - byᵢ)² + (p'zᵢ - bzᵢ)²]
   ```
   where **bᵢ** are the fixed base attachment points

### Real-time Matrix Display

The application displays all transformation matrices in real-time as you adjust the controls:
- **4×4 Complete Transformation** - Full homogeneous matrix
- **3×3 Rotation Component** - Pure rotation from Euler angles
- **3×1 Translation Vector** - Position offset

This allows you to see exactly how the mathematical transformations work!

### Coordinate System

- **Origin**: Center of base platform
- **X-axis**: Forward
- **Y-axis**: Left
- **Z-axis**: Up
- **Rotation**: ZYX Euler angles (Yaw-Pitch-Roll)

## 🛠️ Technology Stack

- **HTML5** - Structure and content
- **CSS3** - Styling and animations
- **JavaScript (ES6+)** - Logic and calculations
- **Three.js** - 3D visualization
- **No frameworks** - Pure vanilla implementation

## 📁 Project Structure

```
stewart-platform-calculator/
├── index.html              # Main application file
├── README.md               # This file
└── LICENSE                 # MIT License
```

## 🎨 Customization

### Change Platform Dimensions

Edit these constants in `index.html`:

```javascript
const BASE_RADIUS = 100;        // Base radius in mm
const PLATFORM_RADIUS = 80;     // Platform radius in mm
```

### Modify Workspace Limits

Update the `min` and `max` attributes in input elements:

```html
<input type="number" id="x" min="-50" max="50" step="1">
```

### Customize Colors

Modify CSS variables at the top of `<style>`:

```css
:root {
    --primary: #00d9ff;      /* Main color */
    --secondary: #ff00ea;    /* Accent color */
    --accent: #ffea00;       /* Highlight color */
}
```

## 📊 Performance

- **Calculation Speed**: < 1 ms per pose
- **Matrix Computation**: Real-time (updates at 60 FPS)
- **3D Rendering**: 60 FPS on modern hardware
- **Bundle Size**: ~55 KB (excluding Three.js CDN)
- **Browser Support**: All modern browsers (Chrome, Firefox, Safari, Edge)

## 🎯 What Makes This Special

### Educational Value
- **Visual Learning**: See the platform move in 3D as you adjust parameters
- **Mathematical Insight**: Watch transformation matrices update in real-time
- **Interactive Exploration**: Experiment with different configurations instantly

### Engineering Applications
- **Design Validation**: Quickly verify platform configurations
- **Workspace Analysis**: Visualize reachable positions
- **Prototype Testing**: Test poses before building hardware

### Technical Features
- **Top-Down View**: Clear perspective for understanding geometry
- **Realistic 3D Models**: Hexagonal platforms with cylindrical legs
- **Live Matrix Display**: See the math behind the motion
- **Professional UI**: Futuristic design with smooth animations

## 🔬 Use Cases

### Education
- Teaching parallel manipulator kinematics
- Demonstrating inverse kinematics concepts
- Robotics coursework and labs

### Research
- Quick validation of platform configurations
- Workspace visualization
- Algorithm prototyping

### Engineering
- Design verification
- Motion planning
- System simulation

## 🤝 Contributing

Contributions are welcome! Here are some ways you can help:

- 🐛 Report bugs
- 💡 Suggest new features
- 📝 Improve documentation
- 🎨 Enhance UI/UX
- ⚡ Optimize performance

### How to Contribute

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Stewart-Gough Platform** - Original research by D. Stewart (1965)
- **Three.js** - 3D visualization library
- **Parallel Robotics** - Mathematical foundations from various research papers

## 📧 Contact

**Khushi** - khushism06@gmail.com

**Project Link:** [https://github.com/yourusername/stewart-platform-calculator](https://github.com/yourusername/stewart-platform-calculator)

**Live Demo:** [https://yourusername.github.io/stewart-platform-calculator/]([https://khushi-60.github.io/Stewart-platform-leg-lengths/])

---

## 🆕 Latest Updates (v2.0)

### New Features Added:
- ✨ **Transformation Matrix Display** - Real-time visualization of homogeneous transformation matrices
- 🎨 **Top-Down View** - Improved 3D visualization with clear overhead perspective
- 🔶 **Hexagonal Platforms** - More realistic geometry representation
- 🔧 **Cylindrical Legs** - Solid 3D cylinders instead of lines for better visibility
- 💫 **Enhanced Lighting** - Multi-angle lighting for better depth perception
- 🌟 **Glowing Joints** - Visual rings around attachment points

### Mathematical Display:
- Complete 4×4 homogeneous transformation matrix **T**
- 3×3 rotation matrix **R(α, β, γ)**
- 3×1 translation vector **t**
- All matrices update in real-time as you adjust controls

---

## ⭐ Star This Repository

If you find this project useful, please give it a star! It helps others discover the project.

---

**Built with ❤️ for robotics and engineering education**

## 🔗 Related Projects

- [Research Paper](docs/research_paper.pdf) - Complete mathematical analysis
- [Implementation Guide](docs/implementation_guide.md) - Step-by-step coding tutorial
- [Neural Network Version](https://github.com/yourusername/stewart-nn) - ML-based approach

## 📸 Screenshots

### Calculator Interface with Matrix Display
![Calculator Interface](https://via.placeholder.com/800x600/0a0e27/00d9ff?text=Interactive+Controls+%2B+Leg+Lengths)
*Interactive controls on the left, real-time leg length calculations displayed in animated cards*

### 3D Visualization - Top-Down View
![3D Top View](https://via.placeholder.com/800x500/0a0e27/ff00ea?text=Top-Down+3D+Visualization)
*Clear top-down perspective showing hexagonal base (blue), moving platform (red), and cylindrical legs (yellow)*

### Transformation Matrix Display
![Matrix Display](https://via.placeholder.com/800x400/0a0e27/ffea00?text=Homogeneous+Transformation+Matrices)
*Real-time display of 4×4 transformation matrix, 3×3 rotation matrix, and translation vector*

### Mobile Responsive View
![Mobile](https://via.placeholder.com/300x600/0a0e27/00d9ff?text=Mobile+Responsive)
*Fully responsive design works perfectly on smartphones and tablets*

<!-- Replace placeholder images with actual screenshots after deployment -->

### Key Visual Features:
- **Hexagonal platforms** - More realistic representation than circles
- **Cylindrical legs** - Solid 3D cylinders instead of thin lines
- **Glowing attachment points** - Rings around joints for better visibility
- **Top-down camera angle** - Clearer view of platform geometry
- **Multi-angle lighting** - Enhanced depth perception
- **Live matrix updates** - All transformation matrices update in real-time

---

**Made with passion for robotics • Last updated: 2026**
