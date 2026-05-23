# PyLUSAT-

**This repository include the reproducible codes, processes and relevant contents about the thesis:PyLUSAT: An open-source Python toolkit for GIS-based land use suitability analysis made by Yang. Li, Dong and Mai.**

#项目名称：PyLUSAT文献复现分析报告

##项目简介：

- 文献名称：PyLUSAT: An open-source Python toolkit for GIS-based land use suitability analysis

- 作者：Changjie Chen, Jasmeet Judge, David Hulse

- 发表期刊：Environmental Modelling & Software

- 发表时间：2025年

- 文章链接： https://www.sciencedirect.com/science/article

- 项目概述：本项目依托矢量 GIS 技术框架，整合地理空间运算、数据转换、聚合分析三大类核心功能，开发了PyLUSAT这一开源、跨平台、高效率且可拓展的python工具包，主要应用于土地利用适宜性分析效率和精度的提升，为国土空间规划、生态格局优化、城镇用地布局等研究提供了轻量化、高效可复用的开源技术支撑。

##数据说明：

- 数据来源：
  
  1. https://github.com/chjch/pylusat/tree/master/pylusat/datasets 示例数据
  
  2. ArcGIS标准空间数据（土地利用数据、地形数据和距离因子数据等）

- 数据格式：
  
  | 数据类型 | 具体数据             | 格式        | 用途        |
  | ---- | ---------------- | --------- | --------- |
  | 栅格数据 | DEM、适宜性栅格和距离栅格   | GeoTIFF   | 道路/线状空间对象 |
  | 矢量数据 | 道路数据、河流数据和土地利用图层 | Shapefile | 空间统计区域    |

- 变量说明：PyLUSAT主要处理ArcGIS中的栅格与矢量数据，这些数据共同构成了典型土地利用适宜性分析中的评价因子与约束条件，继而通过加权分析实现土地适宜性分析、距离分析与空间叠加计算。

##文件结构：

、、、



data/    -  数据文件

scripts/   - 复现步骤

results/  - 复现结果



、、、

##运行环境：

- Anaconda Prompt version: 25.11.1 （[Anaconda, Inc. (formerly Continuum Analytics, Inc.) · GitHub](https://github.com/ContinuumIO)）

- Jupyter Notebook version: 2.16.0   [(https://github.com/jupyter/notebook)](https://github.com/jupyter/notebook)

##作者

- 杨丽萍  2025303110007

- 李春雪   2025303120171

- 董娟     2025303120140

- 买柯馨    2025303120066
