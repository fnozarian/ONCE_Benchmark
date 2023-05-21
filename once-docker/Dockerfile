FROM nvcr.io/nvidia/pytorch:20.10-py3

RUN apt-get update -y

WORKDIR /opt

RUN git clone -b v1.2.1 https://github.com/traveller59/spconv.git --recursive \
    && cd spconv \
    && sed -i 's/PYTORCH_VERSION = list(map(int, PYTORCH_VERSION.split(".")))/PYTORCH_VERSION = [1, 7, 0]/g' setup.py \ 
    && python setup.py bdist_wheel \
    && pip install dist/spconv-1.2.1*

WORKDIR /opt

RUN git clone https://github.com/danish87/ONCE_Benchmark \
    && cd ONCE_Benchmark/ \
    && pip install tensorboardX easydict pyyaml scikit-image tqdm numba torchmetrics \
    && python setup.py develop \
    && cd pcdet/ops/dcn \
    && python setup.py develop

WORKDIR /opt/ONCE_Benchmark/tools/
