# Real-time 3D Reconstruction via RGB-D Camera
This is my implementation of real-time 3D reconstruction using Intel RealSense D435i RGB-D camera, following this [official tutorial](http://www.open3d.org/docs/latest/tutorial/t_reconstruction_system/index.html).

## Set up Environment
Tested on Windows 10, with AMD® Ryzen 9 7900x & NVIDIA GeForce RTX 3090 Ti.
```bash
conda create --name open3d
conda activate open3d
conda install pip
pip install open3d
pip install pyrealsense2
pip install opencv-python
```

## Capture Your Own Dataset
Tips for capturing:
- Capture scene with feature, not plain wall
- Capture as holistic space as possible, and walk toward further for accuracy
  
Follow [Capture your own dataset tutorial](http://www.open3d.org/docs/latest/tutorial/reconstruction_system/capture_your_own_dataset.html#capture-your-own-dataset)
- Change directory to: Open3D\examples\python\reconstruction_system\sensors
- Output in: Open3D\examples\python\reconstruction_system\dataset
- run: `python realsense_recorder.py --record_imgs`
- Move `\reconstruction_system\dataset` to `\t_reconstruction_system`
- Change directory to `Open3D\examples\python\t_reconstruction_system`
- Create a new FL_config.yml
    - copy defaul_config.yml
    - modify:
     ```
     path_dataset: dataset
     path_intrinsic: FL_camera_intrinsic.json
     ```
Alternatively, you can record from RealSense Viewer and save a bag file
- then in FL_config.yml, modify: `path_dataset: 20231010_011717.bag # only if recorded with realsense viewer`

Make sure the directory structure is as follow
```
t_reconstruction_system
	-> dense_slam_gui.py # to run
	-> FL_camera_intrisic.python
	-> FL_config.yml
	-> dataset
		-> color
		-> depth
	-> 20231010_011717.bag # only if recorded with realsense viewer
# will be created
	-> output.log
	-> output.npz
	-> output.ply
```

## Run reconstruction
Follow [reconstruction tutorial](http://www.open3d.org/docs/latest/tutorial/t_reconstruction_system/index.html)
```
python dense_slam_gui.py --device "CUDA:0" --config FL_config.yml
```

## Result
<img width="500" alt="office_real-sense_2" src="https://github.com/felicialuo/Open3D/assets/129685045/29c0371d-ba3e-4e73-a5a2-2e159bdbc37d">
<img width="500" alt="office_real-sense" src="https://github.com/felicialuo/Open3D/assets/129685045/7d79f032-ee64-40d0-9810-09cc99b3d7e8">  

**-- END of my implementation--**
 


<p align="center">
<img src="https://raw.githubusercontent.com/isl-org/Open3D/master/docs/_static/open3d_logo_horizontal.png" width="320" />
</p>

# Open3D: A Modern Library for 3D Data Processing

<h4>
    <a href="http://www.open3d.org">Homepage</a> |
    <a href="http://www.open3d.org/docs">Docs</a> |
    <a href="http://www.open3d.org/docs/release/getting_started.html">Quick Start</a> |
    <a href="http://www.open3d.org/docs/release/compilation.html">Compile</a> |
    <a href="http://www.open3d.org/docs/release/index.html#python-api-index">Python</a> |
    <a href="http://www.open3d.org/docs/release/cpp_api.html">C++</a> |
    <a href="https://github.com/isl-org/Open3D-ML">Open3D-ML</a> |
    <a href="https://github.com/isl-org/Open3D/releases">Viewer</a> |
    <a href="http://www.open3d.org/docs/release/contribute/contribute.html">Contribute</a> |
    <a href="https://www.youtube.com/channel/UCRJBlASPfPBtPXJSPffJV-w">Demo</a> |
    <a href="https://github.com/isl-org/Open3D/discussions">Forum</a>
</h4>

Open3D is an open-source library that supports rapid development of software
that deals with 3D data. The Open3D frontend exposes a set of carefully selected
data structures and algorithms in both C++ and Python. The backend is highly
optimized and is set up for parallelization. We welcome contributions from
the open-source community.

[![Ubuntu CI](https://github.com/isl-org/Open3D/actions/workflows/ubuntu.yml/badge.svg)](https://github.com/isl-org/Open3D/actions?query=workflow%3A%22Ubuntu+CI%22)
[![macOS CI](https://github.com/isl-org/Open3D/actions/workflows/macos.yml/badge.svg)](https://github.com/isl-org/Open3D/actions?query=workflow%3A%22macOS+CI%22)
[![Windows CI](https://github.com/isl-org/Open3D/actions/workflows/windows.yml/badge.svg)](https://github.com/isl-org/Open3D/actions?query=workflow%3A%22Windows+CI%22)

**Core features of Open3D include:**

-   3D data structures
-   3D data processing algorithms
-   Scene reconstruction
-   Surface alignment
-   3D visualization
-   Physically based rendering (PBR)
-   3D machine learning support with PyTorch and TensorFlow
-   GPU acceleration for core 3D operations
-   Available in C++ and Python

Here's a brief overview of the different components of Open3D and how they fit
together to enable full end to end pipelines:

![Open3D_layers](https://github.com/isl-org/Open3D/assets/41028320/e9b8645a-a823-4d78-8310-e85207bbc3e4)

For more, please visit the [Open3D documentation](http://www.open3d.org/docs).

## Python quick start

Pre-built pip packages support Ubuntu 18.04+, macOS 10.15+ and Windows 10+
(64-bit) with Python 3.8-3.11.

```bash
# Install
pip install open3d       # or
pip install open3d-cpu   # Smaller CPU only wheel on x86_64 Linux (v0.17+)

# Verify installation
python -c "import open3d as o3d; print(o3d.__version__)"

# Python API
python -c "import open3d as o3d; \
           mesh = o3d.geometry.TriangleMesh.create_sphere(); \
           mesh.compute_vertex_normals(); \
           o3d.visualization.draw(mesh, raw_mode=True)"

# Open3D CLI
open3d example visualization/draw
```

To get the latest features in Open3D, install the
[development pip package](http://www.open3d.org/docs/latest/getting_started.html#development-version-pip).
To compile Open3D from source, refer to
[compiling from source](http://www.open3d.org/docs/release/compilation.html).

## C++ quick start

Checkout the following links to get started with Open3D C++ API

-   Download Open3D binary package: [Release](https://github.com/isl-org/Open3D/releases) or [latest development version](http://www.open3d.org/docs/latest/getting_started.html#c)
-   [Compiling Open3D from source](http://www.open3d.org/docs/release/compilation.html)
-   [Open3D C++ API](http://www.open3d.org/docs/release/cpp_api.html)

To use Open3D in your C++ project, checkout the following examples

-   [Find Pre-Installed Open3D Package in CMake](https://github.com/isl-org/open3d-cmake-find-package)
-   [Use Open3D as a CMake External Project](https://github.com/isl-org/open3d-cmake-external-project)

## Open3D-Viewer app

<img width="480" src="https://raw.githubusercontent.com/isl-org/Open3D/master/docs/_static/open3d_viewer.png">

Open3D-Viewer is a standalone 3D viewer app available on Debian (Ubuntu), macOS
and Windows. Download Open3D Viewer from the
[release page](https://github.com/isl-org/Open3D/releases).

## Open3D-ML

<img width="480" src="https://raw.githubusercontent.com/isl-org/Open3D-ML/master/docs/images/getting_started_ml_visualizer.gif">

Open3D-ML is an extension of Open3D for 3D machine learning tasks. It builds on
top of the Open3D core library and extends it with machine learning tools for
3D data processing. To try it out, install Open3D with PyTorch or TensorFlow and check out
[Open3D-ML](https://github.com/isl-org/Open3D-ML).

## Communication channels

-   [GitHub Issue](https://github.com/isl-org/Open3D/issues): bug reports,
    feature requests, etc.
-   [Forum](https://github.com/isl-org/Open3D/discussions): discussion on the usage of Open3D.
-   [Discord Chat](https://discord.gg/D35BGvn): online chats, discussions,
    and collaboration with other users and developers.

## Citation

Please cite [our work](https://arxiv.org/abs/1801.09847) if you use Open3D.

```bib
@article{Zhou2018,
    author    = {Qian-Yi Zhou and Jaesik Park and Vladlen Koltun},
    title     = {{Open3D}: {A} Modern Library for {3D} Data Processing},
    journal   = {arXiv:1801.09847},
    year      = {2018},
}
```
