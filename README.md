
<img src="logoqpub.png" width="200"> ... **adding Bayesian flavour to peptide quantification**

&nbsp;

**Update April 2021: QPuB is current work in progress, an updated version will be available soon!**

:black_medium_small_square:[Bayesian inference][bayestat-url] 
:black_medium_small_square:[Peptide quantification][peptide-url]
:black_medium_small_square:[Mass spectrometry][massspec-url]
:black_medium_small_square:[Proteomics][proteo-url]

The mass spectrometry ion peak area of peptides is linearly related to the absolute amount of the peptides through 
a proportionality constant called conversion factor [4].
QPuB (**Q**uantifcation of **P**eptides **u**sing **B**ayesian inference) employs [Bayesian statistical inference](https://en.wikipedia.org/wiki/Bayesian_inference) based on [Markov chain Monte Carlo (MCMC)](https://en.wikipedia.org/wiki/Markov_chain_Monte_Carlo) sampling to learn the posterior distributions of the conversion factors for the peptide products without further experimentation. 

## Getting started

The following instructions will help you to download QPuB and execute the same to estimate the conversion factors for your peptide products. 

### Prerequisites

In order to run QPuB, users must install [**R** ≥ 3.5.0](https://www.r-project.org/) and the following R packages:

* [**R.utils**](https://cran.r-project.org/web/packages/R.utils/index.html)
   
* [**tictoc**](https://cran.r-project.org/web/packages/tictoc/index.html) 

* [**sys**](https://cran.r-project.org/web/packages/sys/index.html) 
   
* [**mcmcse**](https://cran.r-project.org/web/packages/mcmcse/index.html) 

* [**mvtnorm**](https://cran.r-project.org/web/packages/mvtnorm/index.html) 
   
* [**tmvtnorm**](https://cran.r-project.org/web/packages/tmvtnorm/index.html)  

* [**corpcor**](https://cran.r-project.org/web/packages/corpcor/index.html) 
   
* [**dqrng**](https://www.rdocumentation.org/packages/dqrng/index.html) 
   
* [**coda**](https://cran.r-project.org/web/packages/coda/index.html) 

* [**matrixcalc**](https://www.rdocumentation.org/packages/matrixcalc) 

* [**ggdmc**](https://www.rdocumentation.org/packages/ggdmc)

* [**matrixStats**](https://www.rdocumentation.org/packages/matrixStats) 

To install the above packages one by one, start your **R** shell, and execute the following command:

```R
 install.packages("package_name")
 ```
where the **package_name** should be replaced by the name of packages that are listed above. Alternatively, one can copy-paste the following command to the R terminal 

```R
install.packages(c("R.utils", "tictoc", "mcmcse", "mvtnorm", "tmvtnorm", "corpcor", "dqrng", "coda", "matrixcalc", "ggdmc", "sys", "matrixStats"))
 ```
and press enter.

REMEMBER, for Linux, the above command might need the root access.


## Running QPuB
   Once all the prerequisites are met, QPuB needs to be downloaded from its Github repository. Click [here](https://github.com/QuantSysBio/QPuB/archive/master.zip) to download the .zip file and unzip it. 
   QPuB is designed to be invoked using the command line arguments as well as from as from any graphical user interface such as [RStudio](https://www.rstudio.com/), but with little modifications in the code. See **Running QPuB from RStudio** below.
   
   In order to run QPuB on your data from the terminal, follow these steps:

**1.** Make sure everything is properly installed on your computer (see
Chapter 3 of the [Documentation](Documentation.pdf)).

**2.** Make sure the data files and the input folder have the right
structure (see Sections 2.3.1 and 2.3.2  of the [Documentation](Documentation.pdf) for more details)

**3.** Open the terminal/command prompt (How to:
[Linux](https://www.wikihow.com/Open-a-Terminal-Window-in-Ubuntu),
[Mac](https://www.wikihow.com/Open-a-Terminal-Window-in-Mac),
[Windows](https://www.wikihow.com/Open-Terminal-in-Windows)).

**4.** Navigate to the directory from where you want to run QPuB, For example, if the name of the directory is "ABC" then 
       the command takes the following generic form:
```sh 
   $ cd <path to the ABC folder>
```
For more details on how to navigate to a particular directory using the **cd** command, see [here](https://en.wikipedia.org/wiki/Cd_(command)). 

**5.** Once you are in your working directory (the directory from where you wish to run QPuB), say "ABC", the command to run QPuB has the following generic form

```sh
   $ Rscript <path to runQPuB.r relative to the folder ABC> -infol <path to input_folder> -outfol <output_folder> -titr <titration_file>
```
**NOTE** The commands described above are providing a generic structure and must not be copy-pasted directly in the terminal.

For execution, the fields enclosed within **<>** including the symbol **<>** must be replaced by appropriate folder and file names along with their relative paths (if required) as explained in the **Examples** below. For the output folder you should not provide the path, but only the name of the folder. The same applies for the titration data file. Note that for now, ./ and ../ notation does not work. Please use the full path. Also avoid leading and trailing slashes.

The table below describes the meaning of the command line arguments:

|         Flag                 |                 Meaning                                                              |
| :----------------------- | :---------------------------------------------------------------------------- |
| <span>**-infol**</span>  | flag for the <span>**input_folder**</span>. This input is mandatory.      |
| <span>**-outfol**</span> | flag for the <span>**output_folder**</span>. This input is optional, and the name can be defined by the user.            |
| <span>**-titr**</span>   | flag for the <span>**titration_file**</span>. It is a csv-file. This input is optional. |

Flags can also be specified using `--` as prefix. For example, `--infol=inputfolder`. If you do not wish to provide the output folder and/or titration data, please do not type the respective flags. Please follow the examples below for illustrations.


## Examples

   The **examples** folder contains two toy examples of endopeptidase digestion, one toy exopeptidase digestion, and a real data gp100<sub>40-52</sub> digestion by 26S proteasomes. In order to run these examples, execute the following commands in the terminal **assuming your current directory is the QPuB-master folder**:
   
   ### Example 1: In silico endopeptidase digestion without noise
   ```sh    
   
      Rscript ./QPuB/runQPuB.r -infol examples/insilico_endopep_nonoise
       
 ``` 
   ### Example 2: In silico endopeptidase digestion with noise  
  ```sh     
  
      Rscript ./QPuB/runQPuB.r -infol examples/insilico_endopep__noise
   
 ``` 
  ### Example 3: In silico exopeptidase digestion with noise 
  ```sh     
       
      Rscript ./QPuB/runQPuB.r -infol examples/insilico_exopep_noise
   
 ``` 
   ### Example 4: gp100<sub>40-52</sub> digestion by 26S proteasomes
  ```sh     
       
      Rscript ./QPuB/runQPuB.r -infol examples/gp100_40-52_proteasome -titr 190423_K386_titration_substrate_charge_3.csv
   
 ``` 
 ## Running QPuB from [RStudio](https://www.rstudio.com/)
 
One can execute QPuB from RStudio, but in that case one first needs to open the main Rscript **runQPuB.r** and disable/comment out the following code snippet in the head of that script

```R
args = commandArgs(trailingOnly=FALSE, asValue=TRUE)
keys <- attachLocally(args)

if (!exists('infol')){
stop("This is the QPuB package. \n
At least one argument must be supplied: -infol.\n 
-infol inputfolder (COMPULSORY): folder containing all of the following input files \n AND folder 'data' with at least one csv file with input data. \n 
-outfol outputfolder (OPTIONAL): if not provided, default name will be 'OUTPUT_inputfolder(i)'. \n
-titr titrationfile (OPTIONAL): csv file with titration data \n
For documentation see: https://github.com/QuantSysBio/QPuB.\n", call.=FALSE)
}
```
and enable/uncomment the following snippet and edit the variables according to the desired example. For **Prot_K386** with an output folder **my_fancy_name**, the snippets looks like the following:

```R
# setwd("...")
# file <- 'runQPuB.r'
# infol <- 'examples/Prot_K386'
# outfol <- 'my_fancy_name'
# titr <- '190423_K386_titration_substrate_charge_3_K386.csv'
```
However, in order to avoid complications (especially crashing of RStudio for large datasets), users are strongly recommended to use the command line as described above.

 ## Output of QPuB
 
  QPuB generates the following set of output files and folders as the algorithm proceeds:
   
 | File/Folder | Description |
| ------ | ------ |
|<span>**runQPuB\_ROUT.txt**</span> | Progress report of the algorithm. The output of every print command directly goes into this file.|  
|<span>**plots\_inputsignals**</span> | Folder containing the kinetic plots of the input signal intensities for all peptide products  |
|<span>**peptide\_i.png**</span> | Kinetic plot of the input signal intensities for peptide i. In the folder.  |
|<span>**identifier.csv**</span> | Table of peptide numbers, sequences and position codes  |
|<span>**plots\_diagnostics**</span> | Folder containing the diagnostic plots of the chain and the residuals  |
|<span>**chain\_j.pdf**</span> | Trace plots and distributions of the Markov chain at j<sup>th</sup> iteration. In the folder.  |
|<span>**residuals\_j.txt**</span> | Residual plots at j<sup>th</sup> iteration. In the folder.  |
|<span>**chain.RData**</span> | Markov chain: time series of all parameters  |
|<span>**chain\_backscaled.RData**</span> | Markov chain after backscaling  |
|<span>**statistics.csv**</span> | Summary statistics of the backscaled Markov chain  |
|<span>**statistics.pdf**</span> | Graphical summary statistics of the backscaled conversion factors for all peptide products  |
|<span>**substratetitration\_given.png**</span> | Plot of the titration data and the linear fit. Only if titration provided.  |
|<span>**substratetitration\_normalized.png**</span> | Plot of the normalised titration data and the linear fits. Only if titration provided.  |
|<span>**concentrations**</span> | Folder containing the numerical values of the absolute amounts (if titration provided) or normalised signals (if not provided)  |
|<span>**conc\_five\_rp.csv, conc\_median\_rp.csv, conc\_ninetyfive\_rp.csv** </span> | 0.05, 0.5 and 0.95 quantiles of concentration kinetics of all products for the rp<sup>th</sup> replicate. In the folder.  |
|<span>**plots\_concentrations**</span> | Folder containing the kinetic plots of the absolute amounts (if titration provided) or normalised signals (if not provided)  |
|<span>**peptide\_i.png**</span> | Kinetic plot of the absolute amounts or normalised signal for peptide i. In the folder.|

Output generated while running the examples are illustrated in Chapter 5 of the [Documentation](Documentation.pdf).
    
## Troubleshooting

In this chapter, we list a non-exhaustive list of issues that the user
might run into while running QPuB. However, users are <span>strongly
recommended</span> to keep track of the **runQPuB\_ROUT.txt** from
<span>the very beginning of the run</span>, as all the outputs, including
the warnings for erroneous input provided, are printed.

### Multiple installations of R

The user must make sure that the installed version of R is 3.5.0 or above. In
case, the user has multiple installations of R, the path to the R
executable corresponding to the version specified for QPuB should be
provided. For Windows, please click
[here](https://cran.r-project.org/bin/windows/base/rw-FAQ.html#Rcmd-is-not-found-in-my-PATH_0021)
for more details on how to include the desired R executable in the PATH
variable.

### Command line execution

Care must be taken while writing the command line to run QPuB. For
example, the following type of command will generate error:  

``` 
$ Rscript path_to_runQPuB.r -infol ../examples/example_folder
```

Instead, the <span>right</span> command type is

    $ Rscript path_to_runQPuB.r -infol examples/example_folder

The same rules applies while including the titration file, for example,
assuming the name of the example folder as **P** and the corresponding
titration file name is **titration\_P**, the following command

    $ Rscript path_to_runQPuB.r -infol examples/P -titr examples/P/titration_P.csv

will generate an error, while the command

    $ Rscript path_to_runQPuB.r -infol examples/P -titr titration_P.csv

will work nicely.

### MCMC chains

It may happen that the Markov chain is not exploring the parameter
space. There might be several reasons for that. For example, the value
of `sigma_start` is so low that the chain stops exploring the parameter
space. At the same time if the value of the `GammaExponent` is higher,
due to vanishing nature of the adaptation, the covariance matrix will
remain stationary leaving the chain stuck at an undesired region.
Therefore, one solution to this is to stop the adaptation at the
beginning for sufficient exploration and then resume the adaptation
again after visually inspecting the chain. This may take several trial
runs to know the number of iterations needed before starting the
adaptation. Remember that this problem is different than the one where
the chain needs to adapt at the beginning to reach the target
covariance matrix. But, it may take over millions of iterations before reaching the target region. This is
especially the case for higher dimensions. Overall, depending upon the
problem, users are recommended to experiment with the parameters
controlling the adaptation scheme and the Markov chain. In [3], the authors
provide an excellent summary of various pathological cases regarding the
adaptive scheme and optimal scaling for MCMC.

 ## Documentation
 
   A documentation explaining the details of QPuB is available as [PDF](Documentation.pdf).
  
 ## Developers
               
  * [**Sarah Henze**](https://www.mpibpc.mpg.de/person/59990/84522)
  
  * [**Debdas Paul**](https://www.mpibpc.mpg.de/person/97709/2169)  
  
  * [**Juliane Liepe**](https://www.mpibpc.mpg.de/person/52238/15851745)
 
 ## References related to QPuB 
    
   [1] Henze, S., Paul, D., Mansurkhodzhaev, A., Henklein, P., Textoris-Taube, K., Urlaub, H., Mishto,
M., and Liepe, J. (2019). Quantification of in vitro peptide hydrolysis and protease-catalyzed
peptide splicing using Bayesian inference. Under review.

   [2] Henze, S*., Paul, D*., Mishto, M., Liepe, J. (2019). QPuB - Quantification of Peptides using Bayesian inference. In preparation.  *Equal contributions
   
## Other references

   [3] Rosenthal, J. S. (2011). Optimal proposal distributions and adaptive MCMC. Handbook of Markov Chain Monte Carlo, 4(10.1201).
   
   [4] Peters, B., Janek, K., Kuckelkorn, U., Holzh<span>ü</span>tter, H.-G. (2002). Assessment of proteasomal cleavage probabilities from kinetic analysis of time-dependent product formation, Journal of molecular biology, 318(3), 847-862.
  
  ## LICENSE
  
  This project is licensed under the GNU General Public License v3.0 - see the [LICENSE.md](LICENSE.md) file for details.
  
  
  
<!-- Markdown link & img dfn's -->
[bayestat-url]: https://en.wikipedia.org/wiki/Bayesian_inference
[peptide-url]: https://en.wikipedia.org/wiki/Peptide
[massspec-url]: https://en.wikipedia.org/wiki/Mass_spectrometry
[proteo-url]: https://en.wikipedia.org/wiki/Proteomics
