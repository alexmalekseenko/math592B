PROG =  ffbM300.a	

SRCS =	BGKVDCF0D_commvar.f90 BGKVDCF0D_miscset.f90 BGKVDCF0D_readwrite.f90 \
	BGKVDCF0D_spat_oper_mod.f90 BGKVDCF0D_time_integr_mod.f90 \
	BGKVDCF0Driver.f90 DGV_collision_mod.f90 DGV_commvar.f90 \
	DGV_dgvtools_mod.f90 DGV_distributions_mod.f90 DGV_miscsetup.f90 \
	DGV_readwrite.f90 DGV_sf02.f90 gaussian_mod.f90 \
	gaussquad.f90 nrroutines_mod.f90 nrtype.f90 nrutil.f90 algama.f

OBJS =	BGKVDCF0D_commvar.o BGKVDCF0D_miscset.o BGKVDCF0D_readwrite.o \
	BGKVDCF0D_spat_oper_mod.o BGKVDCF0D_time_integr_mod.o \
	BGKVDCF0Driver.o DGV_collision_mod.o DGV_commvar.o DGV_dgvtools_mod.o \
	DGV_distributions_mod.o DGV_miscsetup.o \
	DGV_readwrite.o DGV_sf02.o gaussian_mod.o gaussquad.o \
	nrroutines_mod.o nrtype.o nrutil.o algama.o

LIBS =  -Wl,--start-group ${MKLROOT}/lib/intel64/libmkl_intel_ilp64.a ${MKLROOT}/lib/intel64/libmkl_intel_thread.a ${MKLROOT}/lib/intel64/libmkl_core.a -Wl,--end-group -liomp5 -lpthread -lm -ldl 	

CC = cc
CFLAGS = -O
FC = ifort
FFLAGS = -O3 -qopenmp
F90 = ifort
F90FLAGS = -qopenmp -I${MKLROOT}/include -O3 -mkl=parallel
LDFLAGS = -O3 -mkl=parallel

all: $(PROG)

$(PROG): $(OBJS)
	$(F90) $(LDFLAGS) -o $@ $(OBJS) $(LIBS)

clean:
	rm -f $(PROG) $(OBJS) *.mod

.SUFFIXES: $(SUFFIXES) .f90

.f90.o:
	$(F90) $(F90FLAGS) -c $<

BGKVDCF0D_commvar.o: nrtype.o
BGKVDCF0D_miscset.o: BGKVDCF0D_commvar.o gaussian_mod.o gaussquad.o nrtype.o
BGKVDCF0D_readwrite.o: BGKVDCF0D_commvar.o DGV_commvar.o DGV_dgvtools_mod.o \
	DGV_distributions_mod.o nrtype.o
BGKVDCF0D_spat_oper_mod.o: BGKVDCF0D_commvar.o DGV_collision_mod.o nrtype.o
BGKVDCF0D_time_integr_mod.o: BGKVDCF0D_commvar.o BGKVDCF0D_spat_oper_mod.o \
	nrtype.o
BGKVDCF0Driver.o: BGKVDCF0D_commvar.o BGKVDCF0D_miscset.o \
	BGKVDCF0D_readwrite.o BGKVDCF0D_time_integr_mod.o DGV_collision_mod.o \
	DGV_commvar.o DGV_dgvtools_mod.o DGV_miscsetup.o DGV_sf02.o nrtype.o
DGV_collision_mod.o: BGKVDCF0D_commvar.o BGKVDCF0D_readwrite.o DGV_commvar.o \
	DGV_dgvtools_mod.o DGV_distributions_mod.o nrtype.o
DGV_commvar.o: nrtype.o
DGV_dgvtools_mod.o: DGV_commvar.o DGV_distributions_mod.o gaussian_mod.o \
	nrtype.o 
DGV_distributions_mod.o: nrtype.o
DGV_miscsetup.o: DGV_commvar.o DGV_dgvtools_mod.o DGV_readwrite.o \
	gaussian_mod.o gaussquad.o nrtype.o
DGV_readwrite.o: DGV_commvar.o DGV_dgvtools_mod.o nrtype.o
DGV_sf02.o: nrtype.o
gaussian_mod.o: nrtype.o nrutil.o
nrroutines_mod.o: 
nrutil.o: nrtype.o
