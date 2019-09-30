#=================================================================================
#
# Create a docker image for ESMValTool that can be used in combination with
# the Nird Toolkit application : jupyter notebook
#
#=================================================================================
# Create a docker image based on a uninett base image
# See the value of dockerImage in
#
#   https://github.com/Uninett/helm-charts/blob/master/repos/stable/jupyter/values.yaml
#   https://quay.io/repository/uninett/jupyter-spark?tab=tags
#   
# to determine the latest base image
#=================================================================================

FROM quay.io/uninett/jupyter-spark:20190815-ea0ec80

LABEL authors="Tomas Torsvik"
LABEL maintainer="tomas.torsvik@uib.no"

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

#=================================================================================
# ESMValTool depends on Julia. (This is not very clean, can probably be improved)
# Based on:
#   https://github.com/jupyter/docker-stacks/blob/master/datascience-notebook/Dockerfile#L22
#=================================================================================

## USER root
## 
## # Julia dependencies
## # install Julia packages in /opt/julia instead of $HOME
## ENV JULIA_DEPOT_PATH=/opt/julia
## ENV JULIA_PKGDIR=/opt/julia
## ENV JULIA_VERSION=1.2.0
## 
## RUN mkdir /opt/julia-${JULIA_VERSION} && \
##     cd /tmp && \
##     wget -q https://julialang-s3.julialang.org/bin/linux/x64/`echo ${JULIA_VERSION} | cut -d. -f 1,2`/julia-${JULIA_VERSION}-linux-x86_64.tar.gz && \
##     echo "926ced5dec5d726ed0d2919e849ff084a320882fb67ab048385849f9483afc47 *julia-${JULIA_VERSION}-linux-x86_64.tar.gz" | sha256sum -c - && \
##     tar xzf julia-${JULIA_VERSION}-linux-x86_64.tar.gz -C /opt/julia-${JULIA_VERSION} --strip-components=1 && \
##     rm /tmp/julia-${JULIA_VERSION}-linux-x86_64.tar.gz
## RUN ln -fs /opt/julia-*/bin/julia /usr/local/bin/julia
## 
## # Show Julia where conda libraries are \
## RUN mkdir /etc/julia && \
##     echo "push!(Libdl.DL_LOAD_PATH, \"$CONDA_DIR/lib\")" >> /etc/julia/juliarc.jl && \
##     # Create JULIA_PKGDIR \
##     mkdir $JULIA_PKGDIR && \
##     chown $NB_USER $JULIA_PKGDIR && \
##     fix-permissions $JULIA_PKGDIR

#=================================================================================
# Install ESMValTool
# Based on:
#  https://github.com/ESMValGroup/ESMValTool/blob/version2_development/docker/Dockerfile 
#=================================================================================

## # install development tools
## USER root
## RUN apt-get update -y && apt-get install -y \
##     build-essential \
##     curl \
##     unzip
 
# update the conda packages
USER notebook
RUN conda update -y conda pip

# install environment packages
RUN conda env update --file environment.yml

### run tests
##RUN esmvaltool -h
##
##ENTRYPOINT ["esmvaltool"]
##CMD ["-h"]