CUDA_CFLAGS := $(shell pkg-config --cflags cudart-6.5 cublas-6.5 cufft-6.5 nppc-6.5 nppi-6.5 npps-6.5)
CUDA_LIBS := $(shell pkg-config --libs cudart-6.5 cublas-6.5 cufft-6.5 nppc-6.5 nppi-6.5 npps-6.5)

CUDA_LIB_PATH := $(subst -L,,$(shell pkg-config --libs-only-L cudart-6.5))
CUDA_LIBS += -Wl,-rpath=$(CUDA_LIB_PATH)

OPENCV_CFLAGS := $(shell pkg-config --cflags opencv)
OPENCV_LIBS := $(shell pkg-config --libs opencv)

all: stitching

stitching: main.o stitching.o blender.o
	$(CXX) $(LDFLAGS) main.o stitching.o blender.o $(OPENCV_LIBS) $(CUDA_LIBS) -o stitching

main.o: main.cpp
	$(CXX) $(CXX_FLAGS) $(OPENCV_CFLAGS) $(CUDA_CFLAGS) -o main.o -c main.cpp

blender.o: blender.cpp
	$(CXX) $(CXX_FLAGS) $(OPENCV_CFLAGS) $(CUDA_CFLAGS) -o blender.o -c blender.cpp

stitching.o: stitching.cpp
	$(CXX) $(CXX_FLAGS) $(OPENCV_CFLAGS) $(CUDA_CFLAGS) -o stitching.o -c stitching.cpp

clean:
	rm -f main.o blender.o stitching.o
	rm -f stitching
