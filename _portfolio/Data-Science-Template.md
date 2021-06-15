---
title: "Data Science team Project Template"
excerpt: "Providing a consistent structure to a data science team project aids in providing reproducibility, encouraging solution exploring while keeping production goals in mind."
header:
  image: /assets/images/cookiecutter.jpg
  teaser: /assets/images/cookiecutter.jpg
sidebar:
  - title: "Role"
    image: "/assets/images/bio-photo.jpg"
    image_alt: "logo"
    text: "Designer, Front-End Developer"
  - title: "Responsibilities"
    text: "standardizing new data science team structure"
gallery:
  - url: /assets/images/cookiecutter.jpg
    image_path: assets/images/cookiecutter.jpg
    alt: "creating a new project from template"
  - url: /assets/images/2b-cmd_tree_censord.PNG
    image_path: assets/images/2b-cmd_tree_censord.PNG
    alt: "standard project structure"
---

I was hired into a brand new division in the company. They were trying to establish a data science team that could service current customers that were not big enough to require their own data science team.
We were initially a two man team that leveraged the knowledge of other colleagues. Expecting the team to grow and be active in multiple smaller projects I created a template for a project structure that future team members can used for consistency.
I worked off the premise that "Providing a consistent structure to a data science team project aids in providing reproducibility, encouraging solution exploring while keeping production goals in mind."
I assumed that the new hires would be very green and starting out in this structure would aid in getting them up to speed in other projects when they switch.

It is a living template that would mature as the team experience matures. There are not many dogmatic rules except that the initial raw data should be treated as immutable and any wrangling should be done on a copy of the raw data. The structure of each individual template would vary slightly based on the needs of the project, but it would not be changed drastically so that new team members would intuitively be able to find necessary files.

{% include gallery caption="Some screenshots of implementation" %}

There are two documents that are included with each project.
The first [document](https://github.com/Wahe3bru/DataScienceTeamProjectTemplate/blob/master/%7B%7Bcookiecutter.directory_name%7D%7D/docs/admin/Creating_new_project.md)explaining the template, the rationale as well as the expected workflow.

The second document explains the [coding style](https://github.com/Wahe3bru/DataScienceTeamProjectTemplate/blob/master/%7B%7Bcookiecutter.directory_name%7D%7D/docs/reference_material/CodingStyle-Python.md) to be used with examples for illustration.
Below a sample taken from the document on coding style.
```
Put all imports at the top of the page with three sections,
 each separated by a blank line, in this order:

1. System imports
2. Third-party imports
3. Local source tree imports

_Rationale:_ Makes it clear where each module is coming from
```
The key ideas being reproducibility and code creating with production in mind.
 So more testable functions would be created instead of hardcoded variables. Functions and code overall would be refactored multiple times and encouraging coding best practices from the start ensures efficient usage of everyone's time. In the future I envision project documentation being automatically generated, as well as automatically generated reports. Testing would be encouraged and eventually a  library of well-tested functions would be developed speeding up development time.
