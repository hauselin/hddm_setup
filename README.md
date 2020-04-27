# Python HDDM module set up

Python [HDDM package](http://ski.clps.brown.edu/hddm_docs/) for fitting hierarchical drift diffusion models (HDDM)

For help and resources, visit their [mailing list](https://groups.google.com/group/hddm-users/).

All example datasets can be found [here](https://github.com/hddm-devs/hddm/tree/master/hddm/examples). Two (csv files) are provided in this repository.

## Set up conda environment

Install [Anaconda](https://www.anaconda.com/) so you can manage Python environments with conda.

In terminal, run the following code to create a new environment called `py36hddm` which uses Python 3.6:

```bash
conda create -n py36hddm python=3.6 anaconda # might not work with 3.7 or above!
conda activate py36hddm # activate environment
pip install pymc
pip install kabuki
pip install hddm
```

As of 2020-04-26, I've only managed to get the latest version of HDDM (0.7.6) to work in Python 3.6 (but not Python >= 3.7).

## Test HDDM model fitting, saving, reloading

In terminal, activate environment and run Python.

```bash
conda activate py36hddm
python
```

In Python, run the following code (after downloading `simple_difficulty.csv` to your working directory):

```python
import hddm
hddm.__version__  # check version

data = hddm.load_csv('simple_difficulty.csv')  # load data
model = hddm.HDDM(data, depends_on={'v':'difficulty'})  # define model
model.sample(50, burn=20, dbname='traces1', db='pickle')  # sample and save traces
model.print_stats() 

model.save('m1') # save model and traces

m1 = hddm.load('m1') # reload saved model
m1.print_stats()
```

If your installation works well, you shouldn't see any errors when running the code above. 