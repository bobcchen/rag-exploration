FROM nvidia/cuda:11.8.0-cudnn8-devel-ubuntu22.04
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN apt-get install -y python3.10
RUN apt-get install -y python3-pip

# TODO: cleaner way to build vllm image for cuda 11.8
# Compatibility matrix referenced from https://github.com/vllm-project/vllm/issues/2797

# Install vLLM with CUDA 11.8.
ENV VLLM_VERSION 0.2.6
ENV PYTHON_VERSION 310
RUN pip install https://github.com/vllm-project/vllm/releases/download/v${VLLM_VERSION}/vllm-${VLLM_VERSION}+cu118-cp${PYTHON_VERSION}-cp${PYTHON_VERSION}-manylinux1_x86_64.whl

# Re-install PyTorch with CUDA 11.8.
RUN pip uninstall torch -y
RUN pip install torch==2.1.2 --index-url https://download.pytorch.org/whl/cu118

# Re-install xFormers with CUDA 11.8.
RUN pip uninstall xformers -y
RUN pip install xformers==0.0.23.post1 --index-url https://download.pytorch.org/whl/cu118

EXPOSE 8080

ENTRYPOINT ["python3", "-m", "vllm.entrypoints.openai.api_server"]
