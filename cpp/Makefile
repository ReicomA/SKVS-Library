CC=gcc
CXX=g++ -fPIC -g
CXXFLAGS= -std=c++17 -pthread 

TEST_TARGET=test #test target

#library
LIB_NAME=libskvsclient.so
LIB_TARGET=libskvsclient.so.0.0.1
LIB_NONVER_TARGET=libskvsclient.so.0


#resource from skvs
PACKET_SRC=$(wildcard modules/packet/*.cpp)
SOCK_SRC=$(wildcard modules/SockWrapper/*.cpp)
STRUCTURE_SRC=$(wildcard modules/structure/*.cpp)
USER_SRC=$(wildcard modules/user/*.cpp)

#resource in lib
LIB_SRCS=SkvsConnection.cpp SkvsReadStream.cpp SkvsCommand.cpp SkvsConnection-RecvThread.cpp

#the object to make library
#SH_LIB_OBJS = $(wildcard modules/packet/*.o) $(wildcard modules/SockWrapper/*.o) $(wildcard modules/structure/*.o) $(wildcard modules/user/*.o) $(wildcard *.o)

TEST_SRC=test.cpp
SRCS=$(PACKET_SRC) $(SOCK_SRC) $(STRUCTURE_SRC) $(USER_SRC)
OBJS=$(SRCS:.cpp=.o)
LIB_OBJS=$(LIB_SRCS:.cpp=.o)
TEST_OBJ=$(TEST_SRC:.cpp=.o)

#make test to use library
test: 
	g++ -o test test.cpp -L./ -lskvsclient $(CXXFLAGS) 

#make lib + make link
lib: $(OBJS) $(LIB_OBJS)
	#g++ -fPIC -c $(SRCS) $(CXXFLAGS) 
	#g++ -fPIC -c $(LIB_SRCS) $(CXXFLAGS) 
	g++ -shared -o $(LIB_TARGET) $(OBJS) $(LIB_OBJS) $(CXXFLAGS)
	ln -s $(LIB_TARGET) $(LIB_NAME)
	ln -s $(LIB_TARGET) $(LIB_NONVER_TARGET)

clean_test:
	rm test
clean_obj:
	rm $(OBJS)
	rm $(LIB_OBJS)
clean_lib:
	rm $(LIB_TARGET)
	rm $(LIB_NAME)
	rm $(LIB_NONVER_TARGET)
