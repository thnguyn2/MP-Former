## Installation

### Requirements
- Linux or macOS with Python ≥ 3.6
- PyTorch ≥ 1.9 and [torchvision](https://github.com/pytorch/vision/) that matches the PyTorch installation.
  Install them together at [pytorch.org](https://pytorch.org) to make sure of this. Note, please check
  PyTorch version matches that is required by Detectron2.
- Detectron2: follow [Detectron2 installation instructions](https://detectron2.readthedocs.io/tutorials/install.html).
- OpenCV is optional but needed by demo and visualization
- `pip install -r requirements.txt`

### CUDA kernel for MSDeformAttn
After preparing the required environment, run the following command to compile CUDA kernel for MSDeformAttn:

`CUDA_HOME` must be defined and points to the directory of the installed CUDA toolkit.

```bash
cd mask2former/modeling/pixel_decoder/ops
sh make.sh
```

#### Building on another system
To build on a system that does not have a GPU device but provide the drivers:
```bash
TORCH_CUDA_ARCH_LIST='8.0' FORCE_CUDA=1 python setup.py build install
```

### Example conda environment setup
```bash
conda create --name mask2former python=3.8 -y
conda activate mask2former
conda install pytorch==1.9.0 torchvision==0.10.0 cudatoolkit=11.1 -c pytorch -c nvidia
pip install -U opencv-python

# under your working directory
git clone git@github.com:facebookresearch/detectron2.git
cd detectron2
pip install -e .
pip install git+https://github.com/cocodataset/panopticapi.git
pip install git+https://github.com/mcordts/cityscapesScripts.git

cd ..
git clone git@github.com:facebookresearch/Mask2Former.git
cd Mask2Former
pip install -r requirements.txt
cd mask2former/modeling/pixel_decoder/ops
sh make.sh
```

### Installation procedure for PathAI cluster
- Initialize a 2 GPU pod using the `fm-dev` image
- conda create --name mpformer python=3.10 -y
- conda activate mpformer
- pip install -r requirements.txt
- conda install cudatoolkit=11.7 -c pytorch
- pip install https://download.pytorch.org/whl/cu117/torch-2.0.1%2Bcu117-cp310-cp310-linux_x86_64.whl
- pip install https://download.pytorch.org/whl/cu117/torchvision-0.15.2%2Bcu117-cp310-cp310-linux_x86_64.whl#sha256=1ee57f2bee878ad8574ea559bb7172c1cfaad168634fa738479e1fe3bdd7eaca
- conda install -c conda-forge cudatoolkit-dev 
- pip install -U opencv-python

# Install Detectron2
- pip install setuptools==69.5.1  
- cd into the `detection2` folder
- pip install -e .
- pip install git+https://github.com/cocodataset/panopticapi.git
- pip install git+https://github.com/mcordts/cityscapesScripts.git

# Install mmcv-full
- pip install -f https://download.openmmlab.com/mmcv/dist/cu117/torch1.9.0/index.html mmcv-full==1.3.17

# Compile script for the pixel decoder.
- pip install ninja
- cd mask2former
- cd mask2former/modeling/pixel_decoder/ops
- sh make.sh
