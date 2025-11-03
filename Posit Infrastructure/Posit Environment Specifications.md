# Posit Environment Specifications

## Operating System and Application Specifications

- **Operating System**
  - Ubuntu 22.04.5 LTS Jammy Jellyfish
- **Applications and Versions**:
  - **Posit Workbench**: 2025.09.1+401.pro2, “Cucumberleaf Sunflower” (59cf440a).
  - **Posit Package Manager**: v2025.09.0-7
  - **Posit Connect**: _Coming soon..._
- **R and Python Versions**:
  - **R**: Default version is v4.5.1, with additional support for v4.4.2 
  - **Python**: Default version is 3.13.8, with additional support for versions 3.12.11 and 3.10.12
- **Supported IDEs**:
  - RStudio Pro 2025.09.1 Build 401.pro2 with support for Quarto 1.8.25
  - Jupyter Notebook 7.2.3
  - JupyterLab 4.2.7
  - Visual Studio Code 1.102.0
  - Positron Pro 2025.08.1 build 11 (for evaluation purposes only)

## Infrastructure Specification

- The environment is hosted on [Microsoft Azure](https://azure.microsoft.com/en-gb).
- Posit Workbench sessions are launched on a [Kubernetes cluster](https://www.vmware.com/topics/kubernetes-cluster)
- There are two node pools in the Kubernetes cluster (nodepool and bigpool) which have different types of Virtual Machine (VM):
  - nodepool (default): Standard_E20as_v5 with 20 vCPUs and 160GiB RAM - scales up to 48 nodes
  - bigpool (BIG): Standard_E32as_v5 with 32 vCPUs and 256GiB RAM - scales up to 6 nodes
- You will only have access to the "bigpool" if you are a member of the `positwb_super_user` UNIX group.  You can request access to this group by emailing the [Data Science Team](phs.datascience@phs.scot).  You will also need Line Manager authorisation.
- The Kubernetes container image is based on **Ubuntu 22.04.5 LTS (Jammy Jellyfish)**, providing better support for Posit Workbench, R, Python, and associated packages.
- A reduced-size version of TeX has been installed in the container image to decrease its size and reduce session startup times.