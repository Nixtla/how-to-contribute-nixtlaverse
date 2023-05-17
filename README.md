# How to contribute to the Nixtlaverse


> This repository contains instructions for collaborating on the different libraries of Nixtla. The instructions are specific to [mlforecast](https://github.com/Nixtla/mlforecast) but can be applied to [statsforecast](https://github.com/Nixtla/statsforecast) and [neuralforecast](https://github.com/Nixtla/neuralforecast) as well.

## 1. Create a fork of the mlforecast repo.
The first thing you need to do is create a fork of the GitHub repository to your own account:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/e46d02e9-34c6-4efd-bea5-4087f6eae86e)

Your fork on your account will look like this:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/8571f460-681e-49e6-8b75-b70c4a1c2499)

In that repository, you can make your changes and then request to have them added to the main repo.

## 2. Clone the repository.

In this tutorial, we are using Mac (also compatible with other Linux distributions). If you are a collaborator of Nixtla, you can request an AWS instance to collaborate from there. If this is the case, please reach out to Max or Fede on Slack to receive the appropriate access. We also use Visual Studio Code, which you can download from [here](https://code.visualstudio.com/download).

Once the repository is created, you need to clone it to your own computer. Simply copy the repository URL from GitHub as shown below:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/c9bfd4de-9961-468d-bcfc-bf7c82756090)

Then open Visual Studio Code, click on "Clone Git Repository," and paste the line you just copied into the top part of the window, as shown below:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/58847265-b7c9-4140-979d-1d2b2fb45a4b)

Select the folder where you want to copy the repository:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/9776d80b-a031-4046-a8f5-0c5dc62a6ded)

And choose to open the cloned repository:


![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/8ec5fdaf-9820-4177-8d45-b35fcd91199e)


You will end up with something like this:


![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/8be49410-9bef-41bd-a86b-8db1c897f1be)

## 3. Create the Conda environment.

Open a terminal within Visual Studio Code, as shown in the image:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/63304c31-9030-494c-adb3-84ed51de4a69)

We highly recommend using Mamba to speed up the creation of the Conda environment. To install it, simply use `conda install mamba -c conda-forge` in the terminal you just opened:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/f3aac01e-1d59-476a-8311-bf69e54429f5)

Create an empty environment named `mlforecast` with the following command: `mamba create -n mlforecast python=3.10`:

<img width="1439" alt="image" src="https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/cf0b5f5d-b004-4fbb-9874-4457f827d1b7">

Activate the newly created environment using `conda activate mlforecast`:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/1562e347-6c6c-48dd-9cf7-1dc81110e4fb)

Install the libraries within the environment file `environment.yml` using `mamba env update -f environment.yml`:

![image](https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/79b2b4be-db8b-405c-9205-4bd0aa2fa463)


Now install the library to make interactive changes and other additional dependencies using `pip install -e ".[dev]"`:

<img width="1440" alt="image" src="https://github.com/Nixtla/how-to-contribute-nixtlaverse/assets/10517170/c4e24f10-3c87-467e-89da-67f585e30552">

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






