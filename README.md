# cb-tutorial-code
Demo code from [SIGIR 2016 Tutorial on Counterfactual Evaluation and Learning](http://www.cs.cornell.edu/~adith/CfactSIGIR2016/).

To setup environment, run:
```
brew install vowpal-wabbit
conda create -n sigir2016-cb-tutorial python=3.5
conda install scikit-learn=0.17.1 numpy scipy joblib -y
```

## From tutorial site:
Code and Data for News Recommendation Demo
Download all required files for the demo here: Code_Data.zip

Dependencies

All evaluation and most learning approaches are written in Python3. The one exception -- learning using ERM and Inverse Propensity Scoring (or Doubly Robust estimators) -- uses Vowpal Wabbit.

Recommended installation process:

- Download and install Anaconda with Python3 (e.g. Python 3.5).
- Ensure the following python packages are installed : Numpy, Scipy, Scikit-learn, joblib. With Anaconda, just use:
`conda install [package]`
- Install Vowpal Wabbit. On Windows, use cygwin and follow these instructions.
- Unzip the Code_Data.zip downloaded from above, and navigate to Code_Data/Code/Synth_TestBed/.

To run the evaluation experiments, use
```
python EvalExperiment.py [-h]
```
Allowed values for the -e and -f options (the policy to evaluate, and the policy that serves as the scorer for Plackett-Luce randomization) are ridge,lasso,lstsq,tree

Allowed values for the -v option (the metric to measure/optimize) are Revenue,Constant

To plot the results of running evaluation experiments, use
```
python plot_sigir.py --mode [estimate/error] --path [../../Logs/ssynth...pkl]
```

To run the learning experiments, use
```
python OptExperiment.py [-h]
```
If you wish to also observe Vowpal Wabbit results for learning, supply the "-d" option to the OptExperiment script [WARNING: Dumps massive dataset files.] Additionally run,
```
vw -d vw_train.dat --cb_adf -f cb.model --passes 20 –cache_file cb.cache
vw -t -d vw_test.dat -i cb.model -p test.predict
python vw_helper.py –d vw_test2.dat –p test.predict
```

Note that Vowpal Wabbit has several tunable parameters and implements an efficient grid-search and cross-validation strategy. Have fun playing with multiple hyper-parameters!
