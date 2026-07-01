# Base Image
FROM python:3.12-slim

# Install Java + wget + curl
RUN apt-get update && \
    apt-get install -y \
    openjdk-21-jdk \
    wget \
    curl && \
    rm -rf /var/lib/apt/lists/*

# Download Spark
RUN wget https://archive.apache.org/dist/spark/spark-3.5.6/spark-3.5.6-bin-hadoop3.tgz && \
    tar -xzf spark-3.5.6-bin-hadoop3.tgz -C /opt && \
    rm spark-3.5.6-bin-hadoop3.tgz

# JAVA_HOME
ENV JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64
ENV PATH="$JAVA_HOME/bin:${PATH}"

# Spark Version
ENV SPARK_VERSION=3.5.6

# Spark Home
ENV SPARK_HOME=/opt/spark-3.5.6-bin-hadoop3
ENV PATH=$SPARK_HOME/bin:$PATH

# Working Directory
WORKDIR /workspace

# Python Requirements
COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

# Jupyter Port
EXPOSE 8080

# Start JupyterLab
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8080", "--no-browser", "--allow-root"]