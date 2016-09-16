badsed on Ethminer-0.9.41-genoil-1.1.7

For GTX970 : 
cmake -DBUNDLE=cudaminer -DCOMPUTE=52 .. 

I have nowhere else to keep this .. 
IF you get protocol errors and a seg fault STOP THE WINDOW MANAGER ( on wily delete LIGHTDM in init.d ) 
don't install : 
 ocl-icd-libopencl1 opencl-headers ( REMOVE THEM ifthey are installed )  
 any of the qtweb stuff - this doesn't have a gui so no need for qt
 libgmp-dev no need to manipulate gmp files
 

WILY DEPS
apt-get install libjsoncpp-dev libjsonrpccpp-tools  libjsonrpccpp-dev libjsonrpccpp-stub0 build-essential git cmake libboost-all-dev  libleveldb-dev libminiupnpc-dev libreadline-dev libncurses5-dev libcurl4-openssl-dev libcrypto++-dev libmicrohttpd-dev libargtable2-dev libedit-dev libv8-dev zlib1g-dev

build-essential git python curl scons cmake libboost-all-dev automake unzip libgmp-dev libgmp3-dev libtool libleveldb-dev yasm libminiupnpc-dev libreadline-dev libncurses5-dev libcurl4-openssl-dev wget libjsoncpp-dev libargtable2-dev libmicrohttpd-dev libedit-dev mesa-common-dev ocl-icd-libopencl1 opencl-headers libgoogle-perftools-dev ocl-icd-dev libv8-dev binfmt-support libffi-dev libobjc-4.9-dev libobjc4 libjsonrpccpp-dev libjsonrpccpp-tools

Install the AMD SDK into /opt it will pick it up 

-------------
# Install "normal packages"
                sudo apt-get -y update
                sudo apt-get -y install \
                    build-essential \
                    cmake \
                    g++ \
                    gcc \
                    git \
                    libboost-all-dev \
                    libcurl4-openssl-dev \
                    libgmp-dev \
                    libjsoncpp-dev \
                    libleveldb-dev \
                    libmicrohttpd-dev \
                    libminiupnpc-dev \
                    libz-dev \
                    mesa-common-dev \
                    ocl-icd-libopencl1 \
                    opencl-headers \
                    unzip

                # All the Debian releases until Stretch have shipped with CryptoPP 5.6.1,
                # but we need 5.6.2 or newer, so we build it from source.
                #
                # - https://packages.debian.org/wheezy/libcrypto++-dev (5.6.1)
                # - https://packages.debian.org/jessie/libcrypto++-dev (5.6.1)
                # - https://packages.debian.org/stretch/libcrypto++-dev (5.6.3)

                mkdir cryptopp && cd cryptopp
                wget https://www.cryptopp.com/cryptopp563.zip
                unzip -a cryptopp563.zip
                make dynamic
                make libcryptopp.so
                sudo make install PREFIX=/usr/local
                cd ..

                # All the Debian releases until Stretch have shipped with versions of CMake
                # which are too old for cpp-ethereum to build successfully.  CMake v3.0.x
                # should be the minimum version, but the v3.0.2 which comes with Jessie
                # doesn't work properly, so maybe our minimum version should actually be
                # CMake v3.1.x?  Anyway - we just build and install CMake from source
                # here, so that it works on any distro.
                #
                # - https://packages.debian.org/wheezy/cmake (2.8.9)
                # - https://packages.debian.org/jessie/cmake (3.0.2)
                # - https://packages.debian.org/stretch/cmake (3.5.2)

                wget https://cmake.org/files/v3.5/cmake-3.5.2.tar.gz
                tar -xf cmake-3.5.2.tar.gz
                cd cmake-3.5.2/
                cmake .
                ./bootstrap --prefix=/usr
                make -j 2
                sudo make install
                source ~/.profile
                cd ..
                rm -rf cmake-3.5.2
                rm cmake-3.5.2.tar.gz

                # Build libjsonrpccpp-v0.6.0 from source.
                # Rationale for this is given in the Ubuntu comments lower down this file.

                sudo apt-get -y install libargtable2-dev libedit-dev
                git clone git://github.com/cinemast/libjson-rpc-cpp.git
                cd libjson-rpc-cpp
                git checkout v0.6.0
                mkdir build
                cd build
                cmake .. -DCOMPILE_TESTS=NO
                make
                sudo make install
                sudo ldconfig
                cd ../..
                
                
