# vision-based-localization
OS : Ubuntu 18.04.3 LTS  
OpenCV version : 4.1.1  
OpenGL version : 4.3  

비전 기반 카메라 위치 추출 및 openGL 연동

<img src="./_practice/img/result_object.gif" width="60%">

----

#### Required Library
- assimp  
  <pre>$ sudo apt-get install libassimp-dev assimp-utils
  $ sudo apt-get install libxmu-dev libxi-dev</pre>

- glfw  
  <pre>$ sudo apt-get install libglfw3-dev libglfw3</pre>  

- glm  
  <pre>$ sudo apt install libglm-dev</pre>

----
  
### 1. ChArUco
1) make a charucoboard to calibrate  
   <code>
   g++ -o charucoboard charucoboard.cpp $(pkg-config opencv4 --cflags --libs)
   </code>  
   create <code>board.jpg</code>
2) calibrate  
   <code>
    $ g++ -o calibrate calibrate.cpp $(pkg-config opencv4 --cflags --libs)   
   </code>  
   press 'c' 5 or more times. 'ESC' to finish and calibrate.
   create <code>output.txt</code>

### 2. Build
1) In "KnuMakerViewer", <code>$ cmake CMakeLists.txt</code>
2) create <code>viewer</code> by <code>$ make</code> 

#### Error - 하드웨어 성능 차이
- GLSL 3.30 is not supported : In <code>./KnuMarkerViewer/shader/grid.vs</code>, change like this.  
  <pre>
  #version 130
  
  // ...
  in vec3 vertexPosition;
  in vec3 vertexColor;
  ...</pre>  
  In <code>./KnuMarkerViewer/shader/grid.fs</code>, change like this.
  <pre>
  #version 130
  ...</pre>

### 3. Run
1) <code> $./viewer </code>  
   default - marker ID : 0, threadMode : 0(= false), camera ID : 0  
2) <code> $./viewer (marker ID) </code>   
   <code> $./viewer (marker ID) (threadMode)</code>  
   <code> $./viewer (marker ID) (threadMode) (cameara ID)</code>   
   
   -> 프레임 향상을 위해 threadMode 활성화 시 <code>1</code> 입력   
   -> maker ID : imgui 메뉴로 통합 예정

### 4. Result 
  <img src="./_practice/img/result.png">
  
  - 2019.11.12_ 삼각형, 사각형 오브젝트 추가
  <img src="./_practice/img/result_object.gif">
  <img src="./_practice/img/result_object2.gif">  
  
----
