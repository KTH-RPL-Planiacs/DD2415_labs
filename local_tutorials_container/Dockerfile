# Use a base image with Python and standard tools
FROM ubuntu:22.04

# Set up environment variables to avoid interactive prompts
ENV DEBIAN_FRONTEND=noninteractive
ENV PYTHONUNBUFFERED 1
ENV LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

# Install necessary system packages
RUN apt-get update && \
    apt-get install -y \
    python3 \
    python3-pip \
    wget \
    make \
    gcc \
    g++ \
    unzip \
    graphviz \
    libxml2-dev \
    && rm -rf /var/lib/apt/lists/*

# Install Python packages
RUN pip install notebook networkx numpy pandas sympy shapely matplotlib

# --- Install BuDDy (for ltl3ba) ---
WORKDIR /tmp
RUN wget https://downloads.sourceforge.net/project/buddy/buddy/BuDDy%202.4/buddy-2.4.tar.gz && \
    tar xzf buddy-2.4.tar.gz && \
    rm buddy-2.4.tar.gz

WORKDIR /tmp/buddy-2.4
RUN ./configure --prefix=/usr/local && \
    make && \
    make install

# --- Install ltl3ba ---
WORKDIR /tmp
RUN wget http://downloads.sourceforge.net/project/ltl3ba/ltl3ba/1.1/ltl3ba-1.1.3.tar.gz && \
    tar xzf ltl3ba-1.1.3.tar.gz && \
    rm ltl3ba-1.1.3.tar.gz

WORKDIR /tmp/ltl3ba-1.1.3
# Patch Makefile to use local BuDDy installation
RUN sed -i '36s#.*#BUDDY_INCLUDE=/usr/local/include#' Makefile && \
    sed -i '38s#.*#BUDDY_LIB=/usr/local/lib#' Makefile && \
    make
# Move executable to a PATH directory
RUN mv ltl3ba /usr/local/bin/

# --- Install Triangle ---
WORKDIR /tmp
RUN wget https://netlib.org/voronoi/triangle.zip && \
    unzip triangle.zip -d triangle && \
    rm triangle.zip

WORKDIR /tmp/triangle
# Run `make triangle` instead of just `make` to compile only the core executable, 
# bypassing the compilation of the optional 'showme' utility which requires X11 libs.
RUN make triangle
# Move executable to a PATH directory
RUN mv triangle /usr/local/bin/

# Set the working directory for the lab notebook
WORKDIR /usr/src/app

# The user needs to mount the notebook into this directory,
# so we only expose the port for Jupyter.
EXPOSE 8888

# Command to run Jupyter Notebook. The user will override this in VS Code or CLI.
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]