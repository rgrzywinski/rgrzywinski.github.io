---
layout: post
title:  Source Code Summarization
subtitle: State-of-the-art research into techniques for summarizing source code
description: XXX
date: 2016-04-06 01:23:45
categories: Research
comments: true
---
*This series of posts captures my current work-in-progress ideas and resulting research.*

## The Problem

I believe McBurney _et al._ articulated the problem well in "[An empirical study of the textual similarity between source code and source code summaries](http://www3.nd.edu/~cmc/papers/mcburney_emse15.pdf)"

> There is a mismatch between [software] authors and readers. Authors translate the high-level concepts into low-level implementation, whiler eaders  must deduce the concepts and  behaviors from the low-level  details. The  readers struggle to understand the author’s intent, and inevitably make mistakes in their understanding. At the same time, authors who write documentation of their source code must choose which key concepts and details to communicate to readers via documentation. The concepts and details described in documentation are the ones that authors believe readers would need to know.

In my personal experience, one of the largest barriers for entry to contributing changes to a project is simply understanding the composition of the source code. If you've ever cracked open a repository of source code then you know the problems of just figuring out where to begin diving in. Over the years many techniques have been developed to combat this -- source code documentation, UML, design patterns and naming conventions are just a few. Most of these techniques require manual effort to create and maintain. 

My hypothesis is this: if it's possible for me to manually grok an undocumented repository and walk away with an understanding of its structure, function and general purpose then I should be able to get a computer to accomplish the same task. Having an automated system is useful beyond the obvious use case of "documentation generation". It would provide for an automated "pair" (as in "pair programming") in that the summarized natural language can be a source of continual feedback to the source code author. Assuming a sufficiently correct summarization tool exists then if the summary is incorrect, confusing, incomplete, etc then the author can make immediate modifications to the source code. XXX

This post focuses on source code summarization techniques, their pitfalls and some thoughts on future directions. Other aspects of "program comprehension" will be covered in future posts.

## SOMETHING

(Cross-cut the papers by reviewing the problem statement, and overview the different techniques that are used. Use http://www.languageandcode.org/nlse2015/neubig15nlse-survey.pdf as a baseline?)
* Techniques
* Problems


## Papers

**Neubig, Graham. "[Survey of Methods to Generate Natural Language from Source Code.](http://www.languageandcode.org/nlse2015/neubig15nlse-survey.pdf)"(2015)**

An informal survey of methods for generating natural language from source code. It covers a broader scope than this blog post and is a great starting point. 

**Hill, Emily, Lori Pollock, and K. Vijay-Shanker. "[Automatically capturing source code context of NL-queries for software maintenance and reuse.](https://www.researchgate.net/profile/K_Vijay-Shanker/publication/221554137_Automatically_capturing_source_code_context_of_NL-queries_for_software_maintenance_and_reuse/links/55760c1b08ae7521586c2b28.pdf)" Proceedings of the 31st International Conference on Software Engineering. IEEE Computer Society, 2009.**

SKIP?

**McBurney, Paul W., and Collin McMillan. "[Automatic Documentation Generation via Source Code Summarization of Method Context.](http://www3.nd.edu/~pmcburne/papers/gensum.pdf)" (2014).**

The authors succinctly state that a "more effective" documentation generator needs to help the programmer understand:
> 1. what the methods do internally,
> 2. why the methods exist, and
> 3. how to use the methods

Their approach uses PageRank against the static call-graph to provide context for each method coupled with the Software Word Usage Model (SWUM) which extracts nouns, verbs and prepositional statements from source code and provides results that are better than the state-of-the-art.

**Fowkes, Jaroslav, et al. "[Autofolding for Source Code Summarization.](http://arxiv.org/pdf/1403.4503.pdf)" arXiv preprint arXiv:1403.4503 (2014).**

**Fowkes, Jaroslav, et al. "[TASSAL: Autofolding for Source Code Summarization.](http://homepages.inf.ed.ac.uk/jfowkes/icse2016-demo.pdf)"**

The authors focus on summarization for the purposes of automatic code folding. Their goal is to achieve a "compression ratio" of the source by folding elements that are less useful in understanding the content in question -- this is in effect a summary of the source. Tree-based Autofolding Software Summarization ALgorithm (TASSAL) is introduced which is an Abstract Syntax Tree (AST) based approach that leverages a latent Dirichlet allocation (LDA) topic model (specifically, it extends TopicSum which is a hierarchical topic model) using different scopes (e.g. project, file and method) to produce a model that is then used to obtain a rooted contiguous subtree that best characterizes the element in question. 

The authors also provide a succinct set of cases in which different forms of summarization can be used: "first look" in which a developer new to the project simply needs an overview of the algorithms used, debugging and code reviewing. 

**Ying, Annie TT, and Martin P. Robillard. "[Code fragment summarization.](http://www.annieying.ca/papers/esecfse2013.pdf)" Proceedings of the 2013 9th Joint Meeting on Foundations of Software Engineering. ACM, 2013.**

The authors focus on summarization for the purposes of presenting a useful code snippet in search results. Support Vector Machines (SVM) and Naive Bayes models were generated based on hand-picked features. both performed better than simply chosing either the first-N or last-N lines of code or by chosing those lines that have the most number of matching terms.

**McBurney, Paul W., and Collin McMillan. "[An empirical study of the textual similarity between source code and source code summaries.](http://www3.nd.edu/~cmc/papers/mcburney_emse15.pdf)" Empirical Software Engineering 21.1 (2016): 17-42.**

A fascinating read that highlights the challenges involved when creating source code summaries: summaries created by source code _readers_ differ from those summaries created by source code _authors_ and that there is varying accuracy of these summaries when compared against the actual source code. It attributes the root causes of these challenges to the different strategies that developers use to understand source code (_systemic_ to understanding how the components of software interact and _opportunistic_ to understand how to modify a section of code) and the difficulty in measuring the quality of summaries (multiple techniques such as Short Text Semantic Similarity are reviewed).

**Moreno, Laura, et al. "[Automatic Generation of Natural Language Summaries for Java Classes.](http://ieeexplore.ieee.org/xpl/login.jsp?tp=&arnumber=6613830)" Program Comprehension (ICPC), 2013 IEEE 21st International Conference on. IEEE, 2013.**

The authors focus on summarization of classes "as they are the primary decomposition unit in Object-Oriented (OO) programming languages" with a goal of supporting rapid understanding of the class' intent rather than "its context and any algorithmic details." The stereotype(s) of the class in question are determined using a rules-based approach and then heuristic- and access-based filters based on the class' stereotypes(s) are applied to the method stereotypes. SWUM and templates are thenused to generate the resulting summaries.

**Haiduc, Sonia, et al. "[On the use of automated text summarization techniques for summarizing source code.](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.228.2460&rep=rep1&type=pdf)" Reverse Engineering (WCRE), 2010 17th Working Conference on. IEEE, 2010.**

The authors apply standard automated text summarization based techniques on text retrieval to source code. Their focus is on term-based rather than natural language summaries. The best performing techniques were created by combining lead summaries (where initial terms in a document are weighted highly) and Vector Space Models (VSM), noticing that smaller summaries were not necessarily better and using TF-IDF weighting. (I personally like how systematic this paper is in its approach.)

**Eddy, Brian P., et al. "Evaluating source code summarization techniques: Replication and expansion." Program Comprehension (ICPC), 2013 IEEE 21st International Conference on. IEEE, 2013.**

The author's extend the work of Haiduc _et al._ by using a hierarchical  pachinko allocation model (hPAM) which were found to perform worse than VSM. In fact, the authors found that very simple heuristics involving the identifiers produce summaries that are very close to the human ones. They spend much time trying to understand how humans perform term-based summarization which I believe is funamentally flawed due to their use of undergraduate students as a reference. Unskilled developers will tend to rely on simple heurestics (as they haven't even been introduced to higher-order concepts much less have the necessary synthesis skills) which is what the authors found.

**McBurney, Paul W., et al. "[Improving topic model source code summarization.](http://www3.nd.edu/~cmc/papers/mcburney_icpcera_2014.pdf)" Proceedings of the 22nd International Conference on Program Comprehension. ACM, 2014.**

The authors imploy the Hierarchical Document Topic Model (HDTM) which uses a non-parametric Bayesian graphical model to generate a hierarchy of keywords derived from the keywords of each method. (It is not obvious in the paper how the keywords are determined.)

**Fudaba, Hiroyuki, et al. "[Pseudogen: A Tool to Automatically Generate Pseudo-Code from Source Code.](http://www.phontron.com/paper/fudaba15asedemo.pdf)" Automated Software Engineering (ASE), 2015 30th IEEE/ACM International Conference on. IEEE, 2015.**

The authors apply statistical machine translation (SMT) to generate pseudocode from a parse tree. Translation rules are created from human-generated pseudocode.

**Wong, Elaine, Jinqiu Yang, and Lin Tan. "[AutoComment: Mining question and answer sites for automatic comment generation.](https://ece.uwaterloo.ca/~lintan/publications/autocomment-ase13.pdf)" Automated Software Engineering (ASE), 2013 IEEE/ACM 28th International Conference on. IEEE, 2013.**

The authors step outside of the boundaries of the source code itself and suggest using Q&A websites such as StackOverflow to provide summaries to source code snippets. A search using a modified code-clone detection technique is performed on the Q&A website's code snippets. The text description of highly-rated matching responses are used to generate the summary. 

Some of the challenges of this technique lie in the content on the Q&A website itself which typically focus on troubleshooting rather than describing code. These are mitigated with heuristic and natural language processing techniques.

**Wong, Edmund, Taiyue Liu, and Lin Tan. "[CloCom: Mining existing source code for automatic comment generation.](https://www.ece.uwaterloo.ca/~lintan/publications/clocom-saner15.pdf)" Software Analysis, Evolution and Reengineering (SANER), 2015 IEEE 22nd International Conference on. IEEE, 2015.**

The authors extend their "AutoComment" work from Q&A websites to other repositories in GitHub in order to leverage existing comments. Clone detection is used to find source code that is similar to the source in question. Effort is made to "prune out project specific comments" and well as match context.

**Panichella, Sebastiano, et al. "[Mining source code descriptions from developer communications.](https://www.researchgate.net/profile/Sebastiano_Panichella/publication/230735390_Mining_Source_Code_Descriptions_from_Developer_Communications/links/09e41503b890006b61000000.pdf)" Program Comprehension (ICPC), 2012 IEEE 20th International Conference on. IEEE, 2012.**

**Vassallo, Carmine, et al. "[CODES: mining sourCe cOde Descriptions from developErs diScussions.](https://www.researchgate.net/profile/Sebastiano_Panichella/publication/266657926_CODES_mining_source_code_descriptions_from_developers_discussions/links/55cb0f8c08aebc967dfbfa5b.pdf)" Proceedings of the 22nd International Conference on Program Comprehension. ACM, 2014.**

Similar to "AutoComment", the authors step outside of the source code itself and suggest using bug reports, emails, mailing lists and Q&A websites to provide summaries to source code snippets. Because the authors focus on method summarization rather than snippets (as with "AutoComment") the search technique is brute-force: if an artifact contains the fully-qualified class name or filename then it is a match. Heuristics are used to identify and filter which paragraphs summarize the method.

**Rahman, Mohammad Masudur, Chanchal K. Roy, and Iman Keivanloo. "[Recommending insightful comments for source code using crowdsourced knowledge.](http://homepage.usask.ca/~masud.rahman/papers/masud-SCAM2015.pdf)" Source Code Analysis and Manipulation (SCAM), 2015 IEEE 15th International Working Conference on. IEEE, 2015.**

The authors posit that simply describing the functionality of the source code via summarization is insufficient. To be truly useful, the system should highlight any known quality issues associated with the code. I agree with their assessment and believe that it should be added to the list of qualities that McBurney _et al._ propose for a "more effective" documentation generator.

Following the lead of the previous papers the authors look outside of the source code itself to Q&A websites for the necessary information. The authors go beyond Wong _et al._ by including the available follow-up discussions. Searching is performed using topic modeling (specifically, Latent Dirichlet Allocation (LDA)), a modified version of PageRank is used to rank the results and numerous heuristics are used to filter less important results.

Given that this technique is outside of the scope of pure summarization I will not focus on it.

**Treude, Christoph, and Martin P. Robillard. "[Augmenting API documentation with insights from Stack Overflow.](https://hekyll.services.adelaide.edu.au/dspace/bitstream/2440/98061/3/hdl_98061.pdf)" (2016).**

The authors highlight that Q&A websites contain information that is different from that which is traditionally found in API documentation such as "design, rationale, usage scenarios and code examples." Their goal was to suppliment API documentation with "insightful sentences" extracted from Q&A websites.

Two standard unsupervised natural language summarization techniques, LexRank and Maximal Marginal Relevance (MMR), were applied to the top answers from a Q&A website associated with the API in question and were found to perform poorly. A pattern-based approach tailored to extract fragments of API documentation known to be useful performed similarly to the unsupervied approaches. A supervised approach (using random forests and support vector machines) called Supervised Insight Sentence Extractor (SISE) was created leveraging a plethora of features and was found to be superior to the other techniques.

**Cortés-Coy, Luis Fernando, et al. "[On automatically generating commit messages via summarization of source code changes.](https://www.researchgate.net/profile/Luis_Cortes11/publication/267326224_On_Automatically_Generating_Commit_Messages_via_Summarization_of_Source_Code_Changes/links/5583f12208ae4738295bd3ca.pdf)" 2014 IEEE 14th International Working Conference on Source Code Analysis and Manipulation (SCAM). IEEE, 2014.**

**Linares-Vásquez, Mario, et al. "[ChangeScribe: A Tool for Automatically Generating Commit Messages.](http://www.cs.wm.edu/~denys/pubs/ICSE'15-ChangeScribeTool-CRC.pdf)" Proceedings of the 37th International Conference on Software Engineering-Volume 2. IEEE Press, 2015.**

Because source code changes over time, in order to fully understand a system it may be essential to walk through those changes. By automatically summarizaing source code changes this task can be simplified. The authors of this paper approach source code summarization from this perspective.

The authors suggest that a method's stereotype provides a basis of its intent and therefore is useful in summarization. A set of rules that leverage the stereotype and any changes to it are manually created to generate the summarization. Based on the type of change, other heuristics such as the class' stereotype and simply listing the names of the elements that have changed are used in the summary.

**Li, Boyang, et al. "[Automatically Documenting Unit Test Cases.](http://www.cs.wm.edu/~denys/pubs/_ICST'16-JUnitTestScribe-CRC.pdf)" 2016 IEEE International Conference on Software Testing, Verification and Validation (ICSE). IEEE, 2016**

Unit tests and the documentation that co-evolves with them provide another point-of-interest for source code summarization. Assertions (such as `Assert.isNotNull()`) for example provide a rich source of easily summarizable content. The authors identify "focal methods" -- those methods that are "responsible for applicationstate changes that are verified through assertions in the unit test" -- as critical methods to summarize. They use a combination of class and method stereotypes, SWUM, and path analysis to identify features to use in their summaries.

**Pham, Raphael, Yauheni Stoliar, and Kurt Schneider. "[Automatically recommending test code examples to inexperienced developers.](http://www.se.uni-hannover.de/pub/File/pdfpapers/Pham2015.pdf)" Proceedings of the 2015 10th Joint Meeting on Foundations of Software Engineering. ACM, 2015.**

The authors noticed that novice developers tend to look for examples (e.g. of unit tests) and copy and change those examples to fit their situation resulting in what they call "example-centric programming". I posit that a similar technique could be used for summary generation: given a snippet of code for which a summary is desired, a search is performed against code that already has a suitable summary (either human provided or machine generated) associated with it and that summary (perhaps modified based on context) is used as a result.


## Unavailable Papers

**McBurney, Paul W., Cheng Liu, and Collin McMillan. "Automated feature discovery via sentence selection and source code summarization." Journal of Software: Evolution and Process 28.2 (2016): 120-145.**



## Software

* [Source Code Fragment Summarization with Crowdsourcing Based Features](http://oscar-lab.org/CFS/)
* [Automatic Documentation Generation via Source Code Summarization of Method Context](http://www3.nd.edu/~pmcburne/summaries/)
* [An Empirical Study of the Textual Similarity between Source Code and Source Code Summaries](http://www3.nd.edu/~pmcburne/sumalyze/)
* [Pseudogen](http://ahclab.naist.jp/pseudogen/)
* [ChangeScribe: A Tool for Automatically Generating Commit Messages](http://www.cs.wm.edu/semeru/changescribe/)
* [CODES: mining sourCe cOde Descriptions from developErs diScussions](http://www.ing.unisannio.it/spanichella/pages/tools/CODES/)
* [CloCom](http://asset.uwaterloo.ca/clocom/)
* [Tree-based Autofolding Software Summarization Algorithm
 (TASSAL)](https://github.com/mast-group/tassal)


## Editorial

XXX My concern with much of the research in this space is that the "truth" data is being provided by the researchers themselves. It has been my experience that software produced by academics differs greatly from software produced by industry. Much of the source code available via Open Source is of poor quality and strays far from software engineering best practices. (To be fair, most industry software I have encountered is also of poor quality. This may be simply due to a selection bais -- I have spent most of my career as the resource that is brought in to replace existing systems.) 

In addition, most Open Source software that is publically available are either libraries or interal tools XXX such as databases or operating systems rather than products XXX. This represents a significant bias against where the bulk of industry developer time is spent.

Specifically to the desire to preserve generated commit messages I find much fault. If the commit message can be generated from the existing source available in the repository then it should simply be generated each time it is needed as that allows for improvements to be made to the generator. The only meta-data that should be stored with the commit should be that which cannot be derived from the existing source.


Unfortunately I believe that the authors have confused topic-based summarization with "functionality" summarization. There is much more to summarization than to convey what the element does. For example, identifying what role(s) the element plays within its local and global context is critical to summarization.


By providing and having always enabled summarization, the software author is directed to provide meta-data that cannot be determined from the source code directly (or is in fact directly in conflict with an understanding that would be gleaned only from the source code) and therefore is providing the highest value information.




