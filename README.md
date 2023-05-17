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

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/7a108df8-1d9b-4c0f-b32e-7cae923b0f6b)


Once created, open the notebook you want to modify. In this case, it's `nbs/utils.ipynb`, which contains the metadata for the prediction intervals. After opening it, click on the environment you want to use (top right) and select the `mlforecast` environment:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/c7fb0add-d6c1-42a5-9198-641179d15a5f)


Next, execute the notebook and make the necessary changes. In this case, we want to modify the `PredictionIntervals` class:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/aae5787f-1e00-4e0a-851b-f66c0c3e872e)


We will change the default value of `n_window` from 2 to 3:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/fa2730bf-a073-401e-a2c8-53e0b23954a8)


Once you have made the change and performed any necessary validations, it's time to convert the notebook to Python modules. To do this, simply use `nbdev_export` in the terminal.

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/c72e1259-2f37-4a2d-90b7-75e7e0b50db4)

You will see that the `mlforecast/utils.py` file has been modified (the changes from `nbs/utils.ipynb` are reflected in that module). Before committing the changes, we need to clean the notebooks using the command `./action_files/clean_nbs` and verify that the linters pass using `./action_files/lint`:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/38034ab7-47d0-4730-9f3a-709de549be32)

Once you have done the above, simply add the changes using `git add nbs/utils.ipynb mlforecast/utils.py`:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/5c86b9e5-b4bf-4048-8422-b8b72d59d98f)

Create a descriptive commit message for the changes using `git commit -m "[description of changes]"`:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/3b242e24-b633-463e-ac94-e580c6139005)

Finally, push your changes using `git push`:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/1d278ce1-82f2-4878-89de-eb56ac573a9f)


## 5. Create a pull request.

In GitHub, open your repository that contains your fork of the original repo. Once inside, you will see the changes you just pushed. Click on "Compare and pull request":

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/e709b41a-37b4-497d-8e06-4a22f9ba85c3)

Include an appropriate title for your pull request and fill in the necessary information. Once you're done, click on "Create pull request".

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/9eba8015-8ea8-48dd-b802-c506cf58d478)

Finally, you will see something like this:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/26607469-83f3-45bd-9c52-a731dddd4409)






