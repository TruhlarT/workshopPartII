# star-upcDst template

![Bilby Stampede](https://cds.cern.ch/record/2288105/files/fig1.png)

## Overview:
repository contains a template of an analysis using *star-upcDst*, a framework to simplify analysis that are related to forward and UPC physics. 

- Make a clean area on RACF and checkout the repository:

<pre><code> git clone https://github.com/adamjaro/star-upcDst.git </pre></code>

- Go to the main directory ana_partII:

<pre><code> cd ana_partII </pre></code>

- Setup the StRoot and build ( already include compiling ) by doing:

<pre><code> ./build-maker.sh </pre></code>

- With "test.root", the upcDst file, as the input, one can perform simple analysis or run over all events to save information into a tree or histograms. To do that, one needs to compile the package and setup the link to the library. This can be simply done in a few steps:

In build directory, create executable file of the analysis template "Ana",

<pre><code> cd build </code></pre>
<pre><code> cmake ../ </code></pre>
<pre><code> make </code></pre>

Done. To try an example, go to folder "examples":

<pre><code> cd ../examples </code></pre>

and remember to change the input file name to what has been just created, "test.root", for macro "make_pT.C". Then do, 

<pre><code> root -l run_make_pT.C </code></pre>


- For another example, it uses a C++ code (with ROOT libraries) to read the picoDst file and save output into a small ROOT tree or anything one wants to save. Instead of running it as a .C ROOT macro, this example build an executable and can run as a standard C++ code without using ROOT.

Again, under the main directory, 

<pre><code> cd ./examples/dstreader </code></pre>

make another directory for build,

<pre><code> mkdir build </code></pre>

before one compiles the code, the input file needs to be modified accordingly in "./examples/dstreader/src/AnalysisTemplate.cxx". Again, change it to the "test.root" that has just been created, then go back to directory for build,


<pre><code> cd build </code></pre>
<pre><code> cmake ../ </code></pre>
<pre><code> make </code></pre>

The executable will show up as "Ana", now run it:

<pre><code> ./Ana pathToRootFile </code></pre>

It produces an output, "AnalysisOutput.root". 

To run over all data, run: 

<pre><code> ./SubmitPlugin.py outputDir inputSource  </code></pre>

One can check the job status (you can just do condor_q or) using "PrintStat.py":

<pre><code> PrintStat.py -c  </pre></code>

Or one can check the job status and also resubmit failed jobs:

<pre><code> PrintStat.py -r -c </pre></code>

PS: -r has to be first then -c.

Finally, merge the outpus of all jobs into one (or few) root files:

<pre><code> ./RunMerge.py </pre></code>

## Contact:
Tomas Truhlar: <Tomas.Truhlar@fjfi.cvut.cz>








