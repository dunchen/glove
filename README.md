glove
=====
author: dunchen

2014/7/5


using camera, arduino chip, which is embeded into a wearable glove, and serveal sensors to create a new three diemsional human-computer interface.

###some perequests
1: this project needs to be used together with the arduino system, the code for which is in the repository glove-arduino. the computer, on which this code is running, needs to be connected to the arduino system through serial port.

2: this code is for the linux user and is tested in the Ubuntu 14.04

3: i assume that YOU have installed the OpenCV and Ogre liberary in the default path, the version that i tested the code with are OpenCV 2.4.4 and Ogre 1.8.1

4: i assume that you have installed cmake but DO NOT use command "cmake" since i have changed manually the /CMakeFiles/OgreApp.dir/link.txt in order to avoid some problems and link the OpenCV liberary. after every time you have changed the source code, you just need use command "make install" and everything will be fine. More explaination of the link.txt please read the last part of this text.

5: the basic structure of the project is based on the clean-project provided by the Ogre website, the link is here: http://www.ogre3d.org/tikiwiki/tiki-download_wiki_attachment.php?attId=141&download=y

###what really does this code do
#### the work process of the whole glove project:
    1: the arduino on the glove turn on the red light and initialize the UFR. then it keep transmitting realtime distance data to the computer through the serial port.
    2: the program on the computer initialize the default camera and display the real time image, waiting for the confirm of the success of initializing the camera.
    3: initialize the communication through the serial port
    4: the Ogre engine start the graphic rendering loop and between each frame, the program will process the image capture from the camera and distance data collected from the sensor. it will then calculate the location of the hand and move the camera-view-point accordingly inside the Ogre engine. 

    so, you can move your view point of the graph displayed on the screen simply by moving your hand.

#### the meaning and the creative points of this project
     1: i have merged two widely used liberaries: OpenCV and Ogre, the combination of which, in my perspective, would provide a simple and powerful realization of the Somatic Game.
     2: long before had some people tried to develop a tool to detect the hand motion and used that as the input to the computer program. the creative points of my design are mostly the following two parts:
          (a) i have just used one camera to locate the three dimensional location. other popular tools, like Kinect by MS, mostly use two or more cameras or motion detect sensors. i have used additional URF to solve this problem.
	  (b) all the equipments i used are very cheap and easily got. we don't need to pay hundred of dollars to get our own motion detect equipment. this is very important for me, a student with little money.

### how to use this project for your own aim
This project is mostly based on the clean-project and the tutorial frame work provided by the Ogre website. please read the tutorial and you will know clearly the structure of the code.

### some notification
####the serial port
   1: frequency 9600Hz
   2: read and write mode: RAW mode (without any change on the data transmitted and all the data is transmitted in the form of char)
   3: serial port number: the default is "/dev/ttyUSB0", you can see your own by typing the command "sudo domesg"
####about the /CMakeFiles/OgreApp.dir/link.txt
the link.txt is stated as follow:


  /usr/bin/c++ -O2 -g -I/usr/local/include/opencv -I/usr/local/include -DNDEBUG    CMakeFiles/OgreApp.dir/BaseApplication.cpp.o CMakeFiles/OgreApp.dir/TutorialApplication.cpp.o  -o dist/bin/OgreApp -L/usr/lib64 -lstdc++ -rdynamic /usr/local/lib/libOgreMain.so /usr/local/lib/libopencv_calib3d.so /usr/local/lib/libopencv_contrib.so /usr/local/lib/libopencv_core.so /usr/local/lib/libopencv_features2d.so /usr/local/lib/libopencv_flann.so /usr/local/lib/libopencv_gpu.so /usr/local/lib/libopencv_highgui.so /usr/local/lib/libopencv_imgproc.so /usr/local/lib/libopencv_legacy.so /usr/local/lib/libopencv_ml.so /usr/local/lib/libopencv_nonfree.so /usr/local/lib/libopencv_objdetect.so /usr/local/lib/libopencv_photo.so /usr/local/lib/libopencv_stitching.so /usr/local/lib/libopencv_ts.so /usr/local/lib/libopencv_video.so /usr/local/lib/libopencv_videostab.so -lboost_system -lOIS -Wl,-rpath,/usr/local/lib:

among them, "-I/usr/local/include/opencv -I/usr/local/include" and "/usr/local/lib/libopencv_calib3d.so /usr/local/lib/libopencv_contrib.so /usr/local/lib/libopencv_core.so /usr/local/lib/libopencv_features2d.so /usr/local/lib/libopencv_flann.so /usr/local/lib/libopencv_gpu.so /usr/local/lib/libopencv_highgui.so /usr/local/lib/libopencv_imgproc.so /usr/local/lib/libopencv_legacy.so /usr/local/lib/libopencv_ml.so /usr/local/lib/libopencv_nonfree.so /usr/local/lib/libopencv_objdetect.so /usr/local/lib/libopencv_photo.so /usr/local/lib/libopencv_stitching.so /usr/local/lib/libopencv_ts.so /usr/local/lib/libopencv_video.so /usr/local/lib/libopencv_videostab.so" are needed for the using of the OpenCV liberary.

and "-lboost_system" is to fix an original bug in the Ogre example project.






//yeti comes down from the jokul~~
//
