# Use the YOLOv5 model in deepstream_python_apps

## git clone deepstream_python_apps

```bash
cd ~
git clone --branch v1.1.1 https://github.com/NVIDIA-AI-IOT/deepstream_python_apps.git
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