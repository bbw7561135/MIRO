===MIRO====
===========

MIRO code to model Faraday Rotation in simulated clusters/filaments, both in IDL and GDL version
;....
;...derived from Bonafede, Vazza et al. 2013 MNRAS

;....miro.pro -> basic IDL(v8.6.0) version of MIRO for simple simulations of Farday Rotation Measure 

;....miro_gdl.pro -> GDL (v0.9.6) version of MIRO - slightly modified version to cope with missing IDL libraries

;...needs/needs_gdl.pro -> necessary auxiliary files for compilations and routines

 Main features:
 ==============
 - 3D magnetic fields with divB=0 and input power spectra, components drawn from the Rayleigh distribution, with adjustable input power spectrum (tunable spectral slope and max/min scales).
 - gas density field from Beta model, with adjustable cluster parameters (core radius, core density...)
 - possibility of adding a simple cylindrical filament model
 - possibility of adding a random distribution of gas substructures (e.g. spherical clumps)
 - RM map making and comparison of profiles with the COMA profile
 

Compilation:
============
(IDL)
.r needs

.r needs

.r miro

(GDL)

.r needs_gdl

.r needs_gdl

.r miro_gdl

  Calling sequence:
  =================
     miro,input,dir_out=dir_out,res=res,n0=n0,rc=rc,bmean=bmean,kin=kin,kmax=kmax,alphak=alphak,seed=seed,name=name,ncentre=ncentre,alphaB=alphaB,nclump=nclump,rc_fila=rc_fila,nc_fila=nc_fila,write_disk=write_disk


  Adjustable parameters:
  ======================
  - dir_out=''   ;...folder for outputs
  - res=10 ;...cell resolution in kpc
  - n0=128 ;..grid size
  - kin=3     ;...minimum k for the power-law [0:n0*0.5-1]
  - kmax=(n0*0.5)-1   ;...maximum k  (n0*0.5-1 is the Nyquist frequency)
  - seed=systime(1) ;..random seed number
  - alphak=1.6666 ;...spectral index for 1D power specrtra (1.666 is for kolmogorov)
  - bmean=2 ;...[muG] wanted normalisation of the rms B-field within the volume
  - ncentre=3.3e-3 ;...[part/cm^3] particle density in the cluster core
  - rc=290 ;...[kpc] core radius of cluster
  - name="test" ;...identifier for this run
  - alphaB=0.666  ;...assumed exponent of the B(n) \propto n^alfaB scaling
  - nclump=0  ;..number of clumps (randomly distributed
   - rc_fila=0  ;...[kpc] core radius of filament 
   - nc_fila=0.1*ncentre  ;...[part/cm^3] central density of filament
   - write_disk=0,1 ;...enables the writing of a 4 x n0^3 binary dataset at the end of the run 
   
   
   Main outputs:
   =============
   
   - .eps file with various B-field statistics (profile, spectra and PDF)
   - .eps file with radial RM profile from model vs observed data for Coma
   - .fits file with projected maps of gas density, magnetic field and RM
   - .bin file with the 3D values of density, Bx, By, Bz for all simulated cells (optional)
   
   CPU Time
   ========
   On a Macbook Pro the basic run including the generation of a 3D magnetic field for a Beta-model (without filaments or clumps), requires a CPU time of T=12.1[s]*(n0/128)^3.  (IDL version)
   
   The code is not particularly well optimized.
   
   Further speedup may be possible with CPU,TPOOL_NTHREADS
