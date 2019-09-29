# The image to use as a base image
# See the value of dockerImage in
#
#   https://github.com/Uninett/helm-charts/blob/master/repos/stable/jupyter/values.yaml
#
# to determine the latest base image

FROM quay.io/uninett/jupyter-spark:20190815-ea0ec80

# Install system packages
USER root
RUN apt update && apt install -y vim

# Install other packages
USER notebook
RUN pip install scikit-learn

