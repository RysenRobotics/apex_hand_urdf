**Language / 语言：** **English** · [中文](README.zh.md)

**Version / 版本：** **0.2.0** (see [`VERSION`](VERSION))

> **Preliminary release:** This package is at an early stage and is **not** the final release. The URDF, meshes, and documentation may change in future versions.

## 1. About this document

This document describes the RysenRobotics Apex Hand URDF package. Both the URDF and this README are preliminary. Dynamics parameters in the URDF are **not fully calibrated** yet. If you find errors, email **support@dexcelbot.com** and we will address them as soon as possible.

## 2. Directory layout

At the repository root you will find **`apex_hand_left/`**, **`apex_hand_right/`** (left/right URDF and meshes), **`images/`** (figures for this README), **`VERSION`** (current package version), **`README.md`** (this file, English, default), and **`README.zh.md`** (Chinese). Each hand folder contains **URDF + `meshes/`**, matching the `./meshes/` relative paths referenced inside the URDF. Link, joint, and mesh names use a **`{left|right}_{digit}_`** prefix (e.g. `left_thumb_j0`, `right_index_link2.STL`).

```text
apex_hand_urdf/                      # repo root (folder name may differ after clone)
├── apex_hand_left/
│   ├── apex_hand_left.urdf         # left-hand URDF
│   └── meshes/                     # STL meshes (URDF references ./meshes/...)
│       ├── left_palm_link.STL
│       ├── left_thumb_link0.STL
│       ├── left_thumb_tactile0.STL
│       └── ...                     # links, tip/pad, tactile shells, etc.
├── apex_hand_right/
│   ├── apex_hand_right.urdf        # right-hand URDF
│   └── meshes/
│       ├── right_palm_link.STL
│       ├── right_thumb_link0.STL
│       ├── right_thumb_tactile0.STL
│       └── ...
├── images/                         # README figures (frames, etc.)
│   ├── left.png
│   ├── left_skeleton.png
│   ├── right.png
│   └── right_skeleton.png
├── VERSION                         # Current version (0.2.0)
├── README.md                       # English (default, this file)
└── README.zh.md                    # Chinese
```

If you only need the **right hand**, copy the entire **`apex_hand_right/`** folder (including `.urdf` and `meshes/`) and keep mesh relative paths consistent with the URDF.

## 3. Joints

#### 3.1 Degrees of freedom

The hand has **21** degrees of freedom in total: **16 actuated** and **5 passive**.

#### 3.2 Joint parameter table

Joint names below use the logical form **`{digit}_j{n}`** (e.g. `thumb_j0`). In the URDF they are prefixed with **`left_`** or **`right_`** (e.g. `left_thumb_j0`, `right_thumb_j0`).

| Name       | Coupled | Coupling relation               | Range (deg) | Notes |
| ---------- | ------- | ------------------------------- | ----------- | ----- |
| thumb_j0   | No      | /                               | 0～90       | Analogous to thumb CMC ab/add |
| thumb_j1   | No      | /                               | -10～60     | Analogous to thumb CMC pron/supination |
| thumb_j2   | No      | /                               | 0～80       | Analogous to thumb CMC flex/extension |
| thumb_j3   | No      | /                               | -20～80     | Analogous to thumb MCP flex/extension |
| thumb_j4   | Yes     | Coupled to **thumb_j3**, 1:1    | -20～80     | Analogous to thumb IP flex/extension |
| index_j0   | No      | /                               | -25～25     | Index MCP ab/add |
| index_j1   | No      | /                               | -20～90     | Index MCP flex/extension |
| index_j2   | No      | /                               | -5～100     | Index PIP flex/extension |
| index_j3   | Yes     | Coupled to **index_j2**, 1:1    | -5～100     | Index DIP flex/extension |
| middle_j0  | No      | /                               | -25～25     | Middle MCP ab/add |
| middle_j1  | No      | /                               | -20～90     | Middle MCP flex/extension |
| middle_j2  | No      | /                               | -5～100     | Middle PIP flex/extension |
| middle_j3  | Yes     | Coupled to **middle_j2**, 1:1   | -5～100     | Middle DIP flex/extension |
| ring_j0    | No      | /                               | -25～25     | Ring MCP ab/add |
| ring_j1    | No      | /                               | -20～90     | Ring MCP flex/extension |
| ring_j2    | No      | /                               | -5～100     | Ring PIP flex/extension |
| ring_j3    | Yes     | Coupled to **ring_j2**, 1:1     | -5～100     | Ring DIP flex/extension |
| pinky_j0   | No      | /                               | -25～25     | Pinky MCP ab/add |
| pinky_j1   | No      | /                               | -20～90     | Pinky MCP flex/extension |
| pinky_j2   | No      | /                               | -5～100     | Pinky PIP flex/extension |
| pinky_j3   | Yes     | Coupled to **pinky_j2**, 1:1    | -5～100     | Pinky DIP flex/extension |

## 4. Frames

Both hands use **right-handed** frames; the **flange** is the base frame. Each digit has frames at the fingertip and the pad, named **tip** and **pad**. For example, the thumb tip frame is **`thumb_tip`** and the thumb pad frame is **`thumb_pad`** (URDF: `left_thumb_tip` / `right_thumb_tip`, `left_thumb_pad` / `right_thumb_pad`).

**Left hand x_i axis convention:** z_{i-1} → z_i

**Right hand x_i axis convention:** z_i → z_{i-1}

#### 4.1 Left-hand frames

![Left hand frames](images/left.png)

![Left hand skeleton frames](images/left_skeleton.png)

### 4.2 Right-hand frames

![Right hand frames](images/right.png)

![Right hand skeleton frames](images/right_skeleton.png)
