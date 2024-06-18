FROM jupyter/pyspark-notebook

USER root

# Set working directory
WORKDIR /home/jovyan/work

# Copy files
COPY  . .

# Install Minio and other dependencies
RUN pip install --no-cache-dir minio selenium beautifulsoup4

# Install Conda and additional Python libraries
RUN conda install -c conda-forge -y \
    pandas \
    numpy \
    matplotlib \
    scikit-learn

# Install Firefox
RUN apt-get update && \
    apt-get install -y curl wget && \
    wget -O firefox.tar.bz2 "https://download.mozilla.org/?product=firefox-latest&os=linux64" && \
    tar xjf firefox.tar.bz2 -C /opt/ && \
    ln -s /opt/firefox/firefox /usr/bin/firefox && \
    rm firefox.tar.bz2

# Install Geckodriver for Selenium
RUN curl -L https://github.com/mozilla/geckodriver/releases/download/v0.30.0/geckodriver-v0.30.0-linux64.tar.gz | tar -xz -C /usr/local/bin/

# Expose port for JupyterLab
EXPOSE 8888

# Start JupyterLab
CMD ["start.sh", "jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]
