DVC can be used for following purposes -

1. Mainting the different version of the data on which model is trained.
2. Storing the data at diffrent place from code.
3. use `.github/workflows/cml.yaml` file to check basic things before pushing code to github repository i.e how this code performs and display the metrices and basic cml report, so that we kow whether to merge this code to main branch or not. [link](https://github.com/elleobrien/wine/tree/experiment-1)
4. use `dvc.yaml` to create dvc pipelines and to compare metrices across diffrent branches i.e main vs current branch. [link](https://github.com/elleobrien/farmer/blob/master/dvc.yaml)
5. It can be used for experiment tracking and hyperparameter tuning as shown below: [link](https://github.com/iterative/pretrained-model-demo)

# Data version control using DVC and metrices logging using using dcvlive.

This code can be used for experiment tracking as well. 

If you open `pretrained_model_tuner`, you'll see a line where we dump the accuracy and loss for the training epochs into the results.json file.We're also saving the model on the epoch run and recording metrics for each epoch using dvclive logging. In this file we also define the parametrs to be used as defined in `params.yaml` file

1. First clone the repo into your local machine.
2. Cd into the cloned repositioy Then download the dataset from [here](https://download.pytorch.org/tutorial/hymenoptera_data.zip) and put it in location data/hymenoptera_data.
3. `pip install -r requiremtnts.txt`
4. `dvc init`
5. Now type `dvc exp run` into the terminal to run the experiment i.e dvc pipeline as defined in `dvc.yml` file.
6.  Type `dvc exp show` to display the results of the experiment. Or `dvc exp show --no-timestamp --include-params lr,momentum,model_name`
7.  Now let's update the hyperparameters and run another experiment. There are several ways to do this with DVC:
       - Change the hyperparameter values directly in `params.yaml`. 
       - Update the values using the --set-param or the shorthand -S option on dvc exp run. Eg: `dvc exp run --reset -S model_name=alexnet -S num_epochs=2`
       - Queue multiple experiments with different values using the --queue option on dvc exp run. Eg: `dvc exp run --queue -S lr=0.0001 -S momentum=0.9 -S num_epochs=2` and `dvc exp run --queue -S lr=0.001 -S momentum=0.09 -S num_epochs=2` back to back.Running this sets up an experiment for future execution so we'll go ahead a run this command one more time with different values. Then you can execute all of the queues with this command `dvc exp run --run-all`
