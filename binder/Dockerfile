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


# RUN wget http://security.ubuntu.com/ubuntu/pool/main/libg/libgd2/libgd-dbg_2.1.1-4ubuntu0.16.04.11_amd64.deb
# RUN dpkg -i libgd-dbg_2.1.1-4ubuntu0.16.04.11_amd64.deb
# RUN wget http://security.ubuntu.com/ubuntu/pool/main/t/tiff/libtiffxx5_4.0.6-1ubuntu0.6_amd64.deb

#RUN sudo sed -i -e 's/archive.ubuntu.com\|security.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list
RUN apt-get update
RUN apt-get install --yes graphviz

COPY . ${HOME}

USER root
RUN chown -R ${NB_UID} ${HOME}
RUN mkdir -p /tmp/share/beakerx/maven/cache
RUN chown -R ${NB_UID} '/tmp/share/beakerx/'

RUN chown -R beakerx:beakerx  /tmp/share/beakerx/ /opt/conda/envs/beakerx

# go back to the standard user
USER $NB_USER
