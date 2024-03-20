# METCS777 Term Paper: Spark Parameter Tuning

This is a document describing our term paper sample code and final results. We decided to do our paper on parameter tuning with PySpark. Our term paper is based on a conference paper that can be found here: [Spark Parameter Tuning via Trial-and-Error](./supporting_docs/spark_param_tuning_conference_paper.pdf).

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
This section will discuss the final results and finding of our term paaper.

### Default SparkConfig Changes: Spark 1.5.2 -> Spark 3.5.1
This section lists the default config for each optimal configuration from the [conference paper](./supporting_docs/spark_param_tuning_conference_paper.pdf)

The version of Spark at the time of the original experiments was 1.5.2 and a lot has changed since then.

- `spark.reducer.maxSizeInFlight` = 48m

- `spark.shuffle.compress` = True

- `spark.shuffle.file.buffer` = 32k

- `spark.io.compression.codec` = org.apache.spark.io.LZ4CompressionCodec

- `spark.shuffle.io.preferDirectBufs` = True

- `spark.rdd.compress` = False

- `spark.serializer` = org.apache.spark.serializer.JavaSerializer

- `spark.shuffle.file.buffer` = 32k

### Deprecations:
This section will highlight the deprecations since the conference paper was written, and the reasons for each deprecation of an optimial config.

For the following deprecated configurations, you can refer to the [Unified Memory Management Spark Paper](./supporting_docs/unified-memory-management-spark-10000.pdf). In short, there is no longer dedicated cache/shuffle memory. All memory can be used for either operation.

- `spark.shuffle.consolidateFiles = False (default)`
    - This configuration seems to be deprecated in version 1.6.0, however there is not any official documentation in the changelog and it's a little unclear.
    - This PR gives a little bit of background into why the configuraton doesn't exist: https://github.com/apache/spark/pull/8089. In short, it seems that the deprecation of HashShuffleManager by default has made this configuration obsolete.

- `spark.shuffle.manager` = sort
    - Deprecated in 2.x
    - `HashShuffleManager` was removed entirely in version 2.x (https://issues.apache.org/jira/browse/SPARK-14667)
    - For more details on this decision refer to this paper: https://www.waitingforcode.com/apache-spark/shuffling-in-spark/read#sort_shuffle_manager

- `spark.shuffle.memoryFraction` = 0.2
    - Deprecated in spark 1.6.0+
    - This is read only if spark.memory.useLegacyMode is enabled. It was the fraction of Java heap to use for aggregation and cogroups during shuffles

- `spark.storage.memoryFraction` = 0.6
    - Deprecated in spark 1.6.0+
    - This is read only if spark.memory.useLegacyMode is enabled. It was the fraction of Java heap to use for Spark's memory cache

