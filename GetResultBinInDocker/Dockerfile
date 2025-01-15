# Use the official Ubuntu 22.04 base image
FROM ubuntu:22.04

# Set the working directory inside the container
WORKDIR /usr/src/app

# Install necessary dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    autoconf \
    cmake \
    git \
    g++ \
    make \
    libboost-all-dev

# Clone rapidcsv repository
#WORKDIR /usr/src/app
#RUN git clone https://github.com/d99kris/rapidcsv.git

# Clone the OpenFHE official repository
RUN git clone https://github.com/openfheorg/openfhe-development.git

# Build and install OpenFHE
WORKDIR /usr/src/app/openfhe-development
RUN mkdir build && cd build && cmake .. && make && make install && git checkout tags/v1.1.2

# Set the library path
ENV LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

# Command to run the compiled binary (replace 'your_binary_name' with the actual binary name)
ENV TERM xterm-256color
RUN echo 'export PS1="\[\e[36m\](docker@\h) \[\e[1;33m\][\[\e[38;5;130m\]\$(date +%H:%M:%S)\[\e[38;5;167m\] \u:\[\e[38;5;228m\] \w\[\e[1;33m\]]\[\e[m\]\n$ "' > /root/.bashrc

# Get and update the CMakeLists file from the library before compilation
WORKDIR /bdt
RUN cp /usr/src/app/openfhe-development/CMakeLists.User.txt ./CMakeLists.txt
#RUN echo "include_directories(/usr/src/app/rapidcsv)" >> CMakeLists.txt
RUN echo "add_executable(encrypt-medical-getresult encrypt-medical-getresult.cpp)" >> CMakeLists.txt

# Add all context files and directories before running
ADD . .

#WORKDIR /bdt/build
#RUN cmake .. && make
#RUN ./bdt-hom-eval 3


CMD ["bash", "-l"] 





