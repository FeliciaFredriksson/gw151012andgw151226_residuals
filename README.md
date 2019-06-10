# Investigating the residuals from gravitational wave event GW151012 and GW151226
The following script is based upon the work done by Nielsen, A. B., Nitz, A. H., Capano, C. D. & Brown, D. A. (2018), ‘Investigatingthe noise residuals around the gravitational wave event GW150914’. <br>
The notebook has been downloaded twice. Each notebook has been changed to work for one other event from LIGOs first observational run, GW151012 and GW151226. With the purpose to investigate the correlations between the two LIGO detectors. 

The notebooks are done as part of a bachelor project done by **Felicia A. Fredriksson, Uppsala University**. The thesis will be published shortly onto Diva with the title: **_Investigating residuals from gravitational wave events, GW151012 and GW151226_.**. <br>



## Purpose of thesis ##
To further study correlations between the detectors this thesis performe the same analysis done for GW150914 but for GW151012 and GW151226. <br>
The effects from changing the bandpass filter and using different windows of data in the Pearson's correlation coefficents calculations are investigated as well. 
In addition to that these parameters were changed in the purpose to modifie the calulation better for each seperate event. What was used to change the upper bandpass limit and the window of data was the ratios of the total masses of each seperate investigated event compaired to the first detetcted signal, GW150914.

For analysis and conclusion read further in the paper: _Investigating residuals from gravitational wave events, GW151012 and GW151226_

The following text is the original README.md from the original work for GW150914, for their work: https://github.com/gwastro/gw150914_investigation.
*** 

# Investigating the noise residuals around the gravitational wave event GW150914

**Alex B. Nielsen<sup>1,2</sup>, Alexander H. Nitz<sup>1,2</sup>, Collin Capano<sup>1,2</sup>, and Duncan A. Brown<sup>3</sup>**

 <sub>1. [Albert-Einstein-Institut, Max-Planck-Institut for Gravitationsphysik, D-30167 Hannover, Germany](http://www.aei.mpg.de/obs-rel-cos)</sub>  
 <sub>2. Leibniz Universitat Hannover, D-30167 Hannover, Germany</sub>  
 <sub>3. Department of Physics, Syracuse University, Syracuse, NY 13244, USA</sub>  

## Introduction ##

We use the Pearson cross-correlation statistic proposed by [Liu and Jackson](http://iopscience.iop.org/article/10.1088/1475-7516/2016/10/014/meta),
and employed by [Creswell et al.](http://iopscience.iop.org/article/10.1088/1475-7516/2017/08/013/meta), to look for statistically significant correlations between
the LIGO Hanford and Livingston detectors at the time of the binary black hole merger
GW150914. We compute this statistic for the calibrated strain data released by LIGO, using
both the residuals provided by LIGO and using our own subtraction of a maximum-likelihood
waveform that is constructed to model binary black hole mergers in general relativity. To
assign a significance to the values obtained, we calculate the cross-correlation of both simulated
Gaussian noise and data from the LIGO detectors at times during which no detection of
gravitational waves has been claimed. We find that after subtracting the maximum likelihood
waveform there are no statistically significant correlations between the residuals of the two
detectors at the time of GW150914.

## Analysis Details ##

Details of the analaysis can be found in our [preprint paper](https://arxiv.org/abs/1811.04071).

## Description of Supplemental Material ##

This repository contains [Jupyter notebooks](http://jupyter.org/) that reproduce the results in our paper. Running the notebooks requires installation of [PyCBC](https://pycbc.org/) v1.12.4 and [LALSuite](https://git.ligo.org/lscsoft/lalsuite) 6.49, which contains version 1.8.0 of the LALSimulation library used to generate the maximum likelihood waveform. Both of these libraries can be installed using [pip](https://pip.pypa.io/en/stable/) with the command:
```sh
pip install 'pycbc==1.12.4' 'lalsuite==6.49'
```

The notebooks available in this repository are:

 1. [CreateResiduals.ipynb](https://github.com/gwastro/gw150914_investigation/blob/master/CreateResiduals.ipynb) creates the data used in the paper starting from data publically available from [GWOSC](https://gw-openscience.org) and the [supplemental materials](https://github.com/gwastro/pycbc-inference-paper/) from [Biwer et al](https://arxiv.org/abs/1807.10312) for the maximum likelihood waveform parameters.
 2. [Fig1_Fig2_Correlation.ipynb](https://github.com/gwastro/gw150914_investigation/blob/master/Fig1_Fig2_Correlation.ipynb) generates Figures 1 and 2 that show the correlations between timeseries data of the Hanford and Livingston detectors and the various residuals.
 3. [Fig3_Background.ipynb](https://github.com/gwastro/gw150914_investigation/blob/master/Fig3_Background.ipynb) generates Figure 3 and the data used to measure the statistical significance of the correlation statistic in simulated Gaussian noise and LIGO detector data.
 4. [Fig4_Fig5_Robustness.ipynb](https://github.com/gwastro/gw150914_investigation/blob/master/Fig4_Fig5_Robustness.ipynb) generates Figures 4 and 5 that explore the robustness of the correlation statistic to various choices of parameters.
 5. [Fig6_Fig7_WhitenedData.ipynb](https://github.com/gwastro/gw150914_investigation/blob/master/Fig6_Fig7_WhitenedData.ipynb) generates Figures 6 and 7 that explore the effect of whitening on the correllation statistic.

The residual file is also included in the repository. This is stored with `git-lfs` so a checkout of this repository is required to directly download the file. [Instructions for installing git-lfs](https://help.github.com/articles/installing-git-large-file-storage/). 

The residual file `residuals.hdf` contains the maximum-likelihood subtracted residuals for each detector (in `{detector}/residual`, where `{detector}` is `H1` and `L1`), as well as the maximum-likelihood waveform projected into each detector (in `{detector}/maxl_waveform`). Both of these datasets are 4096 seconds long, spanning the same time range as the GW150914 datasets that are available from GWOSC. The start time and time step of the datasets are stored in their respective `attrs`.

The parameters of the maximum-likelihood waveform are also stored in `residuals.hdf`, in the top-level `.attrs`. You can obtain them from within python by doing:

```
import h5py
with h5py.File('residuals.hdf', 'r') as fp:
    maxl_params = dict(fp.attrs.items())
```

## License and Citation ##

![Creative Commons License](https://i.creativecommons.org/l/by-sa/3.0/us/88x31.png "Creative Commons License")

This work is licensed under a [Creative Commons Attribution-ShareAlike 3.0 United States License](http://creativecommons.org/licenses/by-sa/3.0/us/).

We encourage use of these data in derivative works. If you use the material provided here, please cite the paper using the reference:

```
@article{Nielsen:2018XXX,
      author         = "Alex B. Nielsen, Alexander H. Nitz, Collin Capano, 
                        and Duncan A. Brown 
      title          = "{Investigating the noise residuals around the gravitational wave event GW150914}",
      year           = "2018",
      eprint         = "1811.04071",
      archivePrefix  = "arXiv",
      primaryClass   = "gr-qc",
      SLACcitation   = "%%CITATION = ARXIV:1811.04071;%%"
}

```


## Acknowledgements ##

We thank Sylvia Zhu and Sebastian Khan for carefully reading an earlier version of this work. ABN and DAB thank Andrew Jackson, Hao Liu and Pavel Naselsky for helpful discussions and the 2017 Kavli Summer Program in Astrophysics at the Niels Bohr Institute in Copenhagen and DARK University of Copenhagen for support during this work. The 2017 Kavli Summer Program program was supported by the the Kavli Foundation, Danish National Research Foundation (DNRF), the Niels Bohr International Academy and DARK. DAB thanks Will Farr for helpful discussions and NSF award PHY-1707954 for support.
