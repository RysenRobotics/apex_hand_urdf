**Language / 语言：** **English** · [中文](README.zh.md)

**Version / 版本：** **0.1.0** (see [`VERSION`](VERSION))

> **Preliminary release:** This package is at an early stage and is **not** the final release. The URDF, meshes, and documentation may change in future versions.

## 1. About this document

This document describes the RysenRobotics Apex Hand URDF package. Both the URDF and this README are preliminary. Dynamics parameters in the URDF are **not fully calibrated** yet. If you find errors, email **support@dexcelbot.com** and we will address them as soon as possible.

## 2. Directory layout

At the repository root you will find **`apex_hand_left/`**, **`apex_hand_right/`** (left/right URDF and meshes), **`images/`** (figures for this README), **`VERSION`** (current package version), **`README.md`** (this file, English, default), and **`README.zh.md`** (Chinese). Each hand folder contains **URDF + `meshes/`**, matching the `./meshes/` relative paths referenced inside the URDF.

```text
apex_hand_urdf/                      # repo root (folder name may differ after clone)
├── apex_hand_left/
│   ├── apex_hand_left.urdf         # left-hand URDF
│   └── meshes/                     # STL meshes (URDF references ./meshes/...)
│       ├── Palm_link_left.STL
│       ├── f0_link0.STL
│       └── ...                     # phalanges, sensor shells, etc.
├── apex_hand_right/
│   ├── apex_hand_right.urdf        # right-hand URDF
│   └── meshes/
│       ├── Palm_link_right.STL
│       ├── f0_link0.STL
│       └── ...
├── images/                         # README figures (frames, etc.)
│   ├── left.png
│   ├── left_skeleton.png
│   ├── right.png
│   └── right_skeleton.png
├── VERSION                         # Current version (0.1.0)
├── README.md                       # English (default, this file)
└── README.zh.md                    # Chinese
```

If you only need the **right hand**, copy the entire **`apex_hand_right/`** folder (including `.urdf` and `meshes/`) and keep mesh relative paths consistent with the URDF.

## 3. Joints

#### 3.1 Degrees of freedom

The hand has **21** degrees of freedom in total: **16 actuated** and **5 passive**.

#### 3.2 Joint parameter table

| Name       | Coupled | Coupling relation              | Range (deg) | Notes |
| ---------- | ------- | ------------------------------ | ----------- | ----- |
| f0_joint0  | No      | /                              | 0～80       | Analogous to thumb CMC ab/add |
| f0_joint1  | No      | /                              | -10～60     | Analogous to thumb CMC pron/supination |
| f0_joint2  | No      | /                              | 0～80       | Analogous to thumb CMC flex/extension |
| f0_joint3  | No      | /                              | -20～80     | Analogous to thumb MCP flex/extension |
| f0_joint4  | Yes     | Coupled to **f0_joint3**, 1:1  | -20～80     | Analogous to thumb IP flex/extension |
| f1_joint0  | No      | /                              | -25～25     | Index MCP ab/add |
| f1_joint1  | No      | /                              | -20～90     | Index MCP flex/extension |
| f1_joint2  | No      | /                              | -5～100     | Index PIP flex/extension |
| f1_joint3  | Yes     | Coupled to **f1_joint2**, 1:1  | -5～100     | Index DIP flex/extension |
| f2_joint0  | No      | /                              | -25～25     | Middle MCP ab/add |
| f2_joint1  | No      | /                              | -20～90     | Middle MCP flex/extension |
| f2_joint2  | No      | /                              | -5～100     | Middle PIP flex/extension |
| f2_joint3  | Yes     | Coupled to **f2_joint2**, 1:1  | -5～100     | Middle DIP flex/extension |
| f3_joint0  | No      | /                              | -25～25     | Ring MCP ab/add |
| f3_joint1  | No      | /                              | -20～90     | Ring MCP flex/extension |
| f3_joint2  | No      | /                              | -5～100     | Ring PIP flex/extension |
| f3_joint3  | Yes     | Coupled to **f3_joint2**, 1:1  | -5～100     | Ring DIP flex/extension |
| f4_joint0  | No      | /                              | -25～25     | Little MCP ab/add |
| f4_joint1  | No      | /                              | -20～90     | Little MCP flex/extension |
| f4_joint2  | No      | /                              | -5～100     | Little PIP flex/extension |
| f4_joint3  | Yes     | Coupled to **f4_joint2**, 1:1  | -5～100     | Little DIP flex/extension |

## 4. Frames

Both hands use **right-handed** frames; the **flange** is the base frame. Each digit has frames at the fingertip and the pad, named **tip** and **pad**. For example, the thumb tip frame is **f0_tip**, and the thumb pad frame is **f0_pad**.

**Left hand x_i axis convention:** z_{i-1} → z_i

**Right hand x_i axis convention:** z_i → z_{i-1}

#### 4.1 Left-hand frames

![Left hand frames](images/left.png)

![Left hand skeleton frames](images/left_skeleton.png)

### 4.2 Right-hand frames

![Right hand frames](images/right.png)

![Right hand skeleton frames](images/right_skeleton.png)
