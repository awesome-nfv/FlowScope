CMAKE_MINIMUM_REQUIRED(VERSION 2.8.10)

IF(CMAKE_CXX_COMPILER_VERSION VERSION_LESS 5.0)
	MESSAGE(FATAL_ERROR "FlowScope requires gcc 5 or newer.")
ENDIF()

SET(CMAKE_CXX_FLAGS "-fno-stack-protector -Wall -Wextra -Wno-unused-parameter -Wno-unused-variable -Wno-unused-function -g -O3 -std=gnu++11 -march=native")
SET(CMAKE_C_FLAGS "-fno-stack-protector -Wall -Wextra -Wno-unused-parameter -Wno-unused-variable -Wno-unused-function -g -O3 -std=gnu11 -march=native")

SET(PRJ qq)

SET(QQ_SRC src/qq_wrapper.cpp)

SET(LIBMOON_DIR ${CMAKE_CURRENT_SOURCE_DIR}/libmoon)

INCLUDE_DIRECTORIES(
	${CMAKE_CURRENT_SOURCE_DIR}/src
	${LIBMOON_DIR}/deps/dpdk/x86_64-native-linuxapp-gcc/include
	${LIBMOON_DIR}/deps/luajit/src
	${LIBMOON_DIR}/lib
	${LIBMOON_DIR}/src
)

ADD_DEFINITIONS(-DNDEBUG)
ADD_LIBRARY(${PRJ} SHARED ${QQ_SRC})

SET(SIGUSR_SRC src/signal.cpp)
ADD_LIBRARY(sigusr SHARED ${SIGUSR_SRC})

