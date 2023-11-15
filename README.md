# GR@PPA-4.10
## Introduction
Please find more details on the [official GR@PPA website](https://atlas.kek.jp/old/physics/nlo-wg/grappa.html) and the [GR@PPA Event Generator paper](https://arxiv.org/abs/1012.5555).

## Dependencies
- **Login Node:** lxplus.cern.ch
- **Operating System:** CentOS Linux release 7.9.2009
- **No need to setupATLAS**
## To Download and Compile
```sh
git clone https://github.com/beatrice-pan/GR-PPA-4.10.git
cd GR-PPA-4.10
tar -zxvf GR@PPA-4.10.tgz
cp matrix_susy2_v1.00.tgz GR@PPA-4.10
cd GR@PPA-4.10
tar -zxvf matrix_susy2_v1.00.tgz
./Config.perl
make susy2
make kinem
make integ
make install
make example
```
## To Run this Monte-Carlo Generator
```sh
cd example/alone/
```
To change the random seed (generating different data based on the same input paramters), one should edit ```upinit.f``` by ```vim upinit.f```, and modify line 91: ```IRSEED = <random number>```)
```sh
make
./alsample
```

## SUSY Mass Configurations
The configurations of the mass of SUSY particles could be found in ```grcpar.F```. For setting the parameters, there are a few constarints. 

- The gluino mass calculation is determined by the following formula: $$m_\text{gluino}= ALPHAS\times(1.0-(\frac{AMW}{AMZ})^2)/ALPHA \times XM2$$
where ALPHAS, AMW, AMZ, ALPHA are given in ```grcpar.F```. To modify the gluino mass $m_\text{gluino}$, only the XM2 should be changed accordingly and the rest of parameters in the formula remain the same. 

- The SUSY particle suffixed with "2" should have a larger mass than that is suffixed with "1". E.g., AMSQ1 should be set smaller than SMSQ2; AMSBT1 should be smaller than AMSBT2. 

Kind reminder: every time the parameters change, one should ```make``` again before running the generator. 
