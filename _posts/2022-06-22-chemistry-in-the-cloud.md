## Computational Chemistry in the Cloud

Computational chemistry has many different tools for different goals. However, one common feature of all the comp chem software is the complexity. This is because the end product results from many years of work by many researchers. Luckily, there are plenty of [open-source codes](https://opensourcemolecularmodeling.github.io) available now. Combine that with free compute resources such as google colab, you can run your own comp chem exercise in the cloud for free, in no time.

Standard quantum chemistry calculations take usually too long. Due to the usage limits for free jobs in Colab (12 hours runtime and 16GB memory) high accuracy calculation might be off limits. Semiempirical methods provide a trade-off between the accuracy and computational expense.  Recently, I posted a [Jupyter notebook](https://github.com/saevrenk/qc/blob/main/xtb.ipynb) to show how to use the [xTB semiempirical code](https://xtb-docs.readthedocs.io/en/latest/contents.html) from the Grimme group in the cloud for free. This notebook was inspired by Prof. Jensen's presentation at [here](https://youtu.be/KEIpJ50Jc0w). 

You can use condacolab to setup rdkit and xtb (it takes sometime to install the packages). 
```python
%%capture
!pip install -q condacolab
import condacolab
condacolab.install()

!mamba install -c conda-forge rdkit
!mamba install -c conda-forge xtb
!pip install py3Dmol
```
An example geometry optimization for the following PROTAC is shown in the notebook:

```python
protac_smi = 'C[C@@H]1CC2=C(NC3=CC=CC=C23)[C@H](N1CC(C)(C)F)C1=C(F)C=C(OCCOCCOCCOCC(=O)N[C@H](C(=O)N2C[C@H](O)C[C@H]2C(=O)NCC2=CC=C(C=C2)C2=C(C)N=CS2)C(C)(C)C)C=C1F'
protac = Chem.MolFromSmiles(protac_smi)
protac
```
![protac 2d](/assets/protac_2d.png)

To do the optimization we need an initial 3D geometry. In the notebook, we obtained this from rdkit by MMFF force field optimization. The molecular mechanic geometry from rdkit is shown on the left. Using the rdkit geometry as the initial structure, we optimized the geometry (tight) with xTB; this is shown on the right.

![protac 3d](/assets/protac_3d.png)

Unfortunately 3D geometries do not display properly in the jupyter notebook, but the colab link is also provided which works fine.
