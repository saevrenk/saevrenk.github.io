## Computational Chemistry in the Cloud

Computational chemistry has many different tools for different goals. However, one common feature of all the comp chem software is the complexity. This is because the end product results from many years of work by many researchers. Luckily, you do not have to write your own from scratch, there are plenty of [open-source codes](https://opensourcemolecularmodeling.github.io) available now. Combine that with free compute resources such as google colab, you can run your own comp chem exercise in the cloud for free, in no time at all.

Standard quantum chemistry calculations usually take too long. Also, due to the usage limits for free jobs in Colab (12 hours runtime and 16GB memory), a high accuracy calculation might be off limits. Semiempirical methods provide a trade-off between the accuracy and computational expense.  Recently, I posted a [Jupyter notebook](https://github.com/saevrenk/qc/blob/main/xtb.ipynb) to show how to use the [xTB semiempirical code](https://xtb-docs.readthedocs.io/en/latest/contents.html) from the Grimme group in the cloud for free. This notebook was inspired by Prof. Jensen's presentation at [here](https://youtu.be/KEIpJ50Jc0w). 

You can use condacolab to setup rdkit and xtb (it takes a few minutes to install the packages). 

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #333333">%%</span>capture
<span style="color: #FF0000; background-color: #FFAAAA">!</span>pip install <span style="color: #333333">-</span>q condacolab
<span style="color: #008800; font-weight: bold">import</span> <span style="color: #0e84b5; font-weight: bold">condacolab</span>
condacolab<span style="color: #333333">.</span>install()

<span style="color: #FF0000; background-color: #FFAAAA">!</span>mamba install <span style="color: #333333">-</span>c conda<span style="color: #333333">-</span>forge rdkit
<span style="color: #FF0000; background-color: #FFAAAA">!</span>mamba install <span style="color: #333333">-</span>c conda<span style="color: #333333">-</span>forge xtb
<span style="color: #FF0000; background-color: #FFAAAA">!</span>pip install py3Dmol
<span style="color: #FF0000; background-color: #FFAAAA">!</span>pip install rdkit<span style="color: #333333">-</span>pypi
</pre></div>

An example geometry optimization for the following PROTAC is shown in the notebook:

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%">protac_smi <span style="color: #333333">=</span> <span style="background-color: #fff0f0">&#39;C[C@@H]1CC2=C(NC3=CC=CC=C23)[C@H](N1CC(C)(C)F)C1=C(F)C=C(OCCOCCOCCOCC(=O)N[C@H](C(=O)N2C[C@H(O)C[C@H]2C(=O)NCC2=CC=C(C=C2)C2=C(C)N=CS2)C(C)(C)C)C=C1F&#39;</span>
protac <span style="color: #333333">=</span> Chem<span style="color: #333333">.</span>MolFromSmiles(protac_smi)
protac
</pre></div>

![protac 2d](/assets/protac_2d.png)

We need an initial 3D geometry for the geometry optimization with xTB. Below, the initial geometry from rdkit is shown on the left; the optimized geometry with xTB is shown on the right. 

![protac 3d](/assets/protac_3d.png)

Note: Unfortunately 3D geometries do not display properly in the jupyter notebook. The geometries can be seen in the original colab notebook by clicking the "Open in Colab" link.
