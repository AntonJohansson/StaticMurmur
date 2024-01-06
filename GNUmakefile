CXX:=g++
# C++11:=c++11
C++14:=c++14
C++17:=c++17
C++20:=c++2a
C++STANDARDS:=$(C++14) $(C++17) $(C++20)

.PHONY: default all clean rebuild
.NOTPARALLEL: clean rebuild
default: all;

define bycppstd
test_$(1).o: CXXFLAGS+=-std=$(1)

test_$(1).o: test.cpp
	$$(COMPILE.cc) $$(OUTPUT_OPTION) $$<

TARGETS+=$$(strip $$(TARGET) test_$(1))
endef
# Instantiate the above function for each standard
$(foreach i,$(C++STANDARDS),$(eval $(call bycppstd,$(i))))
TARGETS:=$(strip $(TARGETS))

%: %.o
	$(LINK.cc) $^ $(LOADLIBES) $(LDLIBS) -o $@

all: $(TARGETS)

test.cpp: StaticMurmur.hpp

clean:
	-rm -f $(TARGETS) $(addsuffix .o,$(TARGETS))

rebuild: clean all
