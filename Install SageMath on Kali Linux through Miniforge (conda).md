# 1. Install Miniforge

Download the Miniforge installer.

```bash
wget https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh
````

Run the installer.

```bash
bash Miniforge3-Linux-x86_64.sh
```

During installation:
- Accept the license.
- Allow the installer to initialize your shell.    

Reload the shell configuration.

```bash
source ~/.bashrc
```

Verify Conda installation.

```bash
conda --version
```

---
# 2. Update Conda

Update Conda to the latest version.

```bash
conda update -n base -c conda-forge conda
```

---
# 3. Create a SageMath Environment

Create a dedicated environment for SageMath.

```bash
conda create -n sage -c conda-forge sage
```

This installs SageMath and all required dependencies.

---
# 4. Activate the Environment

Activate the Sage environment.

```bash
conda activate sage
```

---
# 5. Run SageMath

Start Sage.

```bash
sage
```

Test the installation.

```python
factor(123456)
```

---
# 6. Install PyCryptodome

Some cryptography scripts require the `Crypto` module.  
Install **pycryptodome** inside the Sage environment.

Using Conda:

```bash
conda install -c conda-forge pycryptodome
```

Alternative using pip:

```bash
pip install pycryptodome
```

Verify installation.

```bash
python -c "from Crypto.Cipher import AES"
```

---
# 7. Optional: Jupyter Notebook Support

Install Jupyter.

```bash
conda install -c conda-forge notebook
```

Launch Sage inside Jupyter.

```bash
sage -n jupyter
```

---
# 8. Updating SageMath Later

Activate the environment.

```bash
conda activate sage
```

Update SageMath.

```bash
conda update sage
```

---
# 9. Deactivating the Environment

Exit the Sage environment when finished.

```bash
conda deactivate
```