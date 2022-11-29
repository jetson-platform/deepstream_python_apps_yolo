# Use the YOLOv5 model in [deepstream_python_apps](https://github.com/NVIDIA-AI-IOT/deepstream_python_apps)

## After this steps [LINK](https://github.com/CV-Jetson-Nano/YOLOv5_install_deepstream)

## git clone deepstream_python_apps

```bash
cd ~
git clone --branch v1.1.1 https://github.com/NVIDIA-AI-IOT/deepstream_python_apps.git
```

## Install Necessary Packages

```bash
sudo apt install libgirepository1.0-dev gcc libcairo2-dev pkg-config python3-dev gir1.2-gtk-3.0

pip3 install pycairo

pip3 install PyGObject

pip3 install pyds-ext
```

## Change model configuration

```bash
cd deepstream_python_apps/apps/deepstream-test1

cp ~/DeepStream-Yolo/config_infer_primary_yoloV5.txt dstest1_pgie_config.txt

cp ~/DeepStream-Yolo/yolov5s.cfg .

cp ~/DeepStream-Yolo/yolov5s.wts .

mkdir  nvdsinfer_custom_impl_Yolo

cp ~/DeepStream-Yolo/nvdsinfer_custom_impl_Yolo/libnvdsinfer_custom_impl_Yolo.so ./nvdsinfer_custom_impl_Yolo

cp ~/DeepStream-Yolo/labels.txt ./

cp ~/opt/nvidia/deepstream/deepstream/samples/streams/sample_720.h264 ./
```

## implement this file deepstream_test_1.py
according to this steps

step 1:
```python

PGIE_CLASS_ID_VEHICLE = 0
PGIE_CLASS_ID_BICYCLE = 1
PGIE_CLASS_ID_PERSON = 2
PGIE_CLASS_ID_ROADSIGN = 3

# to

PGIE_CLASS_ID_PERSON = 0
```

step 2:
```python
obj_counter = {
        PGIE_CLASS_ID_VEHICLE:0,
        PGIE_CLASS_ID_PERSON:0,
        PGIE_CLASS_ID_BICYCLE:0,
        PGIE_CLASS_ID_ROADSIGN:0
    }

# to

obj_counter = {
        PGIE_CLASS_ID_PERSON:0
    }
```

step 3:
```python
obj_counter[obj_meta.class_id] += 1

# to

obj_counter[0] += 1
```

step 4:
```python
py_nvosd_text_params.display_text = "Frame Number={} Number of Objects={} Vehicle_count={} Person_count={}".format(frame_number, num_rects, obj_counter[PGIE_CLASS_ID_VEHICLE], obj_counter[PGIE_CLASS_ID_PERSON])

# to

py_nvosd_text_params.display_text = "Person_count={}".format( obj_counter[PGIE_CLASS_ID_PERSON])
```

## Run the Inference 

```bash
python deepstream_test_1.py sample_720.h264
```

# To run RTSP url or .mp4

```bash
python3 deepstream_test_3.py <uri1> [uri2] ... [uriN]
```
e.g:
```bash
python3 deepstream_test_3.py file:///opt/nvidia/deepstream/deepstream-6.0/samples/streams/sample_720p.mp4
# NOTE:
# Give absolute path, relative path is not supported

python3 deepstream_test_3.py rtsp://admin:888888aa@192.168.0.31
```

