TOP=../..

include $(TOP)/configure/CONFIG
#----------------------------------------
#  ADD MACRO DEFINITIONS AFTER THIS LINE
#=============================

USR_CPPFLAGS += -DUSE_TYPED_RSET

# Cygwin rpc is in tirpc
USR_INCLUDES_cygwin32 += -I/usr/include/tirpc
USR_INCLUDES_Linux += -I/usr/include/tirpc

#PROD_HOST += caExample
#caExample_SRCS	+= caExample.c
#caExample_LIBS	+= ca
#caExample_LIBS	+= Com
ca_DIR           = $(EPICS_BASE_LIB)
Com_DIR          = $(EPICS_BASE_LIB)


#=============================
# xxxRecord.h will be created from xxxRecord.dbd

DBDINC += scanparmRecord
DBDINC += sscanRecord
DBDINC += menuSscan

# <name>.dbd will be created from <name>Include.dbd
DBD += sscan.dbd
DBD += sscanSupport.dbd
DBD += sscanProgressSupport.dbd
DBD += menuSscan.dbd
INC += recDynLink.h

#=============================

LIBRARY_IOC += sscan
sscan_SRCS += sscanRecord.c
sscan_SRCS += scanparmRecord.c
sscan_SRCS += recDynLink.c
sscan_SRCS += req_file.c

ifdef SNCSEQ
	LIBRARY_IOC += scanProgress
	scanProgress_SRCS += scanProg.st
endif

# save scan data stuff
sscan_SRCS += saveData_writeXDR.c, writeXDR.c

# The old saveData code, in case it's still needed on some platform
#sscan_SRCS += xdr_lib.c
#sscan_SRCS += saveData.c
#sscan_SRCS_vxWorks += xdr_stdio.c
#sscan_SYS_LIBS_cygwin32 += $(CYGWIN_RPC_LIB)


# for scanProgress
ifdef SNCSEQ
	scanProgress_LIBS += seq pv
	scanProgress_LIBS += $(EPICS_BASE_IOC_LIBS)
endif

sscan_LIBS += $(EPICS_BASE_IOC_LIBS)

include $(TOP)/configure/RULES
#----------------------------------------
#  ADD RULES AFTER THIS LINE

# Parallel build sometimes fails.
# Make dependences on sscanRecord.h explicit.
sscanRecord$(OBJ):     $(COMMON_DIR)/sscanRecord.h
scanparmRecord$(OBJ):  $(COMMON_DIR)/scanparmRecord.h
