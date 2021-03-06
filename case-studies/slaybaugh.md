##### Introduction
*Please answer these introductory questions for your case study in a few sentences.*

1) Who are you and what is your research field? Include your name, affiliation, discipline, and the background or context of your overall research that is necessary specifically to introduce your specific case study.

My name is Rachel Slaybaugh and I am an Assistant Professor in the Nuclear Engineering Department at the University of California, Berkeley.
I study computational methods for neutron transport: numerical methods for solving the Boltzmann equation applied to neutral particle interactions. 
The methods I study are both deterministic (e.g. finite difference, etc.) and stochastic (Monte Carlo).
I develop these algorithms for reactor design and analysis, radiation shielding, and nuclear nonproliferation applications. 
Much of my work has an emphasis on high performance computing. 
(Tagline: intersection of applied math and computational science, informed by nuclear engineering)


2) Define what the term "reproducibility" means to you generally and/or in the particular context of your case study.

The first way I think of reproducibility is "can I/my lab reproduce the results in my paper exactly?" 
After that, "can an independent researcher, given that they have legal access to the required data and software, reproduce the results?" 
Nuclear engineering data and codes are often controlled, so for many projects only researchers within my field will have access to the required data and software. 
Fortunately, such non-open-source codes are typically available at no cost to researchers through a simple licensing process. 

##### Workflow diagram

[Diagram](slaybaugh.pdf)


##### Workflow narrative

I tend to think of my workflow for code development as having three fundamental steps:
  (1) idea generation and refinement,
  (2) idea implementation and testing, and
  (3) large scale testing and publication.

**Step 1**:
The starting point of a new project is the development of an algorithm.
This comes from a combination of reviewing literature, discussion with colleagues, familiarity with challenges in the field, etc.
As I refine an idea, I find I need to do more literature review, and as I research more background information, I refine the idea.
The algorithm development tends to be collaborative as it is based on discussions with others, but the lit review tends to just be me.
I like to write the lit review in LaTeX and keep it in a repository with all of my other notes and reviews so I only have one place to look for things I have researched in the past.

Next, I implement a simplified version of the algorithm to make sure that it works at all. 
For example, I would implement a 0D (as opposed to 3D) version of a method quickly and simply in Python to use for testing.
In this step there can be iteration between the algorithm idea and the test code, informed by additional literature review as necessary. 
Once satisfied with the experiments with the simple code, the algorithm is considered "final" (though of course it can be adjusted later if needed).
I am not sure that this part of the workflow is reproducible in the sense that the process could be exactly replicated, but version controlling everything at least makes it possible to recover intermediate steps, which in some ways allows the idea refinement to be traced back. 

**Step 2**:
Once there is a finalized algorithm, it gets implemented in the "real" code that has multiple developers and is written in a compiled language like C++.
The repository for the code is typically private because, as mentioned, these codes are not completely open.
It is often the case that only one or a very few people are working on this idea, so we make a branch and do the development there.
I add unit tests to a testing framework associated with the code as I go (for example GoogleTest); the tests reside in the same repository as the main code. 
As the code approaches completion, I use small test problems to investigate basic system functionality: does the code get the correct answer for analytical/known solutions? what does basic performance look like? etc. 
The small tests are also version controlled--and that can be in the same repository or a separate one.

Once the unit tests are deemed sufficient and, combined with the small tests, everything indicates that code is correct, I finalize documentation. 
I use Doxygen to comment the code, which is useful for creating an API that can be built with the code.
However, some extra work is often required to get the theory down and provide clearer directions for using the new algorithm.
All of that is written in LaTeX for incorporation into the user manual. 
Again, all of these things are version controlled. 
At this point the code will be reviewed and merged into the main code base.
Once the code is finalized, the unit test and small test results should all be reproducible by the other developers--the people who have access to the developer repository.

**Step 3**:
Once there is "finalized" code, it is time to do the real demonstration testing for publication.
This involves running large test problems that demonstrate performance of the new algorithm for problems of interest as well as comparison to benchmarks to demonstrate correctness. 
The literature review, algorithm description, and results of the large (and sometimes small) tests will go in the final LaTeX document for journal submission.
This will also be version controlled, typically in a public GitHub repo.
The idea is that the large test input files will be in the same repository as any scripts required to process data and generate plots, all with corresponding directions. 
This means that if you have access to the code and the repository you can rerun all the calculations and process the data. 

##### Pain points
There are a few pain points: 
- Getting the documentation right. 
It seems like just using Doxygen is not enough.
To get something that really is user-manual quality you have to write a lot of things twice, just slightly differently.
I try to reuse as much as I can, but if things are replicated there is the challenge of maintaining consistency.
- Ensuring that the version of what is released in the end is actually reproducible.
This requires the extra step of documenting which version of the code was used (the results should not change in the future, but they might).
Providing directions about how to run everything and which versions of third party libraries were used is also some extra work. 
- A final pain point is re-implementing the algorithm from the simple case to the complex case, since the simple code is never really used for anything.
However, I consider this to be a pretty small issue and I do not actually mind it.


##### Key benefits
The largest key benefit is having confidence in the validity of the data that you publish.
I think everyone should have a unit testing system.
I just don't get how anyone can have confidence that they're code is correct without one. 
The ability to actually rerun a test later and get the same answer as before gives confidence as well because people can check that what you are reporting is actually true.

I also really want everyone to properly comment their code with something like Doxygen so that it is (a) easier to modify later since what is going on is clear and (b) easier to build from because there is a useful API.

The little things at the beginning that I like don't impact reproducibility, but I think they make a useful workflow. 
Having a repo with little test codes lets you play around with stuff you've already got the next time you're investigating a new algorithm.
Having a repo with lit review notes is good for remembering past research and speeds up writing.


##### Key tools
I don't think I have anything that isn't widely used. 


##### General questions about reproducibility

*Please provide short answers (a few sentences each) to these general questions about reproducibility and scientific research. Rough ideas are appropriate here, as these will not be published with the case study. Please feel free to answer all or only some of these questions.*

1) Why do you think that reproducibility in your domain is important?

The codes that we write are often used to investigate new nuclear systems and make long-term policy or design decisions based on the results. 
They are also used to study existing nuclear systems. 
This is important stuff; the codes need to be right and the results need to be verifiable. 

2) How or where did you learn the reproducible practices described in your case study? Mentors, classes, workshops, etc.

- Mentors: my PhD advisers valued reproducible practices and insisted that we used them
- Student groups: the Hacker Within
- Practice: taking on a project that used good practices was how I really learned many of these skills
- Community exposure: spending time with others who value reproducible practices 
- Self-study: looking up things I saw people do that looked helpful

3) What do you see as the major pitfalls to doing reproducible research in your domain, and do you have any suggestions for working around these? Examples could include legal, logistical, human, or technical challenges.

The biggest challenge is legal: only some people can access the codes and data required. 
A secondary challenge is access: some of the work I do requires high-performance computing that is not readily available to many.

4) What do you view as the major incentives for doing reproducible research?

*Ethical mandate*: I want my work to be right and for others to be able to know that it is right. 

*Impact*: My ideas and products might then be adopted and built upon. 

5) Are there any broad reproducibility best practices that you'd recommend for researchers in your field?

Testing, testing, testing. 

6) Would you recommend any specific websites, training courses, or books for learning more about reproducibility?

Software Carpentry; the new Scopatz-Huff book.
