# = HOW TO USE ===============================

# BUILDING
# docker build -t rf-appium-server path/to/folder/Dockerfile-folder
# Or with test source form git (contents downloaded to /test folder)
# docker build -t rf-appium-server --build-arg TEST_SRC_PATH=https://github.com/repository_id/repository.git path/to/folder/Dockerfile-folder

# RUNNING CONTAINER
# # docker run --privileged -d -p 4723:4723 -v /dev/bus/usb:/dev/bus/usb --name container-appium rf-appium-server
# Or with local (test)src
# # docker run --privileged -d -p 4723:4723 -v /dev/bus/usb:/dev/bus/usb -v /path/to/your/test/folder:/testvolume/ --name container-appium rf-appium-server 

# RUNNING TESTS EXAMPLES
# docker exec -it container-appium robot /test/yourtest.robot 
# docker exec -it container-appium robot /testvolume/yourtest.robot

FROM appium/appium

LABEL Maintainer="Petri Sadinmäki <petri.sadinmaki@qubilea.fi>" 
LABEL description="Sets up an environment to test Android devices. \
It has Appium (server) with all it needs to work \
(java, android sdk and some general packages) \
and Robot Framework % AppiumLibrary to run tests"

#=====================
# Install Python and set timezone
#=====================
ENV TZ="Europe/Helsinki"
RUN apt-get -y update \
    && apt-get install -y build-essential python3.6 python3.6-dev python3-pip python3.6-venv git \
    && python3.6 -m pip install pip --upgrade \ 
    && apt-get clean autoclean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && echo "${TZ}" > /etc/timezone \
    && rm /etc/localtime

#=====================
# Install latest Robot Framework & AppiumLibrary
#=====================
RUN pip install --upgrade pip setuptools
RUN pip install robotframework
RUN pip install --upgrade robotframework-appiumlibrary

#=====================
# Download test source from git (--build-arg TEST_SRC_PATH is used)
#=====================
ARG TEST_SRC_PATH=no_git_src
RUN if [ "${TEST_SRC_PATH}" != "no_git_src" ]; then git clone ${TEST_SRC_PATH} /test; fi
