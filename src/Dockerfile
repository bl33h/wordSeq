FROM python:3.8

# Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libsm6 \
    libxext6 \
    libxrender-dev \
    wget \
    && rm -rf /var/lib/apt/lists/*

# Create a working directory
WORKDIR /lab

# Install Python dependencies
RUN pip install -U --force-reinstall --no-cache https://github.com/johnhw/jhwutils/zipball/master
RUN pip install scikit-image
RUN pip install -U --force-reinstall --no-cache https://github.com/AlbertS789/lautils/zipball/master
RUN pip install notebook
RUN pip install datasets nltk
RUN pip install -U torch==1.9.0+cu111 -f https://download.pytorch.org/whl/cu111/torch_stable.html
RUN pip install -U torchtext==0.10.0
RUN pip install spacy

# Install spaCy models
RUN python -m spacy download de_core_news_sm
RUN python -m spacy download en_core_web_sm

RUN pip install --upgrade pip
RUN pip install ipywidgets

# Download and extract the dataset Multi30k
RUN wget -P /lab/datasets/Multi30k https://raw.githubusercontent.com/neychev/small_DL_repo/master/datasets/Multi30k/training.tar.gz
RUN wget -P /lab/datasets/Multi30k https://raw.githubusercontent.com/neychev/small_DL_repo/master/datasets/Multi30k/validation.tar.gz
RUN wget -P /lab/datasets/Multi30k https://raw.githubusercontent.com/neychev/small_DL_repo/master/datasets/Multi30k/mmt16_task1_test.tar.gz
RUN tar -xzf /lab/datasets/Multi30k/training.tar.gz -C /lab/datasets/Multi30k
RUN tar -xzf /lab/datasets/Multi30k/validation.tar.gz -C /lab/datasets/Multi30k
RUN tar -xzf /lab/datasets/Multi30k/mmt16_task1_test.tar.gz -C /lab/datasets/Multi30k

RUN mkdir -p /lab/datasets/Multi30k/multi30k
RUN mv /lab/datasets/Multi30k/._test.de /lab/datasets/Multi30k/multi30k/test2016.de
RUN mv /lab/datasets/Multi30k/._test.en /lab/datasets/Multi30k/multi30k/test2016.en
RUN ls /lab/datasets/Multi30k/multi30k

# Copy the notebook to the container
COPY . .

# Expose the port for Jupyter Notebook
EXPOSE 8811

# Command to run Jupyter Notebook and keep the container running
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8811", "--no-browser", "--allow-root"]