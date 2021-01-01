# Scaled Algencan

[Algencan](https://www.ime.usp.br/~egbirgin/tango/codes.php) is an augmented Lagrangian solver written by E. Birgin and J.M. Martínez. It is available under the GNU General Public License.

**Scaled Algencan** is a modification of Algencan that implements the additional option of scaling the final solution, as described in

> [R. Andreani, G. Haeser, M.L. Schuverdt, L.D. Secchin, P.J.S. Silva. "On scaled stopping criteria for a safeguarded augmented
Lagrangian method with theoretical guarantees", 2020.](http://www.optimization-online.org/DB_HTML/2020/08/7985.html)

Scaled Algencan was implemented over the Algencan 3.1.1 code.


## Installation

All the code are generated from the original Algencan 3.1.1 code. To do so, follow the steps

1. Clone this repository;
1. Download the original Algencan 3.1.1 code from the [TANGO project](https://www.ime.usp.br/~egbirgin/tango/codes.php);
1. Put `algencan-3.1.1.tgz` in the `algencan-3.1.1-orig.code` directory. **Do NOT extract it**;
1. Run the script `install_algencan_scaled`. It applies the necessary patches to the Algencan 3.1.1 code.

**Scaled Algencan** will be placed in the `algencan-3.1.1_scaled` directory.


## Support for HSL packages

Algencan 3.1.1 supports [HSL](http://www.hsl.rl.ac.uk) MA57/MA86/MA97 packages. In order to use/compile them, the user needs to get they by yourself from [http://www.hsl.rl.ac.uk/catalogue](http://www.hsl.rl.ac.uk/catalogue). HSL packages are available at no cost for personal academic research and teaching, see [http://www.hsl.rl.ac.uk/licencing.html](http://www.hsl.rl.ac.uk/licencing.html) for more information.

**Scaled Algencan** was tested with the following packages:

- HSL MA57 version 5.2.0
- HSL MA86 version 1.6.0
- HSL MA97 version 2.5.0

To use them, put the downloaded files `hsl_ma57-5.2.0.tar.gz`, `hsl_ma86-1.6.0.tar.gz` and `hsl_ma97-2.5.0.tar.gz` in the `hsl` directory. **Do NOT extract them**.

*HSL packages are not mandatory for (scaled) Algencan. However, their use is recommended.*


## Support for the Metis package

[Metis](http://glaros.dtc.umn.edu/gkhome) is a package for serial graph partitioning and fill-reducing matrix ordering, freely available for educational and research purposes. HSL packages offer support to Metis. Until this moment, only Metis 4.0.3 is supported.

1. Download `metis-4.0.3.tar.gz` from [http://glaros.dtc.umn.edu/gkhome/fsroot/sw/metis/OLD](http://glaros.dtc.umn.edu/gkhome/fsroot/sw/metis/OLD);
1. Put `metis-4.0.3.tar.gz` in the `metis` directory. **Do NOT extract it**.

*Metis is not mandatory for HSL packages. However, its use is recommended.*


## Compilation and use

All instructions contained in the original `README` file of Algencan 3.1.1 remain valid, except for the compilation of BLAS, HSL and Metis packages.

The Scaled Algencan `Makefile` is prepared to unpack and compile HSL and Metis packages if their `.tar.gz` files were provided by the user, as described before. Only the mentioned versions are supported.

BLAS routines must be provided. The script is prepared to use the native [OpenBLAS](https://www.openblas.net) package. Other/Specific BLAS implementations can be used. In this case, the `BLAS` variable in the `hsl/compile` file must be adjusted accordingly. Indeed, vendor-specific implementations may be recommended for best performance.

To run Algencan with scaled stopping criterion, call it with the `OPTSCALE` parameter. You can use the `algencan.dat` file. For the CUTEst interface, just copy this file to the same folder as the Algencan executable file. For AMPL interface, run
~~~
./algencan problem.nl specfnm="algencan.dat"
~~~
from the folder where the executable file and `algencan.dat` are located.


## Funding

This research was supported by "Fundação de Amparo à Pesquisa e Inovação do Espírito Santo" - FAPES (grant 116/2019) - and FAPESP.


## How to cite

If you use this code in your publications, please cite us. For the moment, we only have the manuscript:

> [R. Andreani, G. Haeser, M.L. Schuverdt, L.D. Secchin, P.J.S. Silva. "On scaled stopping criteria for a safeguarded augmented
Lagrangian method with theoretical guarantees", 2020.](http://www.optimization-online.org/DB_HTML/2020/08/7985.html)

Also, consider citing the Algencan's original reference:

> R. Andreani, E. G. Birgin, J. M. Martínez and M. L. Schuverdt, "On Augmented Lagrangian methods with general lower-level constraints", SIAM Journal on Optimization 18, pp. 1286-1309, 2007.
