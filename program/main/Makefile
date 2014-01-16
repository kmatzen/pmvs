######################################################################
#
# The following 2 commands to compile pmvs2.
# > make depend
# > make
#
######################################################################
CXX = g++


# Your INCLUDE path (e.g., -I/usr/include)
YOURINCLUDEPATH =-I/tmp/kmatzen/intel/mkl/include/intel64 -I/usr/local/intel/mkl/include/intel64 -I../include

# Your LDLIBRARY path (e.g., -L/usr/lib)
YOURLDLIBPATH =-L/tmp/kmatzen/intel/mkl/lib/intel64 -L/usr/local/intel/mkl/lib/intel64

CXXFLAGS = -O3 -g -Wall -Wno-deprecated ${YOURINCLUDEPATH} -DDEBUG

LDFLAGS = ${YOURLDLIBPATH} -lXext -lX11 -ljpeg -lgsl -lgslcblas -lpthread -lm -lmkl_rt

######################################################################
all: pmvs2

pmvs2: pmvs2.o detectFeatures.o dog.o harris.o point.o detector.o \
	findMatch.o detector.o expand.o filter.o optim.o \
	patchOrganizerS.o seed.o point.o option.o \
	image.o camera.o photoSetS.o patch.o photo.o \
	mylapack.o
	${CXX} -o $@ $^ ${LDFLAGS}

%.o : ../base/pmvs/%.cc
	$(CXX) -c $(CXXFLAGS) $<

%.o : ../base/image/%.cc
	$(CXX) -c $(CXXFLAGS) $<

%.o : ../base/numeric/%.cc
	$(CXX) -c $(CXXFLAGS) $<

######################################################################
# general commands
clean:
	/bin/rm -f core core.* *.o ${TARGET}

depend:
	rm -f Dependencies
	for SOURCEFILE in `ls *.cc ../base/*/*.cc ../base/*/*.c ../base/*/*.C ../base/*/*.f`; do \
	  echo $$SOURCEFILE; \
	  $(CXX) -MM $(CXXFLAGS) $$SOURCEFILE >> Dependencies; \
	done

-include Dependencies
