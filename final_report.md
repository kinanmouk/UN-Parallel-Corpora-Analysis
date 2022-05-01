# Final Report UN-Parallel-Corpora-Analysis 
by Kinan Al-Mouk
## Table of Contents
  - [`Introduction`](#-Introduction)
  - [`Data Sourcing and Explanation`](#-Data-Sourcing-and-Explanation)
  - [`Data Cleanup`](#-Introduction)
  - [`Analysis`](#-Introduction)
  - [`Conclusion`](#-Introduction)
  - [`Sources`](#-Sources)

## Introduction
For my term project in Na-Rae Han's Data Science for Linguists class at the University of Pittsburgh, I chose to use the [United Nations' Sixway Parallel Corpus](https://conferences.unite.un.org/uncorpus).

## Data Sourcing and Explanation
This corpus was sourced from the [UN website](https://conferences.unite.un.org/uncorpus). The UN Parallel Corpus is composed of official parliamentary documents, records, and other documents within the public domain that are available in the six official languages of the UN. Those languages are: English, Spanish, French, Russian, Mandarin Chinese, and Arabic. The current version as of May 1st 2022 contains documents created and manually translated between 1990 and 2014. 

The files were downloaded from the source. It states on the website that each document was in `XML` file format with embedded meta-information of the **Symbol** of the official UN document, it's **translation job number**, the **publication date**, the **processing location**, and the **keyword** which determined the document subject.

The value behind using this corpus is that it allows for accesss to multilingual language resources. Oftentimes in technological and ML advancements today we see issues of accessibility for multilingual users as well as L2 speakers of a language of higher prestige. In using UN data I am sure that the data collected represents each of the six UN official langauges to the highest translation standard. 

## Data Cleanup

Cleaning the data for proper use proved to be one of the most difficult tasks of this term project. Each of the `zip` six files downloaded from the [UN website](https://conferences.unite.un.org/uncorpus) were large in size. The largest file being **800 MB**. After unzipping the `tar` files took up a total of **12 GB** of space on my computer.

After opening each file in a text viewer it was clear that each document was not in `XML` file format but in `.txt` format. I explored the new `.txt` file format using the English document and found that there were over 2 billion lines. There were no text markers that I could have used to seperate each document based on the embedded meta-information that was described in the XML format. 

I then moved into [Juypter Notebook](https://jupyter.org/) to begin processing the English text file which was **4.44 GB**.

After several trial and error attempts in seperating each UN document within the large English file, I used command line to slice the document into the first 100k lines labeled it as [`english.100k`](#english). I continued this process with each of the language files, each of them can be found in [`data-samples/`](https://github.com/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/data-samples/).

The next step in processing was reading the files in for use in [Juypter Notebook](https://jupyter.org/). Again I began with English in order to best analyze how the file was being loaded and presented. 

## Analysis
## Conclusion

## Sources
Ziemski, M., Junczys-Dowmunt, M., and Pouliquen, B., (2016), The United Nations Parallel Corpus, Language Resources and Evaluation (LREC’16), Portorož, Slovenia, May 2016.


