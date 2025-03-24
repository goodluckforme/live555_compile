PREFIX = /usr/local
INCLUDES = -I../UsageEnvironment/include -I../groupsock/include -I../liveMedia/include -I../BasicUsageEnvironment/include
# Default library filename suffixes for each library that we link with.  The "config.*" file might redefine these later.
libliveMedia_LIB_SUFFIX = $(LIB_SUFFIX)
libBasicUsageEnvironment_LIB_SUFFIX = $(LIB_SUFFIX)
libUsageEnvironment_LIB_SUFFIX = $(LIB_SUFFIX)
libgroupsock_LIB_SUFFIX = $(LIB_SUFFIX)
##### Change the following for your environment:
NDK=/home/maqi/Android/android-ndk-r26b
TOOLCHAIN=$(NDK)/toolchains/llvm/prebuilt/linux-x86_64
API=21
SYSROOT=$(TOOLCHAIN)/sysroot
CROSS_PREFIX=$(TOOLCHAIN)/bin/aarch64-linux-android-
DESTDIR=$(shell pwd)/../arm64-v8a/lib

COMPILE_OPTS =         $(INCLUDES) -m64  -fPIC -fpic -I$(SYSROOT)/usr/local/include -I. -O2 -DSOCKLEN_T=socklen_t -D_LARGEFILE_SOURCE=1 -D_FILE_OFFSET_BITS=64 -DNO_OPENSSL=1 -DNO_GETIFADDRS=1 --sysroot=$(SYSROOT)
C =                     c
C_COMPILER =            $(TOOLCHAIN)/bin/aarch64-linux-android$(API)-clang
C_FLAGS =               $(COMPILE_OPTS)
CPP =                   cpp
CPLUSPLUS_COMPILER =    $(TOOLCHAIN)/bin/aarch64-linux-android$(API)-clang++
CPLUSPLUS_FLAGS =       $(COMPILE_OPTS) -Wall -DBSD=1
OBJ =                   o
LINK =                  $(CPLUSPLUS_COMPILER) -o 
LINK_OPTS =             -static-libstdc++
CONSOLE_LINK_OPTS =     $(LINK_OPTS)
LIBRARY_LINK =          $(CPLUSPLUS_COMPILER) -shared -o
LIBRARY_LINK_OPTS =		-Wl,-soname,$(NAME).so -static-libstdc++
LIB_SUFFIX =            so
LIBS_FOR_CONSOLE_APPLICATION =  
LIBS_FOR_GUI_APPLICATION =
EXE =
#INSTALL2 =		install_shared_libraries

HLS_PROXY = live555HLSProxy$(EXE)

ALL = $(HLS_PROXY)
all: $(ALL)

.$(C).$(OBJ):
	$(C_COMPILER) -c $(C_FLAGS) $<
.$(CPP).$(OBJ):
	$(CPLUSPLUS_COMPILER) -c $(CPLUSPLUS_FLAGS) $<

HLS_PROXY_OBJS = live555HLSProxy.$(OBJ)

USAGE_ENVIRONMENT_DIR = ../UsageEnvironment
USAGE_ENVIRONMENT_LIB = $(USAGE_ENVIRONMENT_DIR)/libUsageEnvironment.$(libUsageEnvironment_LIB_SUFFIX)
BASIC_USAGE_ENVIRONMENT_DIR = ../BasicUsageEnvironment
BASIC_USAGE_ENVIRONMENT_LIB = $(BASIC_USAGE_ENVIRONMENT_DIR)/libBasicUsageEnvironment.$(libBasicUsageEnvironment_LIB_SUFFIX)
LIVEMEDIA_DIR = ../liveMedia
LIVEMEDIA_LIB = $(LIVEMEDIA_DIR)/libliveMedia.$(libliveMedia_LIB_SUFFIX)
GROUPSOCK_DIR = ../groupsock
GROUPSOCK_LIB = $(GROUPSOCK_DIR)/libgroupsock.$(libgroupsock_LIB_SUFFIX)
LOCAL_LIBS =	$(LIVEMEDIA_LIB) $(GROUPSOCK_LIB) \
		$(BASIC_USAGE_ENVIRONMENT_LIB) $(USAGE_ENVIRONMENT_LIB)
LIBS =			$(LOCAL_LIBS) $(LIBS_FOR_CONSOLE_APPLICATION)

live555HLSProxy$(EXE):	$(HLS_PROXY_OBJS) $(LOCAL_LIBS)
	$(LINK)$@ $(CONSOLE_LINK_OPTS) $(HLS_PROXY_OBJS) $(LIBS)

clean:
	-rm -rf *.$(OBJ) $(ALL) core *.core *~ include/*~

install: $(HLS_PROXY)
	  install -d $(DESTDIR)$(PREFIX)/bin
	  install -m 755 $(HLS_PROXY) $(DESTDIR)$(PREFIX)/bin

##### Any additional, platform-specific rules come here:
