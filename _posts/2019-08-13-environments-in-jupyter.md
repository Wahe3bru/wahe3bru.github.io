---
title: "Environments in Jupyter"
last_modified_at: 2019-08-13T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - Jupyter
  - notes
  - tutorial
classes: wide
---

Best practice when working with Python is to use environments.
The are a plethora of tools to help you with that but I chose the built it Conda - as I use the [Anaconda](https://www.anaconda.com/distribution) platform on my pc.

The benefits of separate environments are [numerous](https://protostar.space/why-you-need-python-environments-and-how-to-manage-them-with-conda). But basically, you want to make sure that the specific library you used for your project does not break your code when you update the library for another project (or improved features).

Especially when you use libraries that need specific versions of other libraries that require upgrading/downgrading. If you are within an environment you can be sure that your other projects are safe.

#### Create environment
To create create an environment with the name "test-env" with a specific python version of 3.6.3:
`conda create -n test_env python=3.6.3`
*the `python=<python version>` is optional, and if left out will default to the base python installed.
I can install other libraries if necessary or create the environment with the libraries installed using a file that already lists the required libraries.

The next step would be to add the virtual environment to Jupyter Notebook/Lab

- activate environment (test_env):
   `conda activate test_env`
- install kernal:
   `pip install --user ipykernal`
- add virtual environment to Jupyter:
   `python -m ipykernel install --user --name=test_env`

When creating a new notebook you can select the kernel (ie environment) required.

!["available kernels"](/assets/images/lab-env.png)

#### happy coding!
