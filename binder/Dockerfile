# Set the base image to beakerx
FROM beakerx/beakerx:latest

# it's better to be root as this Dockerfile will try to update conda etc.
USER root

# that's important to make sure the pip of the beakerx environment is in the path
ENV PATH /opt/conda/envs/beakerx/bin:$PATH

# copy the config file
COPY jupyter_notebook_config.py /etc/jupyter/jupyter_notebook_config.py

# update pip
RUN pip install --no-cache-dir --upgrade pip

# install rise and cvxpy
RUN conda install -y -n beakerx -c conda-forge rise=5.4.1 cvxpy=1.0.14 && conda clean -y --all

COPY . ${HOME}
USER root
RUN chown -R ${NB_UID} ${HOME}

# go back to the standard user
USER $NB_USER
