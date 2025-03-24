INCLUDES = -Iinclude -I../UsageEnvironment/include
PREFIX = /usr/local
LIBDIR = $(PREFIX)/lib
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
LIBRARY_LINK =          $(CPLUSPLUS_COMPILER) -shared -o
LIBRARY_LINK_OPTS =		-Wl,-soname,$(NAME).so -static-libstdc++
LIB_SUFFIX =            so
LIBS_FOR_CONSOLE_APPLICATION =  
LIBS_FOR_GUI_APPLICATION =
EXE =
#INSTALL2 =		install_shared_libraries

NAME = libgroupsock
ALL = $(NAME).$(LIB_SUFFIX)
all:	$(ALL)

.$(C).$(OBJ):
	$(C_COMPILER) -c $(C_FLAGS) $<
.$(CPP).$(OBJ):
	$(CPLUSPLUS_COMPILER) -c $(CPLUSPLUS_FLAGS) $<

GROUPSOCK_LIB_OBJS = GroupsockHelper.$(OBJ) GroupEId.$(OBJ) inet.$(OBJ) Groupsock.$(OBJ) NetInterface.$(OBJ) NetAddress.$(OBJ) IOHandlers.$(OBJ)


GroupsockHelper.$(CPP):	include/GroupsockHelper.hh
include/GroupsockHelper.hh:	include/NetAddress.hh
include/NetAddress.hh:	include/NetCommon.h
GroupEId.$(CPP):	include/GroupEId.hh
include/GroupEId.hh:	include/NetAddress.hh
inet.$(C):		include/NetCommon.h
Groupsock.$(CPP):	include/Groupsock.hh include/GroupsockHelper.hh
include/Groupsock.hh:	include/groupsock_version.hh include/NetInterface.hh include/GroupEId.hh
include/NetInterface.hh:	include/NetAddress.hh
NetInterface.$(CPP):	include/NetInterface.hh include/GroupsockHelper.hh
NetAddress.$(CPP):	include/NetAddress.hh include/GroupsockHelper.hh
IOHandlers.$(CPP):	include/IOHandlers.hh

# libgroupsock.$(LIB_SUFFIX): $(GROUPSOCK_LIB_OBJS) \
#     $(PLATFORM_SPECIFIC_LIB_OBJS)
# 	$(LIBRARY_LINK)$@ $(LIBRARY_LINK_OPTS) \
# 		$(GROUPSOCK_LIB_OBJS)


$(NAME).so: $(GROUPSOCK_LIB_OBJS)
	$(CPLUSPLUS_COMPILER) -shared -o $@ $(GROUPSOCK_LIB_OBJS) -static-libstdc++ -Wl,-soname,$(NAME).so

clean:
	-rm -rf *.$(OBJ) $(ALL) core *.core *~ include/*~

install: install1 $(INSTALL2)
install1: libgroupsock.$(LIB_SUFFIX)
	  install -d $(DESTDIR)$(PREFIX)/include/groupsock $(DESTDIR)$(LIBDIR)
	  install -m 644 include/*.hh include/*.h $(DESTDIR)$(PREFIX)/include/groupsock
	  install -m 644 libgroupsock.$(LIB_SUFFIX) $(DESTDIR)$(LIBDIR)
install_shared_libraries: libgroupsock.$(LIB_SUFFIX)
		install -d $(DESTDIR)
	    cp libBasicUsageEnvironment.so $(DESTDIR)/

##### Any additional, platform-specific rules come here:
