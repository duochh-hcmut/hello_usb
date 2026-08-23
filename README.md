# hello_usb

## Development Environment setup

1. Install bazelisk
2. Install libusb-1.0-0
3. Install Python
4. Install Pip
5. Add Python venv
6. Verify

```sh
/usr/local/bin/bazelisk build \
    tensorflow/lite/micro/examples/hello_world:train \
    bazel-bin/tensorflow/lite/micro/examples/hello_world/train \
    --save_tf_model \
    --save_dir=/tmp/model_created/

wget 
sudo dpkg -i bazelisk-amd64.deb
git submodule add https://github.com/tensorflow/tflite-micro.git
bazelisk version
bazel version
bazel info workspace

python3 -m venv venv
source venv/bin/activate
python3 -m pip install --upgrade pip
python3 -m pip install -r ~/rp2050/hello_usb/requirements.txt
mkdir /tmp/hello_usb && mkdir /tmp/hello_usb/model_created && mkdir /tmp/hello_usb/quant_model
bazel build tensorflow/lite/micro/examples/hello_world:train
bazel-bin/tensorflow/lite/micro/examples/hello_world/train --save_tf_model --save_dir=/tmp/hello_usb/model_created/
python3 -c "import tensorflow as tf; print('TensorFlow:', tf.__version__)"
python -c "import keras; print('Keras:', keras.__version__)"
grep -R "save_format.*tf" -n tensorflow/lite/micro/examples/hello_world
#model.save(FLAGS.save_dir, save_format="tf")
# Fix for TF 2.13, save_format="tf" is deprecated
bazel-bin/tensorflow/lite/micro/examples/hello_world/quantization/ptq  
--source_model_dir=/tmp/hello_usb/model_created/ --target_dir=/tmp/hello_usb/quant_model/
xxd -i /model/model_created/hello_world_float.tflite > model/model_created/hello_world_float.cc

make -f tensorflow/lite/micro/tools/make/Makefile hello
```
