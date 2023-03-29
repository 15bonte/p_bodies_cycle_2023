# Methods, plots and numerical results for Safieddine et al. (2023)

[![License](https://img.shields.io/badge/license-BSD%203--Clause-green)](https://github.com/15bonte/p_bodies_cycle_2023/blob/main/LICENSE)
[![Python 3.6](https://img.shields.io/badge/python-3.9.13-blue.svg)](https://www.python.org/downloads/release/python-3913/)
<!-- [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.4322750.svg)](https://doi.org/10.5281/zenodo.4322750) -->

This repository gathers the code used for the following paper:

__Title:__ Purifying p-bodies across the cell cycle reveals a widespread cyclic RNA storage function and an RNA localization mechanism dependent on the CDS length

__Authors:__ [Adham Safieddine](mailto:safieddine.adham@gmail.com)<sup>\*</sup>, Marie-Noëlle Benassy, Thomas Bonte, Michel Kress, Michèle Ernoult-Lange, Maïté Courel, Emeline Coleno, Antoine Laine, Annie Munier Godebert, Angelique Vinit, Corinne Blugeon, Guillaume Chevreux, Oriane Pourcelot ?, Edouard Bertrand, Daniel Gautheret, Thomas Walter, Marianne Bénard, Dominique Weil<sup>\*</sup>

<!-- [Adham Safieddine](mailto:safieddine.adham@gmail.com)<sup>1,2,\*</sup>, Emeline Coleno<sup>1,2</sup>, Soha Salloum<sup>1,2,3,+</sup>, Arthur Imbert<sup>4,5,6,+</sup>, Abdel-Meneem Traboulsi<sup>1,2</sup>, Oh Sung Kwon<sup>7</sup>, Frederic Lionneton<sup>8</sup>, Virginie Georget<sup>8</sup>, Marie-Cécile Robert<sup>1,2</sup>, Thierry Gostan<sup>1</sup>, Charles Lecellier<sup>1,2</sup>, Racha Chouaib<sup>1,2,5</sup>, Xavier Pichon<sup>1,2</sup>, Hervé Le Hir<sup>3</sup> , Kazem Zibara<sup>5</sup>, Florian Müller<sup>9,10</sup>, Thomas Walter<sup>4,5,6</sup>, Marion Peter<sup>1,2</sup>, [Edouard Bertrand](mailto:edouard.bertrand@igmm.cnrs.fr)<sup>1,2,11,\*</sup>

><sup>1</sup>Institut de Génétique Moléculaire de Montpellier, University of Montpellier, CNRS, Montpellier, France
<sup>2</sup>Equipe labélisée Ligue Nationale Contre le Cancer, University of Montpellier, CNRS, Montpellier, France
<sup>3</sup>ER045, PRASE, DSST, Faculty of Sciences-I, Lebanese University, Beirut, Lebanon
<sup>4</sup>MINES ParisTech, PSL-Research University, CBIO-Centre for Computational Biology, 77300 Fontainebleau, France
<sup>5</sup>Institut Curie, 75248 Paris Cedex, France
<sup>6</sup>INSERM, U900, 75248 Paris Cedex, France
<sup>7</sup>Institut de biologie de l'Ecole normale supérieure (IBENS), Ecole normale supérieure, CNRS, INSERM, PSL Research University, 46 rue d'Ulm, 75005, Paris, France
<sup>8</sup>BioCampus Montpellier, CNRS UMS3426, 141, rue de la Cardonille, 34094 Montpellier Cedex 5, France
<sup>9</sup>Unité Imagerie et Modélisation, Institut Pasteur and CNRS UMR 3691, 28 rue du Docteur Roux, 75015 Paris; France
<sup>10</sup>C3BI, USR 3756 IP CNRS – Paris, France
<sup>11</sup>Institut de Génétique Humaine, University of Montpellier, CNRS, Montpellier, France
>
><sup>+</sup>Equal contributions-->

<sup>\*</sup>To whom correspondence should be addressed.

## Prerequisites

The analysis pipeline consists of three different resources that are best run
in dedicated virtual environments:

- [**BigFISH**](https://github.com/fish-quant/big-fish), a python library to process smFISH images. It allows to detect mRNAs and centrosomes in 2D, format segmentation masks and compute spatial features at the cell-level.
    - Run the command `pip install big-fish==0.6.2` in an empty virtual environment to reproduce our python environment and run BigFISH methods.
- [**Cellpose**](http://www.cellpose.org/), a Deep Learning based approach for nuclei and cells segmentation.
    - Run the command `pip install -r requirements_cellpose.txt` in an empty virtual environment to reproduce our python environment and run Cellpose model.
- A more general environment with classic scientific libraries to perform statistical tests and plot results. We use it as a kernel for the final Ipython notebook _notebook_script.ipynb_.
    - Run the command `pip install -r requirements_notebook.txt` in an empty virtual environment to reproduce our python environment and run the _notebook_script.ipynb_ notebook.

## Pipeline

Below, we provide a quick overview of the different steps in the analysis.

1. **Nucleus and cell segmentation using Cellpose & Bigfish** 
2. **RNA molecules counting**
3. **Recruited RNAs counting**
4. **Results summary**

If you have any question relative to the image analysis, please contact [Thomas Bonte](mailto:thomas.bonte@mines-paristech.fr) or [Adham Safieddine](mailto:safieddine.adham@gmail.com) (or open an issue).

### Data

Current notebook is taking a .TIF image into input. Such image should contain (at least) 3 channels: DAPI, smFISH and GFP.

| DAPI | FISH | GFP |
| ------------- | ------------- | ------------- |
| ![](images/DAPI_example.png) | ![](images/smFISH_example.png) |  ![](images/GFP_example.png) |

### 1 - Nucleus and cell segmentation using Cellpose & Bigfish

Using Cellpose for nucleus segmentation and Bigfish for cell segmentation, one can obtain such result.

![](images/segmentation_example.png)

### 2 - RNA molecules counting

For each cell, RNA spots are then detected using Bigfish.

![](images/rna_counting_cell16.png)


### 3 - Recruited RNAs counting

For each cell, P-bodies are segmented with Bigfish to count the number of RNA molecules recruited.

![](images/rna_recruited_cell16.png)

### 4 - Results summary

Finally, all results can be saved in a csv file.

| cell_id|cell_area|nuc_area|nb_rna1|nb_rna1_in_nuc|nb_rna1_out_nuc|nb_rna1_recruited | 
|---|---|---|---|---|---|--- | 
| 1|47542|20564|114|28|86|0 | 
| 2|71320|33040|142|44|98|5 | 
| 3|19278|6481|61|6|55|1 | 
| 4|59265|27553|126|21|105|60 | 
| 5|34352|17316|73|12|61|4 | 
| 6|48689|12119|88|1|87|17 | 
| 7|54479|27799|37|13|24|9 | 
| 8|68061|26909|44|19|25|5 | 
| 9|33651|16329|125|78|47|0 | 
| 10|22641|9764|90|31|59|14 | 
| 11|50673|26573|39|13|26|1 | 
| 12|52307|27189|61|26|35|4 | 
| 13|63447|21221|113|14|99|60 | 
| 14|43046|24145|27|17|10|2 | 
| 15|56381|25698|155|15|140|100 | 
| 16|20682|10938|13|4|9|0 | 
| 17|96309|32900|412|84|328|39 | 
| 18|22838|12080|16|5|11|5 | 

## Licensing (TO BE MODIFIED ?)

- **BigFISH** and the rest of the code provided in this repository (notebook) are BSD-licenced (3 clause):
>Copyright © 2020, Arthur Imbert  
>All rights reserved.
>
>Redistribution and use in source and binary forms, with or without
>modification, are permitted provided that the following conditions are met:
>    * Redistributions of source code must retain the above copyright
      notice, this list of conditions and the following disclaimer.
>    * Redistributions in binary form must reproduce the above copyright
      notice, this list of conditions and the following disclaimer in the
      documentation and/or other materials provided with the distribution.
>    * Neither the name of the copyright holder nor the names of its
      contributors may be used to endorse or promote products derived from
      this software without specific prior written permission.
>
>THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY
DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.