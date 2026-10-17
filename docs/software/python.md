# Python

INDACO has several Python versions installed. These commands load the latest one, Python 3.10.10 (as of June 2024):

```bash
source /exa/software/Spack-2023/spack/share/spack/setup-env.sh
spack load python@3.10.10%gcc@=8.5.0 arch=linux-rocky8-x86_64
```

This gives you the interpreter, but not libraries such as numpy, scipy or pandas. The recommended way to get them is a virtual environment, which pins package versions per project and avoids conflicts.

## Virtual environments

### Create one

Load Python first, then:

```bash
python -m venv ENVNAME
```

This creates a folder `ENVNAME` holding the environment. Environments can get large, so create them inside `DiscEvol_storage`, not your home.

### Activate it

```bash
source ENVNAME/bin/activate
```

### Install packages

```bash
pip install package_name
pip install package_name==version     # a specific version
pip install -r requirements.txt       # everything a project lists
```

### Ready-made environments

Shared environments for common setups will live in `DiscEvol_storage/python_envs`. Activate one with:

```bash
source ~/DiscEvol_storage/python_envs/env_name/bin/activate
```

!!! note "Shared means read-only"
    Don't install extra packages into a shared environment. Copy it somewhere of your own and change the copy.

*List of available environments: coming soon.*

## Worked example

Goal: run `script.py`, which needs specific versions of numpy, scipy and pandas. The version numbers below are placeholders.

Load Python:

```console
[user@astro01 ~]$ source /exa/software/Spack-2023/spack/share/spack/setup-env.sh
[user@astro01 ~]$ spack load python@3.10.10%gcc@=8.5.0 arch=linux-rocky8-x86_64
```

Create and activate an environment in storage:

```console
[user@astro01 ~]$ python -m venv ~/DiscEvol_storage/user/script_env
[user@astro01 ~]$ source ~/DiscEvol_storage/user/script_env/bin/activate
```

Install requirements (first time only):

```console
[user@astro01 ~]$ pip install numpy==2.12.3 scipy==2.3.4 pandas==4.4.1
```

Run:

```console
[user@astro01 ~]$ python script.py
```
