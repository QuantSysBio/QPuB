## QPuB - Quantification of peptide using Bayesian inference

   QPuB employs Bayesian statistical inference based on Markov chain Monte Carlo (MCMC) sampling to learn the posterior distributions of the converison factors for peptide products. 
   
* **Execution**

  In order to run QPuB, users are strongly advised to install **R** with version **3.5.0** or above along with the dependencies mentioned below.  
  
 Run the QPuB using two simple steps as follows:
 * manually download the package and extract the .zip file in your local computer
 * after changing the working directory to **QPuB** sub-folder, run the following command from the terminal 
    
    ```R     
       Rscript runQPuB.r -fol <INPUT FOLDER> -pf input.txt -tim <file contains timepoints> -titr <file contains titration>
   ```
* **Examples**
  
     The **examples** folder contains two toy examples of endopeptidase digestion. 
      
     In order to run the examples, execute the following command for a date without noise 
      
     ```R
      Rscript runQPuB.r -fol examples/toy_endo3_nonoise -pf input.txt 
     ```
     and 
     
     ```R
      Rscript runQPuB.r -fol examples/toy_endo3_nonoise -pf input.txt 
     ```
     for the data with noise 
     [GitHub](http://github.com)
     
 *  **Output**
 
    1. **boxplot\_chain.pdf** &nbsp; boxplot corresponding to the distributions of conversion factors  
	 
    2.	**chain\_XYZ.RData**   &nbsp; stores trace of the Markov chain or the time series of the parameter draws  
			
    3.	**chain\_backscaled.RData** &nbsp;   stores the Markov chain after dividing the products by the scaling factor pre-calculated according to the substrate concentration     
	 
    4.   **conc\_means\_Nrep.csv, conc\_sd\_Nrep.csv** &nbsp; means and standard deviations of absolute concentrations of the products at different time points for the **Nrep** replicate, respectively  
	
    5.	**massdeviation.png** &nbsp; plot of total mass deviation of the products over Monte Carlo iterations                                                                                                   
 
    6.	**massdev.RData**  &nbsp;  stores mass deviation of the products over Monte Carlo iterations   
 
    7.	**relation.png**   &nbsp; plot of relation between the estimated conversion factors and the peptide lengths                                                                                          
 
    8.  **runQPuB\_ROUT.txt** &nbsp; contains the initial parameters that were feed to the algorithm and acceptance rates as the chain progresses. The output of any print command directly goes into the file. 
 
    9.	**chain\_Niter.pdf**   &nbsp; trace plots of the Markov chain at **Niter** iteration   
 
    10. **residuals\_M.txt**   &nbsp; residual plot at **M** iteration. The plot display mass deviation for individual amino acids of the substrate
    
    11. **statistics.csv**    &nbsp; summary statistic for the Markov chain  
      
    
 * **Dependencies**
 
   1.  **R.utils** for processing the command line arguments.
   
   2. **tictoc** provides timing function
   
   3. **mcmcse** to compute the effective sample size.
   
   4. **tmvtnorm**  to generate the truncated multivariate normal distri-
bution.
   5. **corpcor** to make a matrix postive definite. 
   
   6. **dqRNGkind** to generate fast pseudo random numbers.
   
   7. **coda** to produce an mcmc object for further anaylsis of the
Markov chain.

   8. **base** to execute Base R functions

   9. **matrixcalc** to check whether a matrix is positive definite or not

   10. **ggdmc** to generate univariate truncated normal distributon.

   11. **grDevices** for cairo pdf.

   12. **matrixStats** to compute standard deviation of columns of a ma-
trix.

 * **Documentation**
 
     In progress 

