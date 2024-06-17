FROM jupyter/pyspark-notebook:latest

# Set working directory
WORKDIR /home/jovyan/work

# Install Minio and other dependencies
RUN pip install --no-cache-dir minio selenium beautifulsoup4

# Install Conda and additional Python libraries
RUN conda install -c conda-forge -y \
    pandas \
    numpy \
    matplotlib \
    scikit-learn

# Install Firefox and Geckodriver for Selenium
RUN apt-get update && \
    apt-get install -y firefox-esr && \
    apt-get install -y wget && \
    wget https://github.com/mozilla/geckodriver/releases/download/v0.30.0/geckodriver-v0.30.0-linux64.tar.gz && \
    tar -xvzf geckodriver-v0.30.0-linux64.tar.gz && \
    mv geckodriver /usr/local/bin/

# Expose ports (JupyterLab)
EXPOSE 8888

# Start JupyterLab
CMD ["start.sh", "jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]
