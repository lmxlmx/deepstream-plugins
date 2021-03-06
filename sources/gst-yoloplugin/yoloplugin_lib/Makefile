# MIT License

# Copyright (c) 2018 NVIDIA CORPORATION. All rights reserved.

# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:

# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.

# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.


SRCS:= $(wildcard *.cpp)
BUILD_PATH:= ./build/
OBJS= $(patsubst %, $(BUILD_PATH)%, $(SRCS:.cpp=.o))
TARGET:= libyoloplugin.a
INCS:= -I"$(TENSORRT_INSTALL_DIR)/include" -I"/usr/local/cuda-$(CUDA_VER)/include"
LIBS:= -L"$(TENSORRT_INSTALL_DIR)/lib" -lnvinfer -lnvinfer_plugin \
	   -L"/usr/local/cuda-$(CUDA_VER)/lib64" -lcudart -lcublas -lcurand 
CXXFLAGS:= -std=c++11 -lstdc++fs -fPIC -Wall -Wunused-function -Wunused-variable `pkg-config --cflags glib-2.0` 

all: dir $(SRCS) $(OBJS)
	ar rcs $(TARGET) $(OBJS)

dir:	
	if [ ! -d "models" ]; then mkdir -p models; fi
	if [ ! -d "calibration" ]; then mkdir -p calibration; fi
	if [ ! -d "build" ]; then mkdir -p build; fi

$(BUILD_PATH)%.o: %.cpp
	$(CXX) $(INCS) -c -o $@ $(CXXFLAGS) $<

clean: 
	rm -f ./build/*
	rm -f ./*.a