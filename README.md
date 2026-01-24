# Minor-Project

### 🏙️ Detection of Unplanned Urban Development using AI
A Multi-Approach Framework with K-Means, SSIM & U-Net

#### Minor Project (2024–25 Winter Sem)
Authors: Aryan Parashar & Prakhar Saxena
Institute: Interdisciplinary Centre for Artificial Intelligence,
Aligarh Muslim University (AMU)

### 📌 Project Overview

Rapid urbanization often leads to unplanned and unauthorized development, deviating from approved master plans. Manual monitoring is slow, subjective, and inefficient.

This project proposes an AI-driven framework to automatically detect urban deviations by comparing government master plans with recent satellite imagery, using a progressive pipeline that evolves from classical computer vision to deep learning.

The system not only performs detection but also visualizes results through an interactive Django web platform, making it accessible for planners, researchers, and authorities.

### 🎯 Objectives

Detect deviations between planned vs actual urban structures

Compare classical CV techniques with deep learning models

Quantify deviation using SSIM and tiling-based analysis

Segment urban features (buildings, roads) using U-Net

Present results via a professional web interface

Enable multi-location industrial site analysis

### 🧠 Methodology Pipeline

The project follows a step-by-step evolution of techniques:

#### 1️⃣ Image Preprocessing

Grayscale conversion

Text & legend removal from master plans

Noise reduction and normalization

#### 2️⃣ K-Means Clustering

Baseline segmentation of master plan regions

Color-based zoning extraction

Fast but sensitive to illumination changes

#### 3️⃣ Feature Alignment (ORB)

Keypoint matching between satellite and plan images

Homography-based spatial alignment

#### 4️⃣ Structural Similarity Index (SSIM)

Pixel-wise similarity computation

Deviation heatmap generation

Threshold-based compliance classification

#### 5️⃣ Deep Learning with U-Net

U-Net with ResNet-50 encoder (transfer learning)

Semantic segmentation of buildings and roads

Improved boundary precision and robustness

#### 6️⃣ Tiling-Based Deviation Analysis

Large images divided into spatial tiles

Localized SSIM computation

Area-wise deviation percentage estimation

### 🏗️ Industrial Site Case Studies

The system was tested on multiple industrial regions across Uttar Pradesh:

#### 📍 Aligarh District

Atrauli Industrial Area (1991)

CDF Chharat (2009)

Talanagari (2014)

Sagvan City (2017)

Ozone City (2005)

#### 📍 Hathras District

Salempur (2023)

#### 📍 Etah District

IA Etah (2002)

IID Center (2005)

Orni (2022)

Each site includes:

Satellite vs Master Plan comparison

SSIM deviation heatmap

U-Net segmentation mask

Final AI compliance overlay

Google Maps integration (via coordinates)

#### 🌐 Web Application (Django)

To make the project interactive and presentable, a Django-based web platform was developed.

🔹 Key Features

📖 Documentation Page – full ML pipeline explanation

🧾 Code Explorer – view .py, .md, .ipynb files in-browser

📊 Results Gallery – sliders, heatmaps, segmentation outputs

#### 🗺️ Multi-site Dashboard – industrial site-wise analysis

#### 🖼️ Notebook Rendering – plots & outputs rendered from .ipynb

🛠️ Tech Stack

Programming & ML

Python

OpenCV

NumPy, Pandas

Scikit-learn

PyTorch

segmentation-models-pytorch

SSIM (skimage)

Web & Visualization

Django

HTML, CSS, Bootstrap 5

JavaScript

Google Maps links

Tools

Jupyter Notebook

GitHub

Google Colab

📈 Key Results & Observations

Residential areas show higher deviation due to continuous modifications

Industrial zones show lower deviation due to regulated construction

U-Net significantly outperforms K-Means in boundary accuracy

Tiling-based SSIM provides localized deviation insights

Deep learning improves robustness under real-world conditions

#### 🛰️ Inspiration

This project was inspired by participation in the
ISRO Antariksh Hackathon, where exposure to satellite imagery and geospatial challenges motivated the idea of AI-based urban monitoring.

📂 Repository Structure

├── project_files/        # ML & CV source files

├── notebooks/            # Jupyter notebooks

├── static/               # Images, results, CSS

├── templates/            # Django templates

├── core/                 # Django app

├── manage.py

└── README.md

#### 🚀 Future Scope

Real-time satellite data integration

GIS layer support (QGIS / GeoJSON)

Mobile-friendly dashboard

Automated alert system for violations

Scaling to city/state-level monitoring

#### 👨‍💻 Authors

Prakhar Saxena
B.Tech (AI), AMU
AI • Computer Vision • Django

Aryan Parashar
B.Tech (AI), AMU
Machine Learning • Research

#### ⭐ Acknowledgements

Interdisciplinary Centre for Artificial Intelligence, AMU

ISRO Antariksh Hackathon

Open-source AI & CV community

⭐ If you found this project interesting, give it a star!

It motivates us to keep building 🚀
