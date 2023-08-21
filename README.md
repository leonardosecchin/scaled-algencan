# Scaled Algencan

[Algencan](https://www.ime.usp.br/~egbirgin/tango/codes.php) is a safeguarded augmented Lagrangian solver written by E. Birgin and J.M. Martínez. It is available under the GNU General Public License.

**Scaled Algencan** is a modification of Algencan that implements the additional option of scaling the final solution, as described in

> [R. Andreani, G. Haeser, M.L. Schuverdt, L.D. Secchin, P.J.S. Silva. On scaled stopping criteria for a safeguarded augmented
Lagrangian method with theoretical guarantees. *Mathematical Programming Computation*, 14:121-146, 2022.](https://doi.org/10.1007/s12532-021-00207-9)

Scaled Algencan was implemented over the Algencan 3.1.1 code.


## Installation

All the code are generated from the original Algencan 3.1.1 code. To do so, follow the steps

1. Clone or download this repository;
1. Download the original Algencan 3.1.1 code from the [TANGO project](https://www.ime.usp.br/~egbirgin/tango/codes.php);
1. Put `algencan-3.1.1.tgz` in the `algencan-3.1.1-orig.code` directory. **Do NOT extract it**;
1. Run `./install_algencan_scaled`. It applies the necessary patches to the Algencan 3.1.1 code.

**Scaled Algencan** will be placed in the `algencan-3.1.1_scaled` directory.


## Support for HSL packages

Algencan 3.1.1 supports [HSL](http://www.hsl.rl.ac.uk) MA57/MA86/MA97 packages. To use/compile them, you need to get them yourself from <http://www.hsl.rl.ac.uk/catalogue>. HSL packages are available at no cost for personal academic research and teaching, see <http://www.hsl.rl.ac.uk/licencing.html> for more information.

**Scaled Algencan** was tested with the following packages:

- HSL MA57 version [5.2.0](https://www.hsl.rl.ac.uk/download/HSL_MA57/5.2.0/)
- HSL MA86 version [1.6.0](https://www.hsl.rl.ac.uk/download/HSL_MA86/1.6.0/)
- HSL MA97 version [2.5.0](https://www.hsl.rl.ac.uk/download/HSL_MA97/2.5.0/)

To use them, put the downloaded files `hsl_ma57-5.2.0.tar.gz`, `hsl_ma86-1.6.0.tar.gz` and/or `hsl_ma97-2.5.0.tar.gz` in the `hsl` directory. **Do NOT extract them**. Note that you can use just one or multiple HSL packages simultaneously.

*HSL packages are not mandatory for (scaled) Algencan. However, their use is recommended. Other/Newer versions of HSL_MA57 probably DO NOT WORK.*


## Support for the Metis package

[Metis](http://glaros.dtc.umn.edu/gkhome) is a package for serial graph partitioning and fill-reducing matrix ordering, freely available for educational and research purposes. HSL packages offer support to Metis. Until this moment, only Metis 4.0.3 is supported.

1. Download `metis-4.0.3.tar.gz` from <http://glaros.dtc.umn.edu/gkhome/fsroot/sw/metis/OLD>;
1. Put `metis-4.0.3.tar.gz` in the `metis` directory. **Do NOT extract it**.

*Metis is recommended for HSL packages. It may be required for the correct compilation of the HSL libraries.*


## Compilation

The Scaled Algencan `Makefile` is prepared to unpack and compile HSL and Metis packages if their `.tar.gz` files were provided by the user, as described before. Only the mentioned versions are supported.

BLAS routines must be provided. The script is prepared to use the native [OpenBLAS](https://www.openblas.net) package. Other/Specific BLAS implementations can be used. In this case, the `BLAS` variable in the `hsl/compile` file must be adjusted accordingly. Indeed, vendor-specific implementations may be recommended for best performance.

All instructions contained in the original `README` file of Algencan 3.1.1 remain valid, except for the compilation of BLAS, HSL and Metis packages.

*IMPORTANT: if you have problems compiling Scaled Algencan with HSL, please also provide the Metis 4.0.3 package (actually, it is recommended). See the previous topic.*

### Compiling Scaled Algencan for AMPL

To compile the executable file for AMPL, first you need to download and configure the AMPL Solver Library (ASL):

1. Download `solvers.tgz` or `solvers2.tgz` from [Netlib](http://www.netlib.org/ampl/) and extract it to the directory of your choice;
1. From the ASL directory, run `./configurehere` and then `make`.

To compile Scaled Algencan for AMPL, set the variable `AMPL` in `algencan-3.1.1_scaled/Makefile` to the ASL directory and run
~~~
make algencan-ampl
~~~
from `algencan-3.1.1_scaled`. This will create the executable file `algencan-3.1.1_scaled/bin/ampl/algencan`. To run Scaled Algencan from any folder, add `[YOUR DIRECTORY]/algencan-3.1.1_scaled/bin/ampl` to your PATH environment variable.

### Compiling Scaled Algencan for CUTEst

Firstly, you need to get all CUTEst machinery (CUTEst, SIF decoder and ARCH defs). We recommend obtaining them from the RAL Computational Mathematics git repositories. See <https://github.com/ralna>. After clone/download them, follow the instructions in `CUTEst/README` to install CUTEst.

Then, you need to adjust variables in `algencan-3.1.1_scaled/Makefile`. Set `ARCHDEFS`, `SIFDECODE` and `CUTEST` variables to their respective directories. The variable `MYARCH` will depend on your system and compiler used. Set `MASTSIF` to the directory containing the problem's SIF files. You can get them at <https://bitbucket.org/optrove/sif>.

Scaled Algencan must be compiled for each problem. For example, to compile it for the problem `ACOPR57`, run
~~~
make algencan-cutest PROBNAME=ACOPR57
~~~
from `algencan-3.1.1_scaled`. This will create the executable file `algencan` and the decoded SIF file `OUTSDIF.d` in `algencan-3.1.1_scaled/bin/cutest`.

### Compiling Scaled Algencan for Julia

It is possible to use Scaled Algencan with Julia via `NLPModelsAlgencan.jl`, a package maintained by P.J.S. Silva. To do this, you need to create the shared library `libalgencan.so`. Just run
~~~
make sharedlib
~~~
from `algencan-3.1.1_scaled`. The `libalgencan.so` file will be placed in the `lib` folder. Metis and HSL packages will be automatically incorporated if provided. Finally, follow the instructions on the [`NLPModelsAlgencan.jl` page](https://github.com/pjssilva/NLPModelsAlgencan.jl) to use the compiled shared library.

### Compiling your own C/Fortran code

As with Algencan, you can integrate Scaled Algencan with your C/Fortran code. As a reference, consider the `toyprob.f90` file located at `sources/examples/f90/`. The procedures for C codes are analogous, you just need to include the `-lgfortran` tag when using static libraries with `gcc`.

Following the original Algencan instructions, if you use more than one HSL package you will encounter "multiple definitions" errors when compiling using static libraries. This is because certain internal HSL functions appear repeated within `hsl_ma57-5.2.0.tar.gz`, `hsl_ma86-1.6.0.tar.gz` and `hsl_ma97-2.5.0.tar.gz`. There are at least two solutions:

1. Compile using `-zmuldefs` tag

You can avoid compilation errors by using the `-zmuldefs` tag (GNU compilers). From the `algencan-3.1.1_scaled` directory, try
~~~
make
cd sources/examples/f90/
gfortran -O3 toyprob.f90 -L../../../lib -lalgencan -lm -lopenblas -zmuldefs -o algencan
~~~

1. Compile using dynamic libraries

From the `algencan-3.1.1_scaled` directory, try
~~~
make sharedlib
cd sources/examples/f90/
gfortran -O3 toyprob.f90 -L../../../lib -lalgencan -o algencan
~~~
To run the compiled executable `algencan`, you first need to put the path `[SCALED-ALGENCAN path]/lib` in the environment variable `LD_LIBRARY_PATH` or equivalent.


## Usage

**The scaled stopping criterion is enabled by default.** To run Algencan without it, call the algorithm with the `NON-SCALED-OPTIMALITY` flag. To do this, adjust the `algencan.dat` file accordingly. For the CUTEst interface and your own C/Fortran code, just copy this file to the same folder as the Scaled Algencan executable file. For AMPL interface, run
~~~
algencan problem.nl specfnm="algencan.dat"
~~~
from the folder where `algencan.dat` is located, or set `specfnm` to the absolute/relative path of `algencan.dat`. If you are calling Scaled Algencan from Julia, run
~~~
julia> algencan(nlp, specfnm="algencan.dat")
~~~
where `nlp` is the `NLPModels` structure of the problem to be solved.

It is possible to adjust the maximum scale factor for optimality using `algencan.dat`. See instructions in the file.

You can set all the usual Algencan parameters in `algencan.dat`. See chapter 10 of the [book by E. Birgin and J.M. Martínez](https://doi.org/10.1137/1.9781611973365) for details.

In the AMPL and Julia interfaces, several parameters can be passed diretcly from the command line. To see a list of them, run the AMPL interface with `-=` option (`bin/ampl/algencan -=`). You can also see [this link](https://pjssilva.github.io/NLPModelsAlgencan.jl/dev/parameters/).


## Funding

This research was supported by "Fundação de Amparo à Pesquisa e Inovação do Espírito Santo" - FAPES (grant 116/2019) - and FAPESP.


## How to cite

If you use this code in your publications, please cite us:

> [R. Andreani, G. Haeser, M.L. Schuverdt, L.D. Secchin, P.J.S. Silva. On scaled stopping criteria for a safeguarded augmented
Lagrangian method with theoretical guarantees. *Mathematical Programming Computation*, 14:121-146, 2022.](https://doi.org/10.1007/s12532-021-00207-9)

Also, consider citing the Algencan's original reference:

> R. Andreani, E. G. Birgin, J. M. Martínez and M. L. Schuverdt, On Augmented Lagrangian methods with general lower-level constraints. *SIAM Journal on Optimization*, 18:1286-1309, 2007.
