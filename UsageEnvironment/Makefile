INCLUDES = -Iinclude -I../groupsock/include
PREFIX = /usr/local
LIBDIR = $(PREFIX)/lib
##### Change the following for your environment:
NDK=/g/SDK/ndk/21.4.7075529
TOOLCHAIN=$(NDK)/toolchains/llvm/prebuilt/windows-x86_64
API=24
SYSROOT=$(NDK)/toolchains/llvm/prebuilt/windows-x86_64/sysroot
CROSS_PREFIX=$(TOOLCHAIN)/bin/arm-linux-androideabi-
DESTDIR=$(shell pwd)/../armeabi-v7a
  
COMPILE_OPTS = $(INCLUDES) -march=armv7-a -mfloat-abi=softfp -mfpu=vfpv3-d16 -fPIC -I$(SYSROOT)/usr/local/include -I. -O2 -DSOCKLEN_T=socklen_t -D_LARGEFILE_SOURCE=1 -D_FILE_OFFSET_BITS=64 -DNO_OPENSSL=1 -DNO_GETIFADDRS=1 --sysroot=$(SYSROOT)  
C =                     c
C_COMPILER =            $(TOOLCHAIN)/bin/armv7a-linux-androideabi$(API)-clang 
C_FLAGS =               $(COMPILE_OPTS)
CPP =                   cpp
CPLUSPLUS_COMPILER =    $(TOOLCHAIN)/bin/armv7a-linux-androideabi$(API)-clang++ 
CPLUSPLUS_FLAGS =       $(COMPILE_OPTS) -Wall -DBSD=1
OBJ =                   o
LINK =                  $(CPLUSPLUS_COMPILER) -o 
LINK_OPTS =             -static-libstdc++
CONSOLE_LINK_OPTS =     $(LINK_OPTS)
LIBRARY_LINK =          $(CROSS_PREFIX)ar cr  
LIBRARY_LINK_OPTS =
LIB_SUFFIX =            a
LIBS_FOR_CONSOLE_APPLICATION =  
LIBS_FOR_GUI_APPLICATION =
EXE =##### End of variables to change

NAME = libUsageEnvironment
USAGE_ENVIRONMENT_LIB = $(NAME).$(LIB_SUFFIX)
ALL = $(USAGE_ENVIRONMENT_LIB)
all:	$(ALL)

OBJS = UsageEnvironment.$(OBJ) HashTable.$(OBJ) strDup.$(OBJ)

$(USAGE_ENVIRONMENT_LIB): $(OBJS)
	$(LIBRARY_LINK)$@ $(LIBRARY_LINK_OPTS) $(OBJS)

.$(C).$(OBJ):
	$(C_COMPILER) -c $(C_FLAGS) $<       

.$(CPP).$(OBJ):
	$(CPLUSPLUS_COMPILER) -c $(CPLUSPLUS_FLAGS) $<

UsageEnvironment.$(CPP):	include/UsageEnvironment.hh
include/UsageEnvironment.hh:	include/UsageEnvironment_version.hh include/Boolean.hh include/strDup.hh
HashTable.$(CPP):		include/HashTable.hh
include/HashTable.hh:		include/Boolean.hh
strDup.$(CPP):			include/strDup.hh

clean:
	-rm -rf *.$(OBJ) $(ALL) core *.core *~ include/*~

install: install1 $(INSTALL2)
install1: $(USAGE_ENVIRONMENT_LIB)
	  install -d $(DESTDIR)$(PREFIX)/include/UsageEnvironment $(DESTDIR)$(LIBDIR)
	  install -m 644 include/*.hh $(DESTDIR)$(PREFIX)/include/UsageEnvironment
	  install -m 644 $(USAGE_ENVIRONMENT_LIB) $(DESTDIR)$(LIBDIR)
install_shared_libraries: $(USAGE_ENVIRONMENT_LIB)
	  ln -fs $(NAME).$(LIB_SUFFIX) $(DESTDIR)$(LIBDIR)/$(NAME).$(SHORT_LIB_SUFFIX)
	  ln -fs $(NAME).$(LIB_SUFFIX) $(DESTDIR)$(LIBDIR)/$(NAME).so

##### Any additional, platform-specific rules come here:
