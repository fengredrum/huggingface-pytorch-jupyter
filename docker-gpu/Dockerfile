FROM huggingface/transformers-pytorch-gpu

# Install dependencies
COPY requirements.txt /
RUN pip3 install --no-cache-dir --upgrade pip && \
    pip3 install --no-cache-dir -r /requirements.txt

# Create a demo user
RUN apt update -y && apt install --no-install-recommends -y sudo
RUN adduser --disabled-password --gecos '' demo && \
    adduser demo sudo && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers && chown demo .
ENV PATH=/home/demo/.local/bin:$PATH

# Clear cache
RUN apt clean && \
    apt autoclean && \
    apt-get clean && \
    apt-get autoclean && \
    rm -rf /var/cache/* && \
    rm -rf /tmp/* && \
    rm -rf /var/tmp/* && \
    rm -rf /var/lib/apt/lists/*

USER demo

# Setup PEP8 for Jupyter Notebook
RUN jupyter contrib nbextension install --user

# Setup jupyter notebook and streamlit
RUN jt -t oceans16 -f fira -tf ptmono -ofs 10 -nfs 13 -tfs 13 -fs 12 -T -N -lineh 140 -cellw 90%
ENV LC_ALL=C.UTF-8 LANG=C.UTF-8

CMD /bin/bash