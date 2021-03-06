CRAN Task View: High-Performance and Parallel Computing with R
--------------------------------------------------------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>Maintainer:</strong>
Dirk Eddelbuettel</td>
<td align="left"><strong>Contact:</strong>
Dirk.Eddelbuettel at R-project.org</td>
</tr>
</tbody>
</table>

This CRAN task view contains a list of packages, grouped by topic, that are useful for high-performance computing (HPC) with R. In this context, we are defining 'high-performance computing' rather loosely as just about anything related to pushing R a little further: using compiled code, parallel computing (in both explicit and implicit modes), working with large objects as well as profiling.

Unless otherwise mentioned, all packages presented with hyperlinks are available from CRAN, the Comprehensive R Archive Network.

Several of the areas discussed in this Task View are undergoing rapid change. Please send suggestions for additions and extensions for this task view to the [task view maintainer](mailto:Dirk.Eddelbuettel@R-project.org).

Suggestions and corrections by Achim Zeileis, Markus Schmidberger, Martin Morgan, Max Kuhn, Tomas Radivoyevitch, Jochen Knaus, Tobias Verbeke, Hao Yu, David Rosenberg, Marco Enea, Ivo Welch, Jay Emerson, Wei-Chen Chen, Bill Cleveland, Ross Boylan, and Ramon Diaz-Uriarte (as well as others I may have forgotten to add here) are gratefully acknowledged.

Contributions are always welcome, and encouraged. Since the start of this CRAN task view in October 2008, most contributions have arrived as email suggestions. The source file for this particular task view file now also reside in a GitHub repository (see below) so that pull requests are also possible.

**Direct support in R started with release 2.14.0** which includes a new package **parallel** incorporating (slightly revised) copies of packages multicore and [snow](http://cran.rstudio.com/web/packages/snow/index.html). Some types of clusters are not handled directly by the base package 'parallel'. However, and as explained in the package vignette, the parts of parallel which provide [snow](http://cran.rstudio.com/web/packages/snow/index.html) -like functions will accept [snow](http://cran.rstudio.com/web/packages/snow/index.html) clusters including MPI clusters.
 The **parallel** package also contains support for multiple RNG streams following L'Ecuyer et al (2002), with support for both mclapply and snow clusters.
 The version released for R 2.14.0 contains base functionality: higher-level convenience functions are planned for later R releases.

**Parallel computing: Explicit parallelism**

-   Several packages provide the communications layer required for parallel computing. The first package in this area was rpvm by Li and Rossini which uses the PVM (Parallel Virtual Machine) standard and libraries. rpvm is no longer actively maintained, but available from its CRAN archive directory.
-   In recent years, the alternative MPI (Message Passing Interface) standard has become the de facto standard in parallel computing. It is supported in R via the [Rmpi](http://cran.rstudio.com/web/packages/Rmpi/index.html) by Yu. [Rmpi](http://cran.rstudio.com/web/packages/Rmpi/index.html) package is mature yet actively maintained and offers access to numerous functions from the MPI API, as well as a number of R-specific extensions. [Rmpi](http://cran.rstudio.com/web/packages/Rmpi/index.html) can be used with the LAM/MPI, MPICH / MPICH2, Open MPI, and Deino MPI implementations. It should be noted that LAM/MPI is now in maintenance mode, and new development is focussed on Open MPI.
-   The [pbdMPI](http://cran.rstudio.com/web/packages/pbdMPI/index.html) package provides S4 classes to directly interface MPI in order to support the Single Program/Multiple Data (SPMD) parallel programming style which is particularly useful for batch parallel execution. The [pbdSLAP](http://cran.rstudio.com/web/packages/pbdSLAP/index.html) builds on this and uses scalable linear algebra packages (namely BLACS, PBLAS, and ScaLAPACK) in double precision based on ScaLAPACK version 2.0.2. The [pbdBASE](http://cran.rstudio.com/web/packages/pbdBASE/index.html) builds on these and provides the core classes and methods for distributed data types upon which the [pbdDMAT](http://cran.rstudio.com/web/packages/pbdDMAT/index.html) builds to provide distributed dense matrices for "Programming with Big Data". The [pbdNCDF4](http://cran.rstudio.com/web/packages/pbdNCDF4/index.html) package permits multiple processes to write to the same file (without manual synchronization) and supports terabyte-sized files. The [pbdDEMO](http://cran.rstudio.com/web/packages/pbdDEMO/index.html) package provides examples for these packages, and a detailed vignette. The [pbdPROF](http://cran.rstudio.com/web/packages/pbdPROF/index.html) package profiles MPI communication SPMD code via MPI profiling libraries, such as fpmpi, mpiP, or TAU.
-   An alternative is provided by the [nws](http://cran.rstudio.com/web/packages/nws/index.html) (NetWorkSpaces) packages from REvolution Computing. It is the successor to the earlier LindaSpaces approach to parallel computing, and is implemented on top of the Twisted networking toolkit for Python.
-   The [snow](http://cran.rstudio.com/web/packages/snow/index.html) (Simple Network of Workstations) package by Tierney et al. can use PVM, MPI, NWS as well as direct networking sockets. It provides an abstraction layer by hiding the communications details. The [snowFT](http://cran.rstudio.com/web/packages/snowFT/index.html) package provides fault-tolerance extensions to [snow](http://cran.rstudio.com/web/packages/snow/index.html).
-   The [snowfall](http://cran.rstudio.com/web/packages/snowfall/index.html) package by Knaus provides a more recent alternative to [snow](http://cran.rstudio.com/web/packages/snow/index.html). Functions can be used in sequential or parallel mode.
-   The [biopara](http://cran.rstudio.com/web/packages/biopara/index.html) package by Lazar and Schoenfeld offers socket-based parallel execution with some support for load-balancing and fault-tolerance.
-   The [foreach](http://cran.rstudio.com/web/packages/foreach/index.html) package allows general iteration over elements in a collection without the use of an explicit loop counter. Using foreach without side effects also facilitates executing the loop in parallel which is possible via the [doMC](http://cran.rstudio.com/web/packages/doMC/index.html) (using parallel/multicore on single workstations), [doSNOW](http://cran.rstudio.com/web/packages/doSNOW/index.html) (using [snow](http://cran.rstudio.com/web/packages/snow/index.html), see above), [doMPI](http://cran.rstudio.com/web/packages/doMPI/index.html) (using [Rmpi](http://cran.rstudio.com/web/packages/Rmpi/index.html)) packages and [doRedis](http://cran.rstudio.com/web/packages/doRedis/index.html) (using [rredis](http://cran.rstudio.com/web/packages/rredis/index.html)) packages.
-   The [bigrf](http://cran.rstudio.com/web/packages/bigrf/index.html) package provides a Random Forests implementation with support for parellel execution and large memory.

**Parallel computing: Implicit parallelism**

-   The pnmath package by Tierney ( [link](http://www.stat.uiowa.edu/~luke/R/experimental/)) uses the Open MP parallel processing directives of recent compilers (such gcc 4.2 or later) for implicit parallelism by replacing a number of internal R functions with replacements that can make use of multiple cores --- without any explicit requests from the user. The alternate pnmath0 package offers the same functionality using Pthreads for environments in which the newer compilers are not available. Similar functionality is expected to become integrated into R 'eventually'.
-   The romp package by Jamitzky was presented at useR! 2008 ( [slides](http://www.statistik.tu-dortmund.de/useR-2008/slides/Jamitzky.pdf)) and offers another interface to Open MP using Fortran. The code is still pre-alpha and available from the Google Code project [romp](http://code.google.com/p/romp/). An R-Forge project [romp](http://R-Forge.R-project.org/projects/romp/) was initiated but there is no package, yet.
-   The R/parallel package by Vera, Jansen and Suppi offers a C++-based master-slave dispatch mechanism for parallel execution ( [link](http://www.rparallel.org/))
-   The [Rdsm](http://cran.rstudio.com/web/packages/Rdsm/index.html) package provides a threads-like parallel computing environment, both on multicore machine and across the network by providing facilities inspired from distributed shared memory programming.
-   The [RhpcBLASctl](http://cran.rstudio.com/web/packages/RhpcBLASctl/index.html) detects the number of available BLAS cores, and permits explicit selection of the number of cores.
-   The [Rhpc](http://cran.rstudio.com/web/packages/Rhpc/index.html) permits `*apply()` style dispatch via MPI.

**Parallel computing: Grid computing**

-   The multiR package by Grose was presented at useR! 2008 but has not been released. It may offer a snow-style framework on a grid computing platform.
-   The [biocep-distrib](http://R-Forge.R-project.org/projects/biocep-distrib/) project by Chine offers a Java-based framework for local, Grid, or Cloud computing. It is under active development.

**Parallel computing: Hadoop**

-   The RHIPE package, started by Saptarshi Guha and now developed by a core team via GitHub, provides an interface between R and Hadoop for analysis of large complex data wholly from within R using the Divide and Recombine approach to big data. ( [link](http://www.datadr.org))
-   The rmr package by Revolution Analytics also provides an interface between R and Hadoop for a Map/Reduce programming framework. ( [link](https://github.com/RevolutionAnalytics/RHadoop/wiki/rmr))
-   A related package, segue package by Long, permits easy execution of embarassingly parallel task on Elastic Map Reduce (EMR) at Amazon. ( [link](http://code.google.com/p/segue/))
-   The [RProtoBuf](http://cran.rstudio.com/web/packages/RProtoBuf/index.html) package provides an interface to Google's language-neutral, platform-neutral, extensible mechanism for serializing structured data. This package can be used in R code to read data streams from other systems in a distributed MapReduce setting where data is serialized and passed back and forth between tasks.
-   The [HistogramTools](http://cran.rstudio.com/web/packages/HistogramTools/index.html) package provides a number of routines useful for the construction, aggregation, manipulation, and plotting of large numbers of Histograms such as those created by Mappers in a MapReduce application.

**Parallel computing: Random numbers**

-   Random-number generators for parallel computing are available via the [rlecuyer](http://cran.rstudio.com/web/packages/rlecuyer/index.html) package by Sevcikova and Rossini.
-   The [doRNG](http://cran.rstudio.com/web/packages/doRNG/index.html) package provides functions to perform reproducible parallel foreach loops, using independent random streams as generated by the package rstream, suitable for the different foreach backends.

**Parallel computing: Resource managers and batch schedulers**

-   Job-scheduling toolkits permit management of parallel computing resources and tasks. The slurm (Simple Linux Utility for Resource Management) set of programs (written by a consortium led by Lawrence Livermore Labs) works well with MPI. ( [link](https://slurm.schedmd.com/))
-   The Condor toolkit ( [link](http://www.cs.wisc.edu/condor/)) from the University of Wisconsin-Madison has been used with R as described in this [R News article](http://www.r-project.org/doc/Rnews/Rnews_2005-2.pdf).
-   The sfCluster package by Knaus can be used with [snowfall](http://cran.rstudio.com/web/packages/snowfall/index.html). ( [link](http://www.imbi.uni-freiburg.de/parallel/)) but is currently limited to LAM/MPI.
-   The [batch](http://cran.rstudio.com/web/packages/batch/index.html) package by Hoffmann can launch parallel computing requests onto a cluster and gather results.
-   The [BatchJobs](http://cran.rstudio.com/web/packages/BatchJobs/index.html) package provides Map, Reduce and Filter variants to manage R jobs and their results on batch computing systems like PBS/Torque, LSF and Sun Grid Engine. Multicore and SSH systems are also supported. The [BatchExperiments](http://cran.rstudio.com/web/packages/BatchExperiments/index.html) package extends it with an abstraction layer for running statistical experiments.

**Parallel computing: Applications**

-   The [caret](http://cran.rstudio.com/web/packages/caret/index.html) package by Kuhn can use various frameworks (MPI, NWS etc) to parallelized cross-validation and bootstrap characterizations of predictive models.
-   The [maanova](http://www.Bioconductor.ohttp://cran.rstudio.com/web/packages/release/bioc/html/maanova.html) package on Bioconductor by Wu can use [snow](http://cran.rstudio.com/web/packages/snow/index.html) and [Rmpi](http://cran.rstudio.com/web/packages/Rmpi/index.html) for the analysis of micro-array experiments.
-   The [pvclust](http://cran.rstudio.com/web/packages/pvclust/index.html) package by Suzuki and Shimodaira can use [snow](http://cran.rstudio.com/web/packages/snow/index.html) and [Rmpi](http://cran.rstudio.com/web/packages/Rmpi/index.html) for hierarchical clustering via multiscale bootstraps.
-   The [tm](http://cran.rstudio.com/web/packages/tm/index.html) package by Feinerer can use [snow](http://cran.rstudio.com/web/packages/snow/index.html) and [Rmpi](http://cran.rstudio.com/web/packages/Rmpi/index.html) for parallelized text mining.
-   The [varSelRF](http://cran.rstudio.com/web/packages/varSelRF/index.html) package by Diaz-Uriarte can use [snow](http://cran.rstudio.com/web/packages/snow/index.html) and [Rmpi](http://cran.rstudio.com/web/packages/Rmpi/index.html) for parallelized use of variable selection via random forests.
-   The [bcp](http://cran.rstudio.com/web/packages/bcp/index.html) package by Erdman and Emerson for the Bayesian analysis of change points can use [foreach](http://cran.rstudio.com/web/packages/foreach/index.html) for parallelized operations.
-   The [multtest](http://www.Bioconductor.ohttp://cran.rstudio.com/web/packages/release/bioc/html/multtest.html) package by Pollard et al. on Bioconductor can use [snow](http://cran.rstudio.com/web/packages/snow/index.html), [Rmpi](http://cran.rstudio.com/web/packages/Rmpi/index.html) or rpvm for resampling-based testing of multiple hypothesis.
-   The [GAMBoost](http://cran.rstudio.com/web/packages/GAMBoost/index.html) package by Binder for `glm` and `gam` model fitting via boosting using b-splines, the [Geneland](http://cran.rstudio.com/web/packages/Geneland/index.html) package by Estoup, Guillot and Santos for structure detection from multilocus genetic data, the [Matching](http://cran.rstudio.com/web/packages/Matching/index.html) package by Sekhon for multivariate and propensity score matching, the [STAR](http://cran.rstudio.com/web/packages/STAR/index.html) package by Pouzat for spike train analysis, the [bnlearn](http://cran.rstudio.com/web/packages/bnlearn/index.html) package by Scutari for bayesian network structure learning, the [latentnet](http://cran.rstudio.com/web/packages/latentnet/index.html) package by Krivitsky and Handcock for latent position and cluster models, the [lga](http://cran.rstudio.com/web/packages/lga/index.html) package by Harrington for linear grouping analysis, the [peperr](http://cran.rstudio.com/web/packages/peperr/index.html) package by Porzelius and Binder for parallised estimation of prediction error, the [orloca](http://cran.rstudio.com/web/packages/orloca/index.html) package by Fernandez-Palacin and Munoz-Marquez for operations research locational analysis, the [rgenoud](http://cran.rstudio.com/web/packages/rgenoud/index.html) package by Mebane and Sekhon for genetic optimization using derivatives the [affyPara](http://www.Bioconductor.ohttp://cran.rstudio.com/web/packages/release/bioc/html/affyPara.html) package by Schmidberger, Vicedo and Mansmann for parallel normalization of Affymetrix microarrays, and the [puma](http://www.Bioconductor.ohttp://cran.rstudio.com/web/packages/release/bioc/html/puma.html) package by Pearson et al. which propagates uncertainty into standard microarray analyses such as differential expression all can use [snow](http://cran.rstudio.com/web/packages/snow/index.html) for parallelized operations using either one of the MPI, PVM, NWS or socket protocols supported by [snow](http://cran.rstudio.com/web/packages/snow/index.html).
-   The [bugsparallel](http://code.google.com/p/bugsparallel/) package uses [Rmpi](http://cran.rstudio.com/web/packages/Rmpi/index.html) for distributed computing of multiple MCMC chains using WinBUGS.
-   The [dclone](http://cran.rstudio.com/web/packages/dclone/index.html) package provides a global optimization approach and a variant of simulated annealing which exploits Bayesian MCMC tools to get MLE point estimates and standard errors using low level functions for implementing maximum likelihood estimating procedures for complex models using data cloning and Bayesian Markov chain Monte Carlo methods with support for JAGS, WinBUGS and OpenBUGS; parallel computing is supported via the [snow](http://cran.rstudio.com/web/packages/snow/index.html) package.
-   The [pmclust](http://cran.rstudio.com/web/packages/pmclust/index.html) package utilizes unsupervised model-based clustering for high dimensional (ultra) large data. The package uses [pbdMPI](http://cran.rstudio.com/web/packages/pbdMPI/index.html) to perform a parallel version of the EM algorithm for finite mixture Gaussian models.
-   The [harvestr](http://cran.rstudio.com/web/packages/harvestr/index.html) package provides helper functions for (reproducible) simulations.
-   Nowadays, many packages can use the facilities offered by the **parallel** package. One example is [pls](http://cran.rstudio.com/web/packages/pls/index.html), another is [PGICA](http://cran.rstudio.com/web/packages/PGICA/index.html) which can run ICA analysis in parallel on SGE or multicore platforms.

**Parallel computing: GPUs**

-   The [gputools](http://cran.rstudio.com/web/packages/gputools/index.html) package by Buckner and Seligman provides several common data-mining algorithms which are implemented using a mixture of nVidia's CUDA langauge and cublas library. Given a computer with an nVidia GPU these functions may be substantially more efficient than native R routines. The [rpud](http://cran.rstudio.com/web/packages/rpud/index.html) package provides an optimised distance metric for NVidia-based GPUs.
-   The [cudaBayesreg](http://cran.rstudio.com/web/packages/cudaBayesreg/index.html) package by da Silva implements the `rhierLinearModel` from the [bayesm](http://cran.rstudio.com/web/packages/bayesm/index.html) package using nVidia's CUDA langauge and tools to provide high-performance statistical analysis of fMRI voxels.
-   The rgpu package (see below for link) aims to speed up bioinformatics analysis by using the GPU.
-   The [magma](http://cran.rstudio.com/web/packages/magma/index.html) package provides an interface to the hybrid GPU/CPU library Magma (see below for link).
-   The [gcbd](http://cran.rstudio.com/web/packages/gcbd/index.html) package implements a benchmarking framework for BLAS and GPUs (using [gputools](http://cran.rstudio.com/web/packages/gputools/index.html)).
-   The [OpenCL](http://cran.rstudio.com/web/packages/OpenCL/index.html) package provides an interface from R to OpenCL permitting hardware- and vendor neutral interfaces to GPU programming.
-   The [WideLM](http://cran.rstudio.com/web/packages/WideLM/index.html) package use CUDA (4.1 or greater) to fit many 'skinny' regression models simultaneously from a single data set.
-   The [HiPLARM](http://cran.rstudio.com/web/packages/HiPLARM/index.html) package provide High-Performance Linear Algebra for R using multi-core and/or GPU support using the PLASMA / MAGMA libraries from UTK, CUDA, and accelerated BLAS.
-   The [permGPU](http://cran.rstudio.com/web/packages/permGPU/index.html) package computes permutation resampling inference in the context of RNA microarray studies on the GPU, it uses CUDA (\>= 4.5)

**Large memory and out-of-memory data**

-   The [biglm](http://cran.rstudio.com/web/packages/biglm/index.html) package by Lumley uses incremental computations to offer `lm()` and `glm()` functionality to data sets stored outside of R's main memory.
-   The [ff](http://cran.rstudio.com/web/packages/ff/index.html) package by Adler et al. offers file-based access to data sets that are too large to be loaded into memory, along with a number of higher-level functions.
-   The [bigmemory](http://cran.rstudio.com/web/packages/bigmemory/index.html) package by Kane and Emerson permits storing large objects such as matrices in memory (as well as via files) and uses external pointer objects to refer to them. This permits transparent access from R without bumping against R's internal memory limits. Several R processes on the same computer can also share big memory objects.
-   A large number of database packages, and database-alike packages (such as [sqldf](http://cran.rstudio.com/web/packages/sqldf/index.html) by Grothendieck and [data.table](http://cran.rstudio.com/web/packages/data.table/index.html) by Dowle) are also of potential interest but not reviewed here.
-   The [HadoopStreaming](http://cran.rstudio.com/web/packages/HadoopStreaming/index.html) package provides a framework for writing map/reduce scripts for use in Hadoop Streaming; it also facilitates operating on data in a streaming fashion which does not require Hadoop.
-   The [speedglm](http://cran.rstudio.com/web/packages/speedglm/index.html) package permits to fit (generalised) linear models to large data. For in-memory data sets, speedlm() or speedglm() can be used along with update.speedlm() which can update fitted models with new data. For out-of-memory data sets, shglm() is available; it works in the presence of factors and can check for singular matrices.
-   The [biglars](http://cran.rstudio.com/web/packages/biglars/index.html) package by Seligman et al can use the [ff](http://cran.rstudio.com/web/packages/ff/index.html) to support large-than-memory datasets for least-angle regression, lasso and stepwise regression.
-   The [bigrf](http://cran.rstudio.com/web/packages/bigrf/index.html) package provides a Random Forests implementation with support for parellel execution and large memory.
-   The [MonetDB.R](http://cran.rstudio.com/web/packages/MonetDB.R/index.html) package allows R to access the MonetDB column-oriented, open source database system as a backend.
-   The [ffbase](http://cran.rstudio.com/web/packages/ffbase/index.html) package by de Jonge et al adds basic statistical functionality to the [ff](http://cran.rstudio.com/web/packages/ff/index.html) package.

**Easier interfaces for Compiled code**

-   The [inline](http://cran.rstudio.com/web/packages/inline/index.html) package by Sklyar et al eases adding code in C, C++ or Fortran to R. It takes care of the compilation, linking and loading of embeded code segments that are stored as R strings.
-   The [Rcpp](http://cran.rstudio.com/web/packages/Rcpp/index.html) package by Eddelbuettel and Francois offers a number of C++ clases that makes transferring R objects to C++ functions (and back) easier, and the [RInside](http://cran.rstudio.com/web/packages/RInside/index.html) package by the same authors allows easy embedding of R itself into C++ applications for faster and more direct data transfer.
-   The [rJava](http://cran.rstudio.com/web/packages/rJava/index.html) package by Urbanek provides a low-level interface to Java similar to the `.Call()` interface for C and C++.

**Profiling tools**

-   The [profr](http://cran.rstudio.com/web/packages/profr/index.html) package by Wickham can visualize output from the `Rprof` interface for profiling.
-   The [proftools](http://cran.rstudio.com/web/packages/proftools/index.html) package by Tierney, and the [aprof](http://cran.rstudio.com/web/packages/aprof/index.html) package by Visser, can also be used to analyse profiling output.
-   The [GUIProfiler](http://cran.rstudio.com/web/packages/GUIProfiler/index.html) package visualizes the results of profiling R programs.

### CRAN packages:

-   [aprof](http://cran.rstudio.com/web/packages/aprof/index.html)
-   [batch](http://cran.rstudio.com/web/packages/batch/index.html)
-   [BatchExperiments](http://cran.rstudio.com/web/packages/BatchExperiments/index.html)
-   [BatchJobs](http://cran.rstudio.com/web/packages/BatchJobs/index.html)
-   [bayesm](http://cran.rstudio.com/web/packages/bayesm/index.html)
-   [bcp](http://cran.rstudio.com/web/packages/bcp/index.html)
-   [biglars](http://cran.rstudio.com/web/packages/biglars/index.html)
-   [biglm](http://cran.rstudio.com/web/packages/biglm/index.html)
-   [bigmemory](http://cran.rstudio.com/web/packages/bigmemory/index.html)
-   [bigrf](http://cran.rstudio.com/web/packages/bigrf/index.html)
-   [biopara](http://cran.rstudio.com/web/packages/biopara/index.html)
-   [bnlearn](http://cran.rstudio.com/web/packages/bnlearn/index.html)
-   [caret](http://cran.rstudio.com/web/packages/caret/index.html)
-   [cudaBayesreg](http://cran.rstudio.com/web/packages/cudaBayesreg/index.html)
-   [data.table](http://cran.rstudio.com/web/packages/data.table/index.html)
-   [dclone](http://cran.rstudio.com/web/packages/dclone/index.html)
-   [doMC](http://cran.rstudio.com/web/packages/doMC/index.html)
-   [doMPI](http://cran.rstudio.com/web/packages/doMPI/index.html)
-   [doRedis](http://cran.rstudio.com/web/packages/doRedis/index.html)
-   [doRNG](http://cran.rstudio.com/web/packages/doRNG/index.html)
-   [doSNOW](http://cran.rstudio.com/web/packages/doSNOW/index.html)
-   [ff](http://cran.rstudio.com/web/packages/ff/index.html)
-   [ffbase](http://cran.rstudio.com/web/packages/ffbase/index.html)
-   [foreach](http://cran.rstudio.com/web/packages/foreach/index.html)
-   [GAMBoost](http://cran.rstudio.com/web/packages/GAMBoost/index.html)
-   [gcbd](http://cran.rstudio.com/web/packages/gcbd/index.html)
-   [Geneland](http://cran.rstudio.com/web/packages/Geneland/index.html)
-   [gputools](http://cran.rstudio.com/web/packages/gputools/index.html)
-   [GUIProfiler](http://cran.rstudio.com/web/packages/GUIProfiler/index.html)
-   [HadoopStreaming](http://cran.rstudio.com/web/packages/HadoopStreaming/index.html)
-   [harvestr](http://cran.rstudio.com/web/packages/harvestr/index.html)
-   [HiPLARM](http://cran.rstudio.com/web/packages/HiPLARM/index.html)
-   [HistogramTools](http://cran.rstudio.com/web/packages/HistogramTools/index.html)
-   [inline](http://cran.rstudio.com/web/packages/inline/index.html)
-   [latentnet](http://cran.rstudio.com/web/packages/latentnet/index.html)
-   [lga](http://cran.rstudio.com/web/packages/lga/index.html)
-   [magma](http://cran.rstudio.com/web/packages/magma/index.html)
-   [Matching](http://cran.rstudio.com/web/packages/Matching/index.html)
-   [MonetDB.R](http://cran.rstudio.com/web/packages/MonetDB.R/index.html)
-   [nws](http://cran.rstudio.com/web/packages/nws/index.html)
-   [OpenCL](http://cran.rstudio.com/web/packages/OpenCL/index.html)
-   [orloca](http://cran.rstudio.com/web/packages/orloca/index.html)
-   [pbdBASE](http://cran.rstudio.com/web/packages/pbdBASE/index.html)
-   [pbdDEMO](http://cran.rstudio.com/web/packages/pbdDEMO/index.html)
-   [pbdDMAT](http://cran.rstudio.com/web/packages/pbdDMAT/index.html)
-   [pbdMPI](http://cran.rstudio.com/web/packages/pbdMPI/index.html)
-   [pbdNCDF4](http://cran.rstudio.com/web/packages/pbdNCDF4/index.html)
-   [pbdPROF](http://cran.rstudio.com/web/packages/pbdPROF/index.html)
-   [pbdSLAP](http://cran.rstudio.com/web/packages/pbdSLAP/index.html)
-   [peperr](http://cran.rstudio.com/web/packages/peperr/index.html)
-   [permGPU](http://cran.rstudio.com/web/packages/permGPU/index.html)
-   [PGICA](http://cran.rstudio.com/web/packages/PGICA/index.html)
-   [pls](http://cran.rstudio.com/web/packages/pls/index.html)
-   [pmclust](http://cran.rstudio.com/web/packages/pmclust/index.html)
-   [profr](http://cran.rstudio.com/web/packages/profr/index.html)
-   [proftools](http://cran.rstudio.com/web/packages/proftools/index.html)
-   [pvclust](http://cran.rstudio.com/web/packages/pvclust/index.html)
-   [Rcpp](http://cran.rstudio.com/web/packages/Rcpp/index.html)
-   [Rdsm](http://cran.rstudio.com/web/packages/Rdsm/index.html)
-   [rgenoud](http://cran.rstudio.com/web/packages/rgenoud/index.html)
-   [Rhpc](http://cran.rstudio.com/web/packages/Rhpc/index.html)
-   [RhpcBLASctl](http://cran.rstudio.com/web/packages/RhpcBLASctl/index.html)
-   [RInside](http://cran.rstudio.com/web/packages/RInside/index.html)
-   [rJava](http://cran.rstudio.com/web/packages/rJava/index.html)
-   [rlecuyer](http://cran.rstudio.com/web/packages/rlecuyer/index.html)
-   [Rmpi](http://cran.rstudio.com/web/packages/Rmpi/index.html) (core)
-   [RProtoBuf](http://cran.rstudio.com/web/packages/RProtoBuf/index.html)
-   [rpud](http://cran.rstudio.com/web/packages/rpud/index.html)
-   [rredis](http://cran.rstudio.com/web/packages/rredis/index.html)
-   [snow](http://cran.rstudio.com/web/packages/snow/index.html) (core)
-   [snowfall](http://cran.rstudio.com/web/packages/snowfall/index.html)
-   [snowFT](http://cran.rstudio.com/web/packages/snowFT/index.html)
-   [speedglm](http://cran.rstudio.com/web/packages/speedglm/index.html)
-   [sqldf](http://cran.rstudio.com/web/packages/sqldf/index.html)
-   [STAR](http://cran.rstudio.com/web/packages/STAR/index.html)
-   [tm](http://cran.rstudio.com/web/packages/tm/index.html)
-   [varSelRF](http://cran.rstudio.com/web/packages/varSelRF/index.html)
-   [WideLM](http://cran.rstudio.com/web/packages/WideLM/index.html)

### Related links:

-   [HPC computing notes by Luke Tierney for HPC class at University of Iowa](http://www.stat.uiowa.edu/~luke/classes/295-hpc/)
-   [Mailing List: R Special Interest Group High Performance Computing](https://stat.ethz.ch/mailman/listinfo/r-sig-hpc/)
-   [Schmidberger, Morgan, Eddelbuettel, Yu, Tierney and Mansmann (2009) paper on 'State of the Art in Parallel Computing with R'](http://www.jstatsoft.org/v31/i01/)
-   [Luke Tierney's code directory for pnmath and pnmath0](http://www.stat.uiowa.edu/~luke/R/experimental/)
-   R-Forge Project: [biocep-distrib](http://R-Forge.R-project.org/projects/biocep-distrib/)
-   Bioconductor Package: [affyPara](http://www.Bioconductor.ohttp://cran.rstudio.com/web/packages/release/bioc/html/affyPara.html)
-   Bioconductor Package: [maanova](http://www.Bioconductor.ohttp://cran.rstudio.com/web/packages/release/bioc/html/maanova.html)
-   Bioconductor Package: [multtest](http://www.Bioconductor.ohttp://cran.rstudio.com/web/packages/release/bioc/html/multtest.html)
-   Bioconductor Package: [puma](http://www.Bioconductor.ohttp://cran.rstudio.com/web/packages/release/bioc/html/puma.html)
-   Google Code Project: [romp](http://code.google.com/p/romp/)
-   Google Code Project: [bugsparallel](http://code.google.com/p/bugsparallel/)
-   [Slurm project at Lawrence Livermore National Laboratory](https://computing.llnl.gov/linux/slurm/)
-   [Condor project at University of Wisconsin-Madison](http://www.cs.wisc.edu/condor/)
-   [Parallel Computing in R with sfCluster/snowfall](http://www.imbi.uni-freiburg.de/parallel/)
-   [Wikipedia: Message Passing Interface (MPI)](http://en.wikipedia.org/wiki/Message_Passing_Interface)
-   [Wikipedia: Parallel Virtual Machine (PVM)](http://en.wikipedia.org/wiki/Parallel_Virtual_Machine)
-   [Slides from Introduction to High-Performance Computing with R tutorial help in Nov 2009 at the Institute for Statistical Mathematics, Tokyo, Japan](http://dirk.eddelbuettel.com/papers/ismNov2009introHPCwithR.pdf)
-   [rgpu project at nbic.nl](https://gforge.nbic.nl/projects/rgpu/)
-   [Magma: Matrix Algebra on GPU and Multicore architectures](http://icl.cs.utk.edu/magma/)
-   [Parallel R: Data Analysis in the Distributed World"](http://shop.oreilly.com/product/0636920021421.do)
-   [High Performance Statistical Computing for Data Intensive Research](http://thirteen-01.stat.iastate.edu/snoweye/hpsc/)
-   [Rth: Parallel R through Thrust](http://heather.cs.ucdavis.edu/~matloff/rth.html)
-   [Programming with Big Data in R](http://r-pbd.org)
-   [RHIPE](http://www.datadr.org)
-   [LaplacesDemon](http://www.bayesian-inference.com/software)
-   [GitHub repository for this Task View](https://github.com/eddelbuettel/ctv-hpc)
