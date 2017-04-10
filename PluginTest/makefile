CC = D:\qnx660\host\win32\x86\usr\bin\arm-unknown-nto-qnx6.6.0eabi-g++-4.7.3
CCC = D:\qnx660\host\win32\x86\usr\bin\arm-unknown-nto-qnx6.6.0eabi-g++-4.7.3

TARGET = PluginTest
#全部编译文件
SRC_CPP := ./*.cpp
VPATH :=./:./object/
INCLUDES += -I.
#编译生成文件存放路径					
OBJECT_DIR = object/

##################################################
#额外编译路径

INCLUDES += -IE:\qnx_workspace\PluginCore
INCLUDES += -Id:\qnx660\target\qnx6\usr\include\c++\4.7.3
INCLUDES += -Id:\qnx660\target\qnx6\usr\include\c++\4.7.3\arm-unknown-nto-qnx6.6.0eabi

CFLAGS += -std=gnu++11
LDFLAGS := -L.
LDFLAGS2 += -lPluginShape -lPluginCore

##################################################
VPATH += $(EXTRA_DIR)
EXTRA_INCLUDE = $(addprefix -I,$(EXTRA_DIR))
INCLUDES += $(EXTRA_INCLUDE)
EXTRA_CPP = $(addsuffix *.cpp,$(EXTRA_DIR))
SRC_CPP += $(EXTRA_CPP)
#ABS_CPP = $(notdir $(SRC_CPP))
#DST_CPP=$(addprefix $(OBJECT_DIR),$(ABS_CPP))
SRC_OBJECT = $(patsubst %.cpp,%.o,$(wildcard $(SRC_CPP)))
OBJECT = $(notdir $(SRC_OBJECT))
DST_OBJECT = $(addprefix $(OBJECT_DIR),$(OBJECT))
all:PRE $(TARGET)
PFFILE = $(TARGET).pinfo

$(TARGET):$(DST_OBJECT)
	@echo compile $@
	$(CC) $(LDFLAGS) $^ $(LDFLAGS2)  -o $(OBJECT_DIR)$@ 
	@echo compile finish! TARGET=$(TARGET)
$(DST_OBJECT):$(OBJECT)	
$(OBJECT):%.o:%.cpp
	@echo compile $@
	$(CCC) -c $(CFLAGS) $(INCLUDES) $< -o $(OBJECT_DIR)$@

.PHONY:clean
clean:
	rm -f $(OBJECT_DIR)*.o
	rm -f $(OBJECT_DIR)$(TARGET)


	
.PHONY:PRE
PRE:
ifneq  ($(OBJECT_DIR), $(wildcard $(OBJECT_DIR)))
	mkdir -p $(OBJECT_DIR)
endif

。PHONY:PINFO
PINFO:
	echo DATE=`date` > $(PFFILE)
	echo USER=NOBODY >> $(PFFILE)
	$(PF) $(PFFLAG) -f $(PFFILE) $(OBJECT_DIR)$(TARGET)  

.PHONY:STRIP
STRIP:
	echo STRIP $(OBJECT_DIR)$(TARGET)
	$(STRIP) $(OBJECT_DIR)$(TARGET)
	