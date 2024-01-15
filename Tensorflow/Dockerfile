FROM tensorflow:latest-gpu-jupyter

# Install requirements
COPY requirements.txt .
RUN pip install -r requirements.txt

WORKDIR /tf

EXPOSE map[8888/tcp:{}]

CMD ["bash" "-c" "source /etc/bash.bashrc && jupyter notebook --notebook-dir=/tf --ip 0.0.0.0 --no-browser --allow-root"]
