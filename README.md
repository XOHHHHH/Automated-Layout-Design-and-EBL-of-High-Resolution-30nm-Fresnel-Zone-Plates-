# Automated-Layout-Design-and-EBL-of-High-Resolution-30nm-Fresnel-Zone-Plates-
从自动化CAD脚本（626根参数化支撑筋）到超净间电子束光刻（EBL）实操：30nm高分辨率菲涅尔波带片全流程工程实录。内含蒙特卡洛仿真与3D邻近效应修正。From automated CAD scripting (626 spokes) to cleanroom EBL fabrication: a complete engineering workflow for 30nm high-resolution Fresnel Zone Plates, featuring Monte Carlo simulation and 3D PEC.
# Fabrication of 30nm Fresnel Zone Plate

本项目记录了半径 50 μm、最外环分辨率 30nm 的菲涅尔波带片（FZP）的完整流片数据，包含版图生成、电子散射仿真、邻近效应修正（PEC）及电子束光刻（EBL）脚本。

## 1. Specifications
- **Device:** Fresnel Zone Plate (Radius: 50 μm)
- **Resolution:** ~30 nm (Outer-most zone)
- **Substrate:** 100 nm Si3N4 membrane
- **Resist:** 500 nm HSQ
- **Equipment:** JEOL JBX-6300FS (100 kV)

## 2. Workflow

### 2.1 Layout Design (AutoCAD)
为防止高深宽比的 HSQ 胶在显影时倒塌，采用参数化脚本（`.scr`）生成了 626 根渐变加强筋：
- 10-20 μm: 50 spokes, 0.5 μm width
- 20-30 μm: 94 spokes, 0.4 μm width
- 30-40 μm: 168 spokes, 0.3 μm width
- 40-50 μm: 314 spokes, 0.2 μm width
最终整合并导出为 `.dxf` 格式。

### 2.2 Simulation (GenISys TRACER)
基于 100 kV 电子束在 500nm HSQ / 100nm Si3N4 体系下的蒙特卡洛仿真，提取点扩散函数，生成 `.lpsf` 文件。

### 2.3 Proximity Effect Correction (GenISys BEAMER)
处理 `.dxf` 版图：
1. **Heal:** 融合圆环与加强筋的重叠区域，防止重复曝光。
2. **3D PEC:** 导入 `.lpsf` 数据，对外圈高密度区域进行剂量修正。
3. **Export:** 导出为 JEOL 识别的 `.v30` 格式 (EOS6 Mode, 500 pA)。

### 2.4 Job Deck Configuration (JDF/SDF)
配置 `.jdf` 脚本，设置 500 至 3200 μC/cm² 的剂量阵列（Dose array），用于测试 HSQ 的最佳曝光剂量。

## 3. Directory Structure
- `01_CAD_Design/`: `.scr` 生成脚本及 `.dxf` 最终版图
- `02_Simulation_Tracer/`: 仿真参数及 `.lpsf` 文件
- `03_PEC_Beamer/`: PEC 工程文件及导出的 `.v30` 数据
- `04_Exposure_Scripts/`: JEOL 曝光机控制脚本 `.jdf` / `.sdf`
