# METCS777 Term Paper: Spark Parameter Tuning

This is a document describing our term paper sample code and final results. We decided to do our paper on parameter tuning with PySpark.

## Environment Setup
This section will describe how to set up the local environment using a python virtual env.

## Using Conda & Jupyter Notebook
1. Download [Anaconda](https://www.anaconda.com/download) from the official website.
1. Run `conda install -y jupyter`
1. Change directories into `code`
1. Run `conda env create -f termpaper-conda.yml`
1. Activate the env: `conda activate cs777-termpaper`
1. If you don't have this library: `pip install ipykernel`
1. Run: `python -m ipykernel install --user --name pytorch --display-name "Python (METCS777 Term Paper)"`

### Running the Code Locally
To run the code locally on your machine, you can choose to follow the Jupyter Notebook section or the VS Code section.

#### 1. Running on Jupyter Notebook
Follow the instructions from the [Jupyter official docs](https://docs.jupyter.org/en/latest/running.html)  to install the required CLI command and any additional packages you may need for your machine.

1. Run `jupyter notebook`
1. Select the kernel you just named "Python (Term Paper)"
1. Use the Jupyter UI to run the code

#### 2. Running on VS Code
You can choose to run directly in VS Code by following simply opening the file and clicking the play button on the side of the cell you would like to run.

1. Open up VS Code
1. Select the kernel you just named "Python (Term Paper)"
1. Click the play button on the side of the cell to run the code

## Code Structure
The code structure for the demo is fairly simple with a preprocessing script to clean and output the clean data and a jupyter notebook to run examples of the parameter tuning results.

### Preprocessing and cleaning the data
Run this `cd code && python3 preprocess_and_clean_data.py` to generate clean data into ./clean_data which will handle filtering out outliers and invalid values from the dataset.

## Our Results
