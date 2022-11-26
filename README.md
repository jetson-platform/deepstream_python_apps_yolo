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

## Change model confugiration

```bash
cd deepstream_python_apps/apps/deepstream-test1

cp ~/DeepStream-Yolo/config_infer_primary_yoloV5.txt dstest1_pgie_config.txt

cp ~/DeepStream-Yolo/yolov5s.cfg .

cp ~/DeepStream-Yolo/yolov5s.wts .

mkdir  nvdsinfer_custom_impl_Yolo

cp ~/DeepStream-Yolo/nvdsinfer_custom_impl_Yolo/libnvdsinfer_custom_impl_Yolo.so ./nvdsinfer_custom_impl_Yolo

cp ~/DeepStream-Yolo/labels.txt ./

cp ~/opt/nvidia/deepstream/deepstream/samples/streams/sample_1080p_h264.mp4
```
## Run the Inference 

```bash
python deepstream_test_1.py sample_1080p_h264.mp4
```