FROM tensorflow/tensorflow:latest-gpu-jupyter

# Install requirements
COPY requirements.txt .
RUN pip install -r requirements.txt

RUN apt-get update && apt-get install -y bc

WORKDIR /tf

CMD ["/bin/bash", "-c", "source /etc/bash.bashrc && jupyter notebook --notebook-dir=/tf --ip 0.0.0.0 --no-browser --allow-root"]
# CMD ["/bin/bash", "-c", "source /etc/bash.bashrc && jupyter notebook --notebook-dir=/tf --ip 0.0.0.0 --NotebookApp.token='' --NotebookApp.password='' --no-browser --allow-root"]
