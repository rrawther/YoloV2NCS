# YOLOv2 for Intel/Movidius Neural Compute Stick (NCS)

*This project shows how to run tiny yolov2 (20 classes) with AMD's NN inference engine(Annie):*
+ A python convertor from yolo to caffe
+ A c/c++ implementation and python wrapper for region layer of yolov2
+ A sample for running yolov2 with Annie

---

### Preliminaries
Please install amd ModelCompiler from https://github.com/GPUOpen-ProfessionalCompute-Libraries/amdovx-modules.git.

### Step 1. Compile Python Wrapper
```make```

### Step 2. Convert Caffe to Annie python lib as shown ModelCompiler (amdovx-modules/utils/model_compiler/)
### convert caffe to AMD NNIR format and compile NNIR to deployment python lib using the following steps


```
% python caffe2nnir.py ./models/caffemodels/yoloV2Tiny20.caffemodel <nnirOutputFolder> --input-dims 1,3,416,416
% follow the rest of the steps in ModelCompiler page to build python lib
```
There will be a file libannpython.so and weights.bin

### Step 3. Run tests
```	
python3 ./detectionExample/Main.py --image ./data/dog.jpg --annpythonlib <libannpython.so> --weights <weights.bin>
```
This runs inference and detections and results will be like this: 
![](/data/yolo_dog.jpg)

# Run Other YoloV2 models
### Convert Yolo to Caffe 
```
Install caffe and config the python environment path.
sh ./models/convertyo.sh
```
Tips:

Please ignore the error message similar as "Region layer is not supported".

The converted caffe models should end with "prototxt" and "caffemodel".

### Update parameters

Please update parameters (biases, object names, etc) in ./src/CRegionLayer.cpp, and parameters (dim, blockwd, targetBlockwd, classe, etc) in ./detectionExample/ObjectWrapper.py.

Please read ./src/CRegionLayer.cpp and ./detectionExample/ObjectWrapper.py for details.

# References
+ [caffe](https://github.com/BVLC/caffe)
+ [yolo](https://github.com/pjreddie/darknet)
+ [caffe-yolo](https://github.com/xingwangsfu/caffe-yolo)

# Contributors
+ [ichigoi7e](https://github.com/ichigoi7e)
+ [nathiyaa](https://github.com/nathiyaa)
+ [cpagravel](https://github.com/cpagravel)

---

# License
Research Only

# Author
duangenquan@gmail.com
