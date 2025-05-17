FROM python:3.10-slim

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        git \
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
RUN git clone https://github.com/kunaldahiya/prime.git


CMD ["-c", "print('Usage: python <script.py> [args]')"]
