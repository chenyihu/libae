project(ae)
cmake_minimum_required(VERSION 2.8)

option(HAVE_KQUEUE "use kqueue" OFF)
option(HAVE_EPOLL "use epoll" OFF)
option(HAVE_EVPORT "use evport" OFF)
option(HAVE_SELECT "use select" OFF)

set(SOURCE_FILES ae.h ae.c)

if(HAVE_KQUEUE) 
  set(AE_SOURCE_FILES ae_kqueue.c)
elseif(HAVE_EPOLL)
  set(AE_SOURCE_FILES ae_epoll.c)
elseif(HAVE_EVPORT)
  set(AE_SOURCE_FILES ae_evport.c)
else(HAVE_KQUEUE)
  set(AE_SOURCE_FILES ae_select.c)
endif(HAVE_KQUEUE)

add_library(${PROJECT_NAME} STATIC ${SOURCE_FILES} ${AE_SOURCE_FILES})
