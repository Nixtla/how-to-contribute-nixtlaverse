# How to contribute to the Nixtlaverse

> This repository contains instructions for collaborating on the different libraries of Nixtla. The instructions are specific to [mlforecast](https://github.com/Nixtla/mlforecast) but can be applied to [statsforecast](https://github.com/Nixtla/statsforecast) and [neuralforecast](https://github.com/Nixtla/neuralforecast) as well.

# Table of Contents

1. [Create a fork of the mlforecast repo.](https://github.com/Nixtla/how-to-contribute-nixtlaverse/tree/main#1-create-a-fork-of-the-mlforecast-repo)
2. [Clone the repository](https://github.com/Nixtla/how-to-contribute-nixtlaverse#2-clone-the-repository)
3. [Create the conda environment](https://github.com/Nixtla/how-to-contribute-nixtlaverse#3-create-the-conda-environment)
4. [Make the changes you want](https://github.com/Nixtla/how-to-contribute-nixtlaverse#4-make-the-changes-you-want)
5. [Create a pull request](https://github.com/Nixtla/how-to-contribute-nixtlaverse#5-create-a-pull-request)

## 1. Create a fork of the mlforecast repo.
The first thing you need to do is create a fork of the GitHub repository to your own account:
![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/af767f5b-66f1-4068-9dd2-917096285ae9)

Your fork on your account will look like this:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/912b848d-d3d1-4f79-9d5b-10dd66e1bd35)

In that repository, you can make your changes and then request to have them added to the main repo.

## 2. Clone the repository.

In this tutorial, we are using Mac (also compatible with other Linux distributions). If you are a collaborator of Nixtla, you can request an AWS instance to collaborate from there. If this is the case, please reach out to Max or Fede on Slack to receive the appropriate access. We also use Visual Studio Code, which you can download from [here](https://code.visualstudio.com/download).

Once the repository is created, you need to clone it to your own computer. Simply copy the repository URL from GitHub as shown below:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/1331354e-ac24-4222-82f1-71df7077f2e0)

Then open Visual Studio Code, click on "Clone Git Repository," and paste the line you just copied into the top part of the window, as shown below:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/982827d5-89a6-43d4-8bb8-85bd1758bc10)

Select the folder where you want to copy the repository:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/c1a169e6-df27-41fb-84ee-a441a149e3d6)

And choose to open the cloned repository:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/00140c15-237e-4afa-a47d-078a1afbbac0)

You will end up with something like this:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/ea4aed6f-2000-4ec8-a242-36b9dfd68d26)


## 3. Create the Conda environment.

Open a terminal within Visual Studio Code, as shown in the image:

<img width="1423" alt="image" src="https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/9b3ed42f-1a68-450c-bffd-a7cee40bb781">

We highly recommend using Mamba to speed up the creation of the Conda environment. To install it, simply use `conda install mamba -c conda-forge` in the terminal you just opened:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/08482b00-9434-46f0-9452-c3f4920eca6d)

Create an empty environment named `mlforecast` with the following command: `mamba create -n mlforecast python=3.10`:
![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/5e9032e8-3f5b-4a1c-93e7-3d390d5f73f1)

Activate the newly created environment using `conda activate mlforecast`:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/803ae2b7-8369-4a24-9b7c-9326d52c13ef)

Install the libraries within the environment file `environment.yml` using `mamba env update -f environment.yml`:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/e9672d58-b477-4963-9751-277c944a4d8a)

Now install the library to make interactive changes and other additional dependencies using `pip install -e ".[dev]"`:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/501c8223-862d-40a9-8f2d-ecdaceaeaedb)

## 4. Make the changes you want.

In this section, we assume that we want to increase the default number of windows used to create prediction intervals from 2 to 3. The first thing we need to do is create a specific branch for that change using `git checkout -b [new_branch]` like this:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/7884f89a-ecc6-4200-8176-6a9b9f7c0aa2)

Once created, open the notebook you want to modify. In this case, it's `nbs/utils.ipynb`, which contains the metadata for the prediction intervals. After opening it, click on the environment you want to use (top right) and select the `mlforecast` environment:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/0a0a8285-9344-471e-b699-8bc13159e3a8)

Next, execute the notebook and make the necessary changes. In this case, we want to modify the `PredictionIntervals` class:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/0a614d14-52c9-4ba1-88e5-02e19661cae7)

We will change the default value of `n_window` from 2 to 3:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/af31a79d-0165-4c79-94bc-f411ec67b3ea)

Once you have made the change and performed any necessary validations, it's time to convert the notebook to Python modules. To do this, simply use `nbdev_export` in the terminal.


You will see that the `mlforecast/utils.py` file has been modified (the changes from `nbs/utils.ipynb` are reflected in that module). Before committing the changes, we need to clean the notebooks using the command `./action_files/clean_nbs` and verify that the linters pass using `./action_files/lint`:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/cecf76a1-c025-4b6f-97c0-584394a3f56a)

Once you have done the above, simply add the changes using `git add nbs/utils.ipynb mlforecast/utils.py`:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/107689d8-a270-4621-ac5d-9d077d9203c3)

Create a descriptive commit message for the changes using `git commit -m "[description of changes]"`:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/034578e2-d63c-4d74-a96f-99f405288326)

Finally, push your changes using `git push`:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/49c6851c-949b-4ca7-ac38-6b17ec103437)


## 5. Create a pull request.

In GitHub, open your repository that contains your fork of the original repo. Once inside, you will see the changes you just pushed. Click on "Compare and pull request":

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/c3d2ce0d-5fc9-4356-87d3-51b32e72524a)

Include an appropriate title for your pull request and fill in the necessary information. Once you're done, click on "Create pull request".

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/7de9c461-ad49-4fc2-b648-507662466851)

Finally, you will see something like this:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/846c0b97-46d2-492b-a58e-3e9f669c1632)






