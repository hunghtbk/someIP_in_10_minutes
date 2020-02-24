cmake_minimum_required(VERSION 2.8)
 
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread -std=c++0x")
 
include_directories(
     ./src-gen
     ../someip/capicxx-core-runtime/include
     ../someip/capicxx-someip-runtime/include
     ../someip/vSomeIP/interface
)
 
link_directories(
     ../someip/capicxx-core-runtime/build
     ../someip/capicxx-someip-runtime/build
     ../someip/vSomeIP/build
)
 
add_executable(HelloWorldClient
    ./src/HelloWorldClient.cpp
    ./src-gen/v1/commonapi/HelloWorldSomeIPProxy.cpp
    ./src-gen/v1/commonapi/HelloWorldSomeIPDeployment.cpp
)
target_link_libraries(HelloWorldClient CommonAPI CommonAPI-SomeIP vsomeip)
 
add_executable(HelloWorldService
    ./src/HelloWorldService.cpp
    ./src/HelloWorldStubImpl.cpp
    ./src-gen/v1/commonapi/HelloWorldSomeIPStubAdapter.cpp
    ./src-gen/v1/commonapi/HelloWorldStubDefault.cpp
    ./src-gen/v1/commonapi/HelloWorldSomeIPDeployment.cpp
)
target_link_libraries(HelloWorldService CommonAPI CommonAPI-SomeIP vsomeip)
