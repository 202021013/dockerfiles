ARG ARG_BUILD_FROM="entelecheia/devenv:latest"
FROM $ARG_BUILD_FROM

# install requirements
# (Optional) Makes the build much faster
RUN sudo pip install -U pip setuptools
RUN sudo pip install ninja
# Set TORCH_CUDA_ARCH_LIST if running and building on different GPU types
RUN pip install -v -U git+https://github.com/facebookresearch/xformers.git@main#egg=xformers
# (this can take dozens of minutes)

# set workdir to user home
ARG ARG_USERNAME="a1111"
ARG ARG_WORKSPACE_ROOT="/workspace"
ENV USERNAME $ARG_USERNAME
ENV WORKSPACE_ROOT $ARG_WORKSPACE_ROOT
RUN echo "USERNAME: $USERNAME from $ARG_USERNAME"
RUN echo "WORKSPACE_ROOT: $WORKSPACE_ROOT from $ARG_WORKSPACE_ROOT"

WORKDIR /home/$USERNAME
COPY ./.docker/scripts/ ./scripts/
RUN pip install -r ./scripts/requirements.txt

WORKDIR $WORKSPACE_ROOT
CMD ["zsh"]
