## 0. FastDeploy

FastDeploy is an Easy-to-use and High Performance AI model deployment toolkit for Cloud, Mobile and Edge with out-of-the-box and unified experience, end-to-end optimization for over 150+ Text, Vision, Speech and Cross-modal AI models. FastDeploy Supports AI model deployment on
**X86 CPU、NVIDIA GPU、ARM CPU、XPU、NPU、IPU** etc. You can switch different inference backends and hardware with a single line of code.

Deploying AI model in 3 steps with FastDeploy: (1)Install FastDeploy SDK;  (2)Use FastDeploy's API to implement the deployment code;  (3) Deploy.

**Notes** : This document downloads FastDeploy examples to complete the high performance deployment experience; only X86 CPUs, NVIDIA GPUs are shown for reasoning and GPU environments are ready by default (e.g. CUDA >= 11.2, etc.), if you need to deploy AI model on other hardware or learn about FastDeploy's full capabilities, please refer to [FastDeploy GitHub](https://github.com/PaddlePaddle/FastDeploy).

## 1. Install FastDeploy SDK
```
pip install fastdeploy-gpu-python==0.0.0 -f https://www.paddlepaddle.org.cn/whl/fastdeploy_nightly_build.html
```
## 2. Run Deployment Example
```
# download deployment example
git clone https://github.com/PaddlePaddle/FastDeploy.git
cd  FastDeploy/examples/vision/classification/paddleclas/python

#  download HGNet model and test image
wget https://bj.bcebos.com/paddlehub/fastdeploy/PPHGNet_tiny_ssld_infer.tgz
tar xvfz PPHGNet_tiny_ssld_infer.tgz
wget https://gitee.com/paddlepaddle/PaddleClas/raw/release/2.4/deploy/images/ImageNet/ILSVRC2012_val_00000010.jpeg

# CPU deployment
python infer.py --model PPHGNet_tiny_ssld_infer --image ILSVRC2012_val_00000010.jpeg --device cpu --topk 1
# GPU deployment
python infer.py --model PPHGNet_tiny_ssld_infer --image ILSVRC2012_val_00000010.jpeg --device gpu --topk 1
#TensorRT inference on GPU (note: if you run TensorRT inference the first time, there is a serialization of the model, which is time-consuming and requires patience)
python infer.py --model PPHGNet_tiny_ssld_infer --image ILSVRC2012_val_00000010.jpeg --device gpu --use_trt True --topk 1
#IPU inference (note: the first run of IPU inference will have serialized model operations, which will take a certain amount of time, so you need to wait patiently)
python infer.py --model PPHGNet_tiny_ssld_infer --image ILSVRC2012_val_00000010.jpeg --device ipu --topk 1
```

The results returned after the operation is completed are as follows：

```bash
==============================PPHGNet_tiny_ssld==============================
cpu_label: 153, cpu_score: 0.536040
ipu_label: 153, ipu_score: 0.536039
==============================PPHGNet_tiny_ssld==============================
```