# Automated-Layout-Design-and-EBL-of-High-Resolution-30nm-Fresnel-Zone-Plates-
从自动化CAD脚本（626根参数化支撑筋）到超净间电子束光刻（EBL）实操：30nm高分辨率菲涅尔波带片全流程工程实录。内含蒙特卡洛仿真与3D邻近效应修正。From automated CAD scripting (626 spokes) to cleanroom EBL fabrication: a complete engineering workflow for 30nm high-resolution Fresnel Zone Plates, featuring Monte Carlo simulation and 3D PEC.
# Fabrication of 30nm Fresnel Zone Plate

本项目记录了在**复旦大学陈宜方教授实验室**完成的高分辨率菲涅尔波带片（FZP）全流程制备。通过 626 根参数化支撑筋，成功解决了 500nm 厚 HSQ 胶在 16.6:1 高深宽比下的倒塌难题，并完成了 SEM 表征。

## 1. Specifications
- **Device:** Fresnel Zone Plate (Radius: 50 μm)
- **Resolution:** ~30 nm (Outer-most zone)
- **Substrate:** 100 nm Si3N4 membrane
- **Resist:** 500 nm HSQ
- **Equipment:** JEOL JBX-6300FS (100 kV)

## 2. Workflow & Engineering Logic

### 2.1 Layout Design (AutoCAD)
采用参数化脚本（`.scr`）生成 626 根径向梯度支撑筋（Parametric Spokes），在 10-50μm 的四个环形区域内提供力学支撑，防止超细线条在显影时因毛细张力倒塌。

### 2.2 Simulation & PEC (Tracer/Beamer)
基于蒙特卡洛仿真提取点扩散函数（PSF），并在 Beamer 中完成 3D 邻近效应修正（PEC），针对外圈高密度区域（30nm 线宽）进行剂量梯度优化。

### 2.3 Fabrication Process (Cleanroom)
- **Exposure:** 100kV, EOS6 (500 pA)
- **Development (HSQ 热显影):** - Developer: TMAH : H2O = 1 : 3
  - Temperature: 65 °C
  - Time: 3 min
- **Fixing (定影):**
  - Fixer: DI Water
  - Time: 30 s

## 3. Results (SEM Characterization)

通过 SEM 扫描电镜观察，30nm 最外圈线条清晰、完整，未见明显倒塌或粘连。支撑筋与波带片圆环交接处 Heal 处理良好。

<p align="center">
  <img src="images/sem_overview.png" width="400" title="FZP Overview">
  <img src="images/sem_outer_zone.png" width="400" title="30nm Outer Zones">
</p>

## 4. Directory Structure
- `01_CAD_Design/`: `.scr` 生成脚本及 `.dxf` 最终版图
- `02_Simulation_Tracer/`: 仿真参数及 `.lpsf` 文件
- `03_PEC_Beamer/`: PEC 工程文件及导出的 `.v30` 数据
- `04_Exposure_Scripts/`: JEOL 曝光机控制脚本 `.jdf` / `.sdf`
- `05_Characterization/`: SEM 原始图片及分析结果

---
*Special thanks to Senior Student Xunjia Zhao and Prof. Yifang Chen for their expert guidance.*
