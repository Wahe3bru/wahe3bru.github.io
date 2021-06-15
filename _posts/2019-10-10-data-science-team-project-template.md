---
title: Data Science Team Project Template
last_modified_at: 2019-10-10T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - cookiecutter
  - notes
  - tutorial
  - thoughts
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
excerpt: "Providing a consistent structure to a data science team project aids in providing reproducibility, encouraging solution exploring while keeping production goals in mind."
---
I was hired into a brand new division in the company. They were trying to establish a data science team that could service current customers that were not big enough to require their own data science team.
We were initially a two man team that leveraged the knowledge of other colleagues. Expecting the team to grow and be active in multiple smaller projects I created a template for a project structure that future team members can used for consistency.
I worked off the premise that "Providing a consistent structure to a data science team project aids in providing reproducibility, encouraging solution exploring while keeping production goals in mind."
I assumed that the new hires would be very green and starting out in this structure would aid in getting up to speed in other projects when they switch.

It is a living template that would mature as the team experience matures. There are not many dogmatic rules except that the initial raw data should be treated as immutable and any wrangling should be done on a copy of the raw data. The structure of each individual template would vary slightly based on the needs of the project, but it would not be changed drastically so that new team members would intuitively be able to find necessary files.

The key idea would be reproducibility and code created with production in mind. So more testable functions would be created instead of hardcoded variables. Functions and code overall would be refactored multiple times and encouraging coding best practices from the start ensures efficient usage of everyone's time. In the future I envision project documentation being automatically generated, as well as automatically generated reports. Testing would be encouraged eventually a  library of well-tested functions would be developed speeding up development time.

Below is information provided in the Readme file, as well as in the admin folder.

---

a cookiecutter project structure template
This template is used to standardize the project structure of the data science team to ensure reproducibility, consistency and a systematic workflow that could assist newer team members get up and running as soon as possible.
This structure was designed with a smaller team in mind working on small to medium size projects. The template is a guide to a consistent structure that is only minimally modified to mold to unique projects.

## Creating a new project

### Getting started
##### _requirements:_
- cookiecutter
- LSA_DS_project_template

__install cookiecutter__

`pip install cookiecutter`

__get template__

either copy LSA_DS_project_template.zip file to local pc or copy path to template
- template location: <shared folder>
- github path: https://github.com/Wahe3bru/DSprojectTemplate.git

__installation__

open terminal / command prompt <br>
change to your projects directory, then run cookiecutter followed by the path to template.

```bash
$ cd work/projects
$ cookiecutter path/to/LSA_DS_project_template.zip
# or using github url
$ cookiecutter https://github.com/Wahe3bru/DSprojectTemplate.git
```

### Initializing project template
You will have to answer a few prompted questions.<br> Some will have acceptable defaults (press `enter` to keep the default) but most will be answered by you about the project.

##### Questions to be answered:
__project_name__: default="test_project", <br>
__directory_name__: will default to the project name provided,  <br>
__project_code__: default="LSA-DS-{project_name}",  <br>
__description__: "Enter a short description of the project.",  <br>
__project_lead__: default="Waheeb Agherdien",  <br>
__lead_email__: default="Waheeb.Agherdien@gmail.com"  <br>
<br>

##### Project structure
```bash
├───data
│   ├───00-raw
│   ├───01-interim
│   └───02-processed
├───docs
│   ├───admin
│   │   └───Contact_info.docx
│   ├───project_documentation
│   │   └───Team-DoL.docx
│   ├───reference_material
│   │   └───Data-dictionary.txt
│   └───reports
│   │   └───initial_findings.ppt
├───notebooks
│   ├───01-WA-EDA.ipynb
│   ├───02-TC-EDA.ipynb
│   └───03-WA-process_features.ipynb
└───src
│   ├───01-TC-get_data.py
│   └───02-WA-process_data.ipynb
└───Readme.md
```

__data folder__ <br>
Data is typically not saved in version control but the scripts used to acquire, manipulate and store data are.

_00-raw_: The raw (unmodified) data should be stored here. This data is immutable so that when scripts are run we get the same out come i.e. reproducibility.

_01-interim_: The intermediate phase of data should be  kept here ie copy of raw data being processed - cleaning, feature engineering, combining with other sources.

_02-processed_: The finalized data - data used to train the model is stored here.

__docs__<br>
_admin_: <br>
All administrative documentation data to placed here. This would vary depending on the project but could contain contact details of the various project holders, customer IT liaison, NDA's etc.  

_project_documentation_:<br>
All documentation of the project code should be here.
Using Sphinx the documentaion can be self-generated and automated so it is always recent.

_reference_material_:<br>
All documentation, links and other supporting material that assisted team members throughout the project should be placed here. It can assist later team members get up to speed, or as reminders when the project gets picked months later.

_reports_:<br>
All generated reports, both internal and published, should be placed here sorted by date. The most up-to-date report should always be here.

__notebooks__<br>
All notebooks should be numbered sequentially followed by team members initials and a succinct title eg. `01-WA-EDA.ipynb`, `02-TK-ExploringMissingData.ipynb`


### Workflow
Exploration should be carried out in Jupyter notebooks.\
All functions that will be used should be refactored and placed into `.py` scripts so that they
can be used by other members of the team.
access functions written in .py scripts stored in src folder.
```
In [1]: %load_ext autoreload

In [2]: %autoreload 2

In [3]: from foo import some_function

In [4]: some_function()
Out[4]: 42

In [5]: # open foo.py in an editor and change some_function to return 43

In [6]: some_function()
Out[6]: 43
```
As the project matures the code will be refactored multiple times and having a separate, consistent scripts with which to access functions speeds up the coding and debugging allowing for more time and energy spent working on the solution.

##### Rationale
All EDA would be performed using Jupyter Lab/notebook. Eventually the functions created would be refactored
and stored in `.py` scripts stored in `src` folder for both reusability, be used when put in production, testing and most importantly reproducibility.
Work is not duplicated and time is saved.
So All data wrangling methods would be put in `/src/data.py` and all plotting methods in `/src/visualization.py`. This would enable members to work on different aspects of the project and be assured that the graphs created from methods from the `visualization.py` would be the right format and can be reproduced using the latest data (eg. for a representation).

reproducibility is key. All manual implementation should be documented in the steps taken in both the notebooks and in the project documentation. Project documentation should be generated using a tool like `Sphinx` to minimize overhead and once automated ensures documentation is updated.
