# Application Research Notes

The entire content of the Application research is built with Jupyter book and other python based documentation, rederers and visualisers.

## Setup Environment

To replicate the development environment or the editing environment can be set up using the Anaconda/Miniconda package manager does'nt matter which one is used as long as you have environment.yml file

**As of 16-May-2023**
For this setup we gone with python 3.8.16 since it's the last python version that's reached Security fix maintenance status in python project 3.10 and 3.11 are in bugfix maintenance status.

### Note

--> ***The entire base will be shortly migrated to python 3.9.16 once offline code templates are tested.***

Pip version is always chosen to be updated to latest available (23.1.2)

```bash
conda env create -f environment.yml
activate application_research_notes

```

## Contribute

Do you wnat to contribute?

The best way is to raise a Github Issue 🙂

### Editing and adding content

The content is only added to the markdown files in the chapters folder and raise a PR.
The content will then be built to Jupyter book by owners and merged to **main branch** from **proof-read** branch.

