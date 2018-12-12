# SetupOpenCVinRaspPi
Step by step to setup, compile, and check build information of Open CV in Raspberry Pi.

In this setup I use OpenCV 3.1.0, you can select different version or latest version but the process remains the same.

Process need to be done:
   1. Installing dependencies / necessary packages
   2. Downloading of OpenCV source-code
   3. Compile OpenCV source-code
   4. Install compiled OpenCV library
   5. Get OpenCV build information (verify)


Code:
//-----Installation of all necessary packages for OpenCV-----//
sudo apt-get install -y build-essential cmake pkg-config
sudo apt-get install -y libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
sudo apt-get install -y libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install -y libxvidcore-dev libx264-dev
sudo apt-get install -y libgtk2.0-dev
sudo apt-get install -y libatlas-base-dev gfortran
sudo apt-get install -y python2.7-dev python3-dev

//-----OpenCV 3.1.0 source-code download------//
cd ~
wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.1.0.zip
unzip opencv.zip

wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.1.0.zip
unzip opencv_contrib.zip

//-----Numpy Installation------//
pip install numpy

//-----OpenCV 3.1.0 compilation------//
cd ~/opencv-3.1.0/
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE=RELEASE \
   -D ENABLE_PRECOMPILED_HEADERS=OFF \
   -D CMAKE_INSTALL_PREFIX=/usr/local \
   -D INSTALL_PYTHON_EXAMPLES=ON \
   -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.1.0/modules \
   -D BUILD_EXAMPLES=ON ..
    
make

//-----OpenCV 3.1.0 installation------//
sudo make install

//-----Create OpenCV library cache and links------//
sudo ldconfig

//-----Get OpenCV build information------//
python
import cv2
print cv2.getBuildInformation()
