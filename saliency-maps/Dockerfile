FROM python:3.11-slim

WORKDIR /app

# System deps
RUN apt-get update && apt-get install -y \
    build-essential gcc g++ \
    && rm -rf /var/lib/apt/lists/*

# PyTorch CPU (installed first for Docker layer caching)
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir \
        torch==2.4.0 torchvision==0.19.0 \
        --index-url https://download.pytorch.org/whl/cpu

# Other dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy notebooks
COPY notebooks/ /app/notebooks/

EXPOSE 8890

# Configure Jupyter (no token, accessible from host)
RUN jupyter notebook --generate-config && \
    echo "c.NotebookApp.ip = '0.0.0.0'"          >> /root/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.open_browser = False"     >> /root/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.allow_root = True"        >> /root/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.token = ''"               >> /root/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.password = ''"            >> /root/.jupyter/jupyter_notebook_config.py

CMD ["jupyter", "notebook", \
     "--notebook-dir=/app/notebooks", \
     "--ip=0.0.0.0", "--port=8890", \
     "--no-browser", "--allow-root", \
     "--NotebookApp.token=''", "--NotebookApp.password=''"]
