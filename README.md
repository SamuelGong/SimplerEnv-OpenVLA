# Guidance

> [This](README-old.md) is the project's original README.

## Preliminary

First, create a new environment

```bash
conda create -n simpler_env Python=3.10 -y
conda activate simpler_env
```


Then, pull the repo and install all the requirements as per the instructions given by the original README

```bash
git clone git@github.com:SamuelGong/SimplerEnv-OpenVLA.git --recurse-submodules --depth 1
# Note that "--recurse-submodules --depth 1" is IMPORTANT!
cd SimplerEnv-OpenVLA

cd ManiSkill2_real2sim
pip install -e .
pip install numpy==1.24.4

cd ..
pip install -e .
pip install -r requirements_full_install.txt
pip install git+https://github.com/nathanrooy/simulated-annealing
pip install --upgrade scipy
```

Suppose that we are interested in running OpenVLA, then also do

```bash
pip install torch==2.3.1 torchvision==0.18.1 timm==0.9.10 tokenizers==0.15.2 accelerate==0.32.1
pip install flash-attn==2.6.1 --no-build-isolation
```

Finally, there are also some system packages that need installing:

```bash
sudo apt install ffmpeg

sudo apt install vulkan-utils
sudo apt install libvulkan1
# If you do not have sudo, can also do it via:
# cd $HOME
# mkdir vulkan-sdk
# tar -xvf vulkansdk-linux-x86_64-1.4.328.1.tar.xz -C ./vulkan-sdk
# vim .bashrc
# Added the following content:
# export VULKAN_SDK=/home/jiangzhifeng/vulkan-sdk/1.4.328.1/x86_64
# export PATH=$VULKAN_SDK/bin:$PATH
# export LD_LIBRARY_PATH=$VULKAN_SDK/lib:$LD_LIBRARY_PATH
# 
# Then do:
# source .bashrc
# conda activate simpler_env
```

## Run

First download the OpenVLA model:

```bash
cd $HOME
mkdir vla-models
cd vla-models
git clone https://huggingface.co/openvla/openvla-7b
```

And then:

```bash
cd simpler_env
unset DISPLAY  # to be safe on a headless box
python main_inference.py \
  --policy-model openvla \
  --env-name GraspSingleOpenedCokeCanInScene-v0 \
  --ckpt-path $HOME/vla-models/openvla-7b \
  --robot google_robot_static \
  --policy-setup google_robot \
  --scene-name google_pick_coke_can_1_v4

# or
python main_inference.py \
  --policy-model openvla \
  --env-name PutCarrotOnPlateInScene-v0 \
  --ckpt-path $HOME/vla-models/openvla-7b \
  --robot widowx \
  --policy-setup widowx_bridge \
  --scene-name bridge_table_1_v1
```

**Remark**:
1. The choice for `policy-model` can be inferred from the source code [here](./simpler_env/main_inference.py),
while the choice for `env-name` can be inferred from the source codce [here](./simpler_env/__init__.py).