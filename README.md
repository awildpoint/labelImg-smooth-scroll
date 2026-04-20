## 使用方法

1. 下载.zip源码解压后，在新虚拟环境中安装lxml和pyqt5
2. 运行labelImg.py即可在中文软件窗口中进行标注工作。
3. 运行'pip install -e .',可在环境路径下Scripts/labelimg.exe双击启动
## Hotkeys

仅对以下三处作出修改。

| **操作分类** | **快捷键 / 动作**          | **功能描述**                    | **状态**    |
| -------- | --------------------- | --------------------------- | --------- |
| **视图交互** | **鼠标右键拖拽**            | **抓手工具：平移放大的图片位置**          | **[已修改]** |
|          | **鼠标滚轮**              | **放大 / 缩小图片**               | **[已修改]** |
|          | `Ctrl` + `Shift` + 滚轮 | 增加 / 降低图片亮度                 | 未改动       |
| **标注操作** | `W`                   | 开始绘制矩形框 (Create RectBox)    | 未改动       |
|          | `E`                   | 编辑模式                        | **[已修改]** |
|          | `D`                   | 下一张图片 (Next Image)          | 未改动       |
|          | `A`                   | 上一张图片 (Prev Image)          | 未改动       |
|          | `Del`                 | 删除选中的标注框                    | 未改动       |
|          | `Ctrl` + `D`          | 复制当前选中的标注框                  | 未改动       |
|          | `Ctrl` + `+` / `-`    | 放大 / 缩小 (键盘方式)              | 未改动       |
|          | `Space`               | 将当前标注置为“已验证” (Verify Image) | 未改动       |

[![image](/readme/images/labelimg.png)](https://github.com/heartexlabs/label-studio)

Label Studio is a modern, multi-modal data annotation tool =======

LabelImg, the popular image annotation tool created by Tzutalin with the help of dozens contributors, is no longer actively being developed and has become part of the Label Studio community. Check out [Label Studio](https://github.com/heartexlabs/label-studio), the most flexible open source data labeling tool for images, text, hypertext, audio, video and time-series data. [Install](https://labelstud.io/guide/install.html) Label Studio and join the [slack community](https://label-studio.slack.com/) to get started.

[![image](/readme/images/label-studio-1-6-player-screenshot.png)](https://github.com/heartexlabs/label-studio)

About LabelImg ========

[![image](https://img.shields.io/pypi/v/labelimg.svg)](https://pypi.python.org/pypi/labelimg)

![GitHub Workflow Status](https://img.shields.io/github/workflow/status/tzutalin/labelImg/Package?style=for-the-badge)

[![image](https://img.shields.io/badge/lang-en-blue.svg)](https://github.com/tzutalin/labelImg)

[![image](https://img.shields.io/badge/lang-zh-green.svg)](https://github.com/tzutalin/labelImg/blob/master/readme/README.zh.rst)

[![image](https://img.shields.io/badge/lang-jp-green.svg)](https://github.com/tzutalin/labelImg/blob/master/readme/README.jp.rst)

LabelImg is a graphical image annotation tool.

It is written in Python and uses Qt for its graphical interface.

Annotations are saved as XML files in PASCAL VOC format, the format used by [ImageNet](http://www.image-net.org/). Besides, it also supports YOLO and CreateML formats.

![Demo Image](https://raw.githubusercontent.com/tzutalin/labelImg/master/demo/demo3.jpg)

![Demo Image](https://raw.githubusercontent.com/tzutalin/labelImg/master/demo/demo.jpg)

[Watch a demo video](https://youtu.be/p0nR2YsCY_U)

# Installation

## Get from PyPI but only python3.0 or above

This is the simplest (one-command) install method on modern Linux distributions such as Ubuntu and Fedora.

``` shell
pip3 install labelImg
labelImg
labelImg [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

## Build from source

Linux/Ubuntu/Mac requires at least [Python 2.6](https://www.python.org/getit/) and has been tested with [PyQt 4.8](https://www.riverbankcomputing.com/software/pyqt/intro). However, [Python 3 or above](https://www.python.org/getit/) and [PyQt5](https://pypi.org/project/PyQt5/) are strongly recommended.

### Ubuntu Linux

Python 3 + Qt5

``` shell
sudo apt-get install pyqt5-dev-tools
sudo pip3 install -r requirements/requirements-linux-python3.txt
make qt5py3
python3 labelImg.py
python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

### macOS

Python 3 + Qt5

``` shell
brew install qt  # Install qt-5.x.x by Homebrew
brew install libxml2

or using pip

pip3 install pyqt5 lxml # Install qt and lxml by pip

make qt5py3
python3 labelImg.py
python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

Python 3 Virtualenv (Recommended)

Virtualenv can avoid a lot of the QT / Python version issues

``` shell
brew install python3
pip3 install pipenv
pipenv run pip install pyqt5==5.15.2 lxml
pipenv run make qt5py3
pipenv run python3 labelImg.py
[Optional] rm -rf build dist; pipenv run python setup.py py2app -A;mv "dist/labelImg.app" /Applications
```

Note: The Last command gives you a nice .app file with a new SVG Icon in your /Applications folder. You can consider using the script: build-tools/build-for-macos.sh

### Windows

Install [Python](https://www.python.org/downloads/windows/), [PyQt5](https://www.riverbankcomputing.com/software/pyqt/download5) and [install lxml](http://lxml.de/installation.html).

Open cmd and go to the [labelImg](#labelimg) directory

``` shell
pyrcc4 -o libs/resources.py resources.qrc
For pyqt5, pyrcc5 -o libs/resources.py resources.qrc

python labelImg.py
python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

If you want to package it into a separate EXE file

``` shell
Install pyinstaller and execute:

pip install pyinstaller
pyinstaller --hidden-import=pyqt5 --hidden-import=lxml -F -n "labelImg" -c labelImg.py -p ./libs -p ./
```

### Windows + Anaconda

Download and install [Anaconda](https://www.anaconda.com/download/#download) (Python 3+)

Open the Anaconda Prompt and go to the [labelImg](#labelimg) directory

``` shell
conda install pyqt=5
conda install -c anaconda lxml
pyrcc5 -o libs/resources.py resources.qrc
python labelImg.py
python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

## Use Docker

``` shell
docker run -it 
--user $(id -u) 
-e DISPLAY=unix$DISPLAY 
--workdir=$(pwd) 
--volume="/home/$USER:/home/$USER" 
--volume="/etc/group:/etc/group:ro" 
--volume="/etc/passwd:/etc/passwd:ro" 
--volume="/etc/shadow:/etc/shadow:ro" 
--volume="/etc/sudoers.d:/etc/sudoers.d:ro" 
-v /tmp/.X11-unix:/tmp/.X11-unix 
tzutalin/py2qt4

make qt4py2;./labelImg.py
```

You can pull the image which has all of the installed and required dependencies. [Watch a demo video](https://youtu.be/nw1GexJzbCI)

# Usage

## Steps (PascalVOC)

1.  Build and launch using the instructions above.
2.  Click 'Change default saved annotation folder' in Menu/File
3.  Click 'Open Dir'
4.  Click 'Create RectBox'
5.  Click and release left mouse to select a region to annotate the rect box
6.  You can use right mouse to drag the rect box to copy or move it

The annotation will be saved to the folder you specify.

You can refer to the below hotkeys to speed up your workflow.

## Steps (YOLO)

1.  In `data/predefined_classes.txt` define the list of classes that will be used for your training.
2.  Build and launch using the instructions above.
3.  Right below "Save" button in the toolbar, click "PascalVOC" button to switch to YOLO format.
4.  You may use Open/OpenDIR to process single or multiple images. When finished with a single image, click save.

A txt file of YOLO format will be saved in the same folder as your image with same name. A file named "classes.txt" is saved to that folder too. "classes.txt" defines the list of class names that your YOLO label refers to.

Note:

- Your label list shall not change in the middle of processing a list of images. When you save an image, classes.txt will also get updated, while previous annotations will not be updated.
- You shouldn't use "default class" function when saving to YOLO format, it will not be referred.
- When saving as YOLO format, "difficult" flag is discarded.

## Create pre-defined classes

You can edit the [data/predefined_classes.txt](https://github.com/tzutalin/labelImg/blob/master/data/predefined_classes.txt) to load pre-defined classes

## Annotation visualization

1.  Copy the existing lables file to same folder with the images. The labels file name must be same with image file name.
2.  Click File and choose 'Open Dir' then Open the image folder.
3.  Select image in File List, it will appear the bounding box and label for all objects in that image.

(Choose Display Labels mode in View to show/hide lablels)

  
**Verify Image:**

When pressing space, the user can flag the image as verified, a green background will appear. This is used when creating a dataset automatically, the user can then through all the pictures and flag them instead of annotate them.

**Difficult:**

The difficult field is set to 1 indicates that the object has been annotated as "difficult", for example, an object which is clearly visible but difficult to recognize without substantial use of context. According to your deep neural network implementation, you can include or exclude difficult objects during training.

## How to reset the settings

In case there are issues with loading the classes, you can either:

1.  From the top menu of the labelimg click on Menu/File/Reset All

2.  

    Remove the [.labelImgSettings.pkl]{.title-ref} from your home directory. In Linux and Mac you can do:

    :   [rm ~/.labelImgSettings.pkl]{.title-ref}

## How to contribute

Send a pull request

## License

[Free software: MIT license](https://github.com/tzutalin/labelImg/blob/master/LICENSE)

Citation: Tzutalin. LabelImg. Git code (2015). <https://github.com/tzutalin/labelImg>

## Related and additional tools

1.  [Label Studio](https://github.com/heartexlabs/label-studio) to label images, text, audio, video and time-series data for machine learning and AI
2.  [ImageNet Utils](https://github.com/tzutalin/ImageNet_Utils) to download image, create a label text for machine learning, etc
3.  [Use Docker to run labelImg](https://hub.docker.com/r/tzutalin/py2qt4)
4.  [Generating the PASCAL VOC TFRecord files](https://github.com/tensorflow/models/blob/4f32535fe7040bb1e429ad0e3c948a492a89482d/research/object_detection/g3doc/preparing_inputs.md#generating-the-pascal-voc-tfrecord-files)
5.  [App Icon based on Icon by Nick Roach (GPL)](https://www.elegantthemes.com/)
6.  [Setup python development in vscode](https://tzutalin.blogspot.com/2019/04/set-up-visual-studio-code-for-python-in.html)
7.  [The link of this project on iHub platform](https://code.ihub.org.cn/projects/260/repository/labelImg)
8.  [Convert annotation files to CSV format or format for Google Cloud AutoML](https://github.com/tzutalin/labelImg/tree/master/tools)

## Stargazers over time

![image](https://starchart.cc/tzutalin/labelImg.svg)
