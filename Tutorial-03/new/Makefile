OPTIMIZER := libLoopInvariantCodeMotion.so
OBJs := $(subst .cpp,.o,$(wildcard lib/*.cpp))

LLVM_VERSION ?= 14

CXXFLAGS := $(shell llvm-config-$(LLVM_VERSION) --cxxflags) -fPIC

all: $(OPTIMIZER) 

$(OPTIMIZER): $(OBJs)
	$(CXX) -dylib -shared $^ -o $@

.PHONY: clean
clean:
	$(RM) $(OPTIMIZER) $(OBJs)

run:
	opt -enable-new-pm=0 -load ./libLoopInvariantCodeMotion.so -loop-walk test/Loop.ll -o test/Loop.bc
	llvm-dis test/Loop.bc -o test/OptLoop.ll