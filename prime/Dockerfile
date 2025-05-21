# FROM python:3.10-slim
FROM nvidia/cuda:12.1.0-base-ubuntu22.04

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        git \
        unzip \
        python3 \
        python3-pip \
        python3-dev \
        build-essential && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY requirements.txt .
RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

# Install deps for PRIME (NAACL'25)
RUN git clone https://github.com/kunaldahiya/pyxclib.git && \
    cd pyxclib && \
    pip install -e .
RUN git clone https://github.com/kunaldahiya/deepxml-base.git && \
    cd deepxml-base && \
    pip install -e .

RUN mkdir -p Workspace

RUN mkdir -p Workspace/programs
RUN cd Workspace/programs && \
    git clone https://github.com/kunaldahiya/prime.git

RUN pip install gdown
RUN mkdir -p Workspace/data

RUN gdown 1WuquxCAg8D4lKr-eZXPv4nNw2S2lm7_E -O Workspace/data/LF-AmazonTitles-131K.raw.zip
RUN cd Workspace/data && \
    unzip LF-AmazonTitles-131K.raw.zip && \
    mv LF-Amazon-131K LF-AmazonTitles-131K

CMD ["-c", "print('Usage: python <script.py> [args]')"]
