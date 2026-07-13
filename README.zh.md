**语言 / Language：** **中文** · [English](README.md)

**版本 / Version：** **0.2.0**（见 [`VERSION`](VERSION)）

> **初步版本说明：** 当前为早期版本，**并非**最终发布版本。URDF、网格与文档在后续版本中可能调整。

## 1.文档说明

此文档描述apexhand灵巧手urdf相关信息。此文档和urdf皆为初步拟定，urdf中动力学参数还未标定完成。如发现有任何错误，可以反馈邮件至：support@dexcelbot.com，我们第一时间处理。

## 2.文件结构

仓库根目录下为 **`apex_hand_left/`**、**`apex_hand_right/`**（左右手 URDF 与网格）、**`images/`**（文档配图）、**`VERSION`**（当前版本号）、**`README.md`**（英文，默认）与 **`README.zh.md`**（本中文说明）。左右手各自为 **URDF + `meshes/`**，与 URDF 中 `./meshes/` 相对路径一致。连杆、关节与网格命名采用 **`{left|right}_{手指}_`** 前缀（如 `left_thumb_j0`、`right_index_link2.STL`）。

```text
apex_hand_urdf/                      # 仓库根目录（克隆后的项目文件夹名以实际为准）
├── apex_hand_left/
│   ├── apex_hand_left.urdf         # 左手 URDF
│   └── meshes/                     # STL 网格（URDF 引用 ./meshes/...）
│       ├── left_palm_link.STL
│       ├── left_thumb_link0.STL
│       ├── left_thumb_tactile0.STL
│       └── ...                     # 连杆、指尖/指腹、触觉壳体等
├── apex_hand_right/
│   ├── apex_hand_right.urdf        # 右手 URDF
│   └── meshes/
│       ├── right_palm_link.STL
│       ├── right_thumb_link0.STL
│       ├── right_thumb_tactile0.STL
│       └── ...
├── images/                         # README 用图（坐标系示意等）
│   ├── left.png
│   ├── left_skeleton.png
│   ├── right.png
│   └── right_skeleton.png
├── VERSION                         # 当前版本号（0.2.0）
├── README.md                       # 英文说明（默认）
└── README.zh.md                    # 中文说明（本文件）
```

若仅需右手单机资源，可将 **`apex_hand_right/`** 整个文件夹（含 `.urdf` 与 `meshes/`）单独拷贝使用，路径需与 URDF 内 mesh 相对路径保持一致。

## 3.关节说明

#### 3.1由度说明

整手共21个自由度，其中16个主动自由度，5个被动自由度。

#### 3.2关节参数表

下表关节名采用逻辑形式 **`{手指}_j{n}`**（如 `thumb_j0`）。在 URDF 中会加上 **`left_`** 或 **`right_`** 前缀（如 `left_thumb_j0`、`right_thumb_j0`）。

| 名称       | 是否耦合 | 耦合关系                     | 范围（角度） | 说明                                       |
| ------------ | ---------- | ------------------------------ | -------------- | -------------------------------------------- |
| thumb\_j0  | 否       | /                            | 0～90        | 近似于人的拇指腕掌关节（CMC）的侧摆        |
| thumb\_j1  | 否       | /                            | -10～60      | 近似于人的拇指腕掌关节（CMC）的内/外旋     |
| thumb\_j2  | 否       | /                            | 0～80        | 近似于人的拇指腕掌关节（CMC）的屈/伸       |
| thumb\_j3  | 否       | /                            | -20～80      | 近似于人的拇指掌指关节（MCP）的屈伸        |
| thumb\_j4  | 是       | 与thumb\_j3耦合，关系1：1    | -20～80      | 近似于人的拇指指间关节（IP）的屈/伸        |
| index\_j0  | 否       | /                            | -25～25      | 近似于人的食指掌指关节（MCP）的侧摆        |
| index\_j1  | 否       | /                            | -20～90      | 近似于人的食指掌指关节（MCP）的屈/伸       |
| index\_j2  | 否       | /                            | -5～100      | 近似于人的食指近端指间关节（PIP）的屈/伸   |
| index\_j3  | 是       | 与index\_j2耦合，关系1：1    | -5～100      | 近似于人的食指远端指间关节（DIP）的屈/伸   |
| middle\_j0 | 否       | /                            | -25～25      | 近似于人的中指掌指关节（MCP）的侧摆        |
| middle\_j1 | 否       | /                            | -20～90      | 近似于人的中指掌指关节（MCP）的屈/伸       |
| middle\_j2 | 否       | /                            | -5～100      | 近似于人的中指近端指间关节（PIP）的屈/伸   |
| middle\_j3 | 是       | 与middle\_j2耦合，关系1：1   | -5～100      | 近似于人的中指远端指间关节（DIP）的屈/伸   |
| ring\_j0   | 否       | /                            | -25～25      | 近似于人的无名指掌指关节（MCP）的侧摆      |
| ring\_j1   | 否       | /                            | -20～90      | 近似于人的无名指掌指关节（MCP）的屈/伸     |
| ring\_j2   | 否       | /                            | -5～100      | 近似于人的无名指近端指间关节（PIP）的屈/伸 |
| ring\_j3   | 是       | 与ring\_j2耦合，关系1：1     | -5～100      | 近似于人的无名指远端指间关节（DIP）的屈/伸 |
| pinky\_j0  | 否       | /                            | -25～25      | 近似于人的小指掌指关节（MCP）的侧摆        |
| pinky\_j1  | 否       | /                            | -20～90      | 近似于人的小指掌指关节（MCP）的屈/伸       |
| pinky\_j2  | 否       | /                            | -5～100      | 近似于人的小指近端指间关节（PIP）的屈/伸   |
| pinky\_j3  | 是       | 与pinky\_j2耦合，关系1：1    | -5～100      | 近似于人的小指远端指间关节（DIP）的屈/伸   |

## 4.坐标系说明

左右手的坐标系均为右手坐标系，法兰处为基坐标系。每根手指在指尖和指腹分别有一个坐标系，命名 tip 和 pad。例如大拇指指尖坐标系为：**`thumb_tip`**，指腹坐标系为：**`thumb_pad`**（URDF 中为 `left_thumb_tip` / `right_thumb_tip`、`left_thumb_pad` / `right_thumb_pad`）。

左手的xi轴方向：zi-1->zi

右手的xi轴方向：zi->zi-1

#### 4.1左手坐标系图

![左手坐标系](images/left.png)

![左手骨架坐标系](images/left_skeleton.png)

### 4.2右手坐标系图

![右手坐标系](images/right.png)

![右手骨架坐标系](images/right_skeleton.png)
