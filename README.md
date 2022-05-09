# SLURM profile for SnakeMake

SnakeMake is a pipeline manager for bioinformatic analyses. To make sure SnakeMake works with SLURM at Oregon Health and Science University, please follow the instructions: 

```bash
$ cd ~/.config/snakemake
$ git clone https://github.com/maxsonBraunLab/slurm.git
$ cd slurm # edit cluster.yaml and save the changes
```

When editing the `cluster.yaml` file, you can set default arguments to your snakemake submission command. See the following example:

```
$ cat ~/.config/snakemake/slurm/config.yaml

jobscript: "slurm-jobscript.sh"
cluster: "slurm-submit.py"
cluster-status: "slurm-status.py"
max-jobs-per-second: 20
max-status-checks-per-second: 10
local-cores: 1
latency-wait: 60

use-conda: True
printshellcmds: True
conda-prefix: "/directory/to/anaconda3/envs"

```

With these arguments, running the command `snakemake -j 8 --profile slurm` is the same as `snakemake -j 8 --use-conda -p --conda-prefix /directory/to/anaconda3/envs`. More command line arguments can be found in the [SnakeMake documentation](https://snakemake.readthedocs.io/en/stable/executing/cli.html).

Note that the `cluster.yaml` in this folder belongs in `~/.config/snakemake/slurm`, and is not the same as the `cluster.yaml` in a pipeline that allocates job resources per rule. This is a one-time setup and requires minor edits over time, but the same profile will work for every pipeline you run. To add a different HPC profile, copy the whole directory structure into `~/.config/snakemake/<profile>`. To read more about SnakeMake profiles, please read the [comprehensive documentation](https://snakemake.readthedocs.io/en/stable/executing/cli.html).