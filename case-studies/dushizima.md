##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is Daniela Ushizima, and the bulk of my research work is in devising machine vision and pattern recognition algorithms as part of software tools for handling image data, especially those arising from Department of Energy imaging facilities. I am currently a staff scientist at Lawrence Berkeley National Laboratory and a Data Science Fellow in the Institute for Data Science at the University of California, Berkeley.
The case study I describe illustrates the main steps in designing a machine vision algorithm that analyzes a set of digital images and separates them according to the desired criteria. There are several image processing and analysis algorithms, and this case study will use ImageJ, a popular image processing tool. ImageJ was developed by Wayne Rasband within NIH, originally focusing on medical imaging, however this software has been widely used in other applications, such as material sciences.

2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

I consider a study to be computationally reproducible when my collaborators can transform raw data files into quantifiable patterns through the proposed code, obtaining the same results from previous analyses. Because algorithmic parameters often change from a dataset to another, it can be challenging to get results with the same accuracy, given different datasets.

##### Workflow diagram

[Diagram](dushizima.pdf)

##### Workflow narrative

The workflow follows a data model called SIPOC, which stands for suppliers, inputs, process, outputs, and customers which form the columns of the table. We adapt SIPOC to better represent our use-case, hence the first column is called sources and the final column repositories. The proposed workflow prioritizes the compartmentalization of different processing steps of the analysis system, and hides potential feedback loops that might occur.

In close collaboration with pathologists and cytologists, the goal is to design algorithms for improving the analysis of images. Some of the tasks include increasing the number of fields under scrutiny, speed up cell counting and recognition, comparison among cells, quantitative description of samples, to name a few.

Historically, this use-case begun with brainstorming among pathologists, physicist and software engineers on how to deal with the available large datasets of digital images with respect to cervical cells. Brainstorming and diagraming were fundamental to understand how to well characterize types of cells and foresee limitations imposed by the datasets, such as magnification and usable area within sample.

In order to accomplish these tasks, the team organized the datasets into three main *input* image sets: simulated, real and curated. A simulated image consists of several clipped real cells collated with different levels of overlapping, which facilitates validating algorithms since the ground-truth is known  a priori. A real image is the digital picture of a Pap smear slide, which often contains several cells and other objects, and may be corrupted by noise and other artifacts, such as staining variations, dirt, etc.

The core of this case study lies in the *process* column that illustrates the main steps for the image analysis. The preprocessing step transforms the samples into more reliable representations of the image, for example, removing areas of or the whole image if it is over-stained. This step includes essential image transforms, such as anisotropic filtering to preserve borders and smooth regions that are mostly homogeneous.

As part of the process, the software tool must detect the regions of the interest in each image, i.e., the cellular mass, as opposed to background. While the definition of the problem might seem easy, this step might take a long time to evolve into an algorithm that can correctly split the image into foreground and the rest of the image. The next step is to separate the cellular mass into individual cells: by modeling simple biological prior knowledge, such as, relationship between nucleus and cytoplasm, the algorithm is able to quickly estimate cytoplasm boundaries. After identification of the cells, feature extraction takes place, including nucleus-cytoplasm area ratio, convexity of cytoplasm contour, and other parameters that are relevant on identifying cell lineage. Finally, we use simulated and curated datasets to validate results, for example, considering sensitivity and specificity measures based on the number of pixels or the number of cells identified.

An important step of the data processing is keeping track of the *outputs*. The forth column lists 4 main outputs of the system: technical reports, scientific papers, documentation about the software tool and educational videos about the science problem and algorithm developments. Although the diagram omits output of partial results, they are very common and useful outputs throughout the design of the software tool.

The fifth column shows the main *consumers* of the outputs. In the context of this case study, it indicates the main hubs of information distribution about the project.


##### Pain points
*Describe in detail the steps of a reproducible workflow which you consider to be particularly painful. How do you handle these? How do you avoid them?*

The software tool design and testing required intense communication among team members through reports and presentations. Although part of team used version control, much of the code is still to be made available open-source through Github. Because commit messages tend to be short, technical reports developed as a diary of activities were fundamental to keep the whole team up to speed. The painful side of diary or electronic lab books was mostly the free form of inputs that may require extra-time to understand.

##### Key benefits
*Discuss one or several sections of your workflow that you feel makes your approach better than the "normal" non-reproducible workflow that others might use in your field. What does your workflow do better than the one used by your lesser-skilled colleagues and students, and why? What would you want them to learn from your example? (200-400 words)*

The most reproducible part of this project has been the use of code applied to simulated datasets. This task improved among the team particularly due to participation in code competitions, which forced the whole team to organize data sources and code for easy re-run by reviewers. Keeping track of advancements in a common digital lab book helped considerably in preparing manuscripts and other technical reports.


##### Key tools
*If applicable, provide a detailed description of a particular specialized tool that plays a key role in making your workflow reproducible, if you think that the tool might be of broader interest or relevance to a general audience. (200-400 words)*

An important tool that we started using is Overleaf for latex-text collaboration over the internet, which improved our ability to quickly edited our manuscripts as a group.

##### General questions about reproducibility

*Please provide short answers (a few sentences each) to these general questions about reproducibility and scientific research. Rough ideas are appropriate here, as these will not be published with the case study. Please feel free to answer all or only some of these questions.*

1) Why do you think that reproducibility in your domain is important?

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

4) What do you view as the major incentives for doing reproducible research?

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?
