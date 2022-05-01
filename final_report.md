# Final Report UN-Parallel-Corpora-Analysis 
by Kinan Al-Mouk
## Table of Contents
  - [`Introduction`](#-Introduction)
  - [`Data Sourcing and Explanation`](#-Data-Sourcing-and-Explanation)
  - [`Data Cleanup`](#-Introduction)
  - [`Analysis`](#-Introduction)
     -  [`Computational Methods`](#-Computational-Methods)
     -  [`Linguistic Analysis`](#-Linguistic-Analysis)
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

I then moved into [Juypter Notebook](https://jupyter.org/) to begin processing the English text file which was **4.44 GB**. Due to the size, it took around 12 minutes for the file to be read into Juypter. The Mandarin file took 32 minutes. After working around in these files in Juypter, the program and cell kernels would die because of the size of files in processing. 

After several trial and error attempts in seperating each UN document within the large files, I used command line to slice the English document into the first 100k lines labeled it as [english.100k](#english). I continued this process with each of the language files, each of them can be found in [`data-samples/`](https://github.com/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/data-samples/).

The next step in cleaning was reading the workable files in for use in [Juypter Notebook](https://jupyter.org/). Again I began with English in order to best analyze how the file was being loaded and presented. Using the `time` method I found that the new workable files were read within around 20 seconds. 

## Analysis
### Computational Methods

I first began processing each language using `nltk` for **word tokenization** and **sentence tokenization**. This worked effectively for English however fell short in other languages as `nltk` is not specifically designed for multilingual processing. This error was captured in word tokenization of the [mandarin.100k](#mandarin). 

As you can see in the [`pandas` dataframe](https://nbviewer.org/github/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/UN_Data_Analysis.ipynb#DataFrame-Construction), the **Word_Tokens** column shows the `nltk` word tokenization of each UN language. The last row of the column shows '1994年5月17日安全理事会第3377次会' ("Security Council of May 17, 1994") being treated by `nltk` as one token. The proper way to tokenize this Mandarin text would have been ["1994年", "5月", "17日", "安全", "理事会"].

After researching other ways to process a multilingual parallel corpus, Na-Rae suggested the use of `SpaCy`. `SpaCy` supports the use of over 64 langauges, however the difference between this and `nltk` is that it allows for linguistically-motivated tokenization, named entity recognition, part-of-speech tagging, dependency parsing, and sentence segmentation. It is a super power processor. 

I then created a new Juypter notebook file for processing labeled [`DataProcessing.ipynb`](https://github.com/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/DataProcessing.ipynb) for using `SpaCy` as my main NLP tool.

[In the notebook](https://nbviewer.org/github/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/DataProcessing.ipynb#Downloading-SpaCy-object-for-English-processing) I downloaded the SpaCy object for processing each language seperately. I created a slice of 1 million characters in order to train the `SpaCy` nlp document without an increase in error rate as according to the website. Using the `time` method it can be observed that it took about 82 seconds for the document to be trained using SpaCy's English module. 

I then moved on to [word tokenization](https://nbviewer.org/github/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/DataProcessing.ipynb#Word-Tokenizing-Mandarin-Document) where it can be observed that SpaCy's Mandarin module properly trained the Mandarin document to tokenize '1994年5月17日安全理事会第3377次会' as ["1994年", "5月", "17日", "安全", "理事会"] in only 2 seconds. 

SpaCy worked properly in processing each UN langauge with the exception of Arabic. There is no module available today for Arabic procesing on their website. After researching other Arabic NLP resources for use I discovered [CAMeL Tool Kit](https://aclanthology.org/2020.lrec-1.868/) which is a suite of Arabic NLP tools developed at NYU Abu Dhabi.

Despite finding CAMeL, it was unable to be used accurately in my parallel corpora analysis due to slight differences in its tools. Its POS tagger did not use the same labels as that of `SpaCy's`, it  does not have a way to sentence tokenize, and also has a lower processing power than `SpaCy`. using this tool would have undermined the parallel aspect of my data collection and analysis. I hope to use it in the future as it is a tool that interests me greatly as an Arabic speaker.

I chose to continue with using SpaCy and ultimately had to put off Arabic processing to the side in order to maintain parallel processing for accurate linguistic comparison and analysis. 

### Linguistic Analysis
All analysis in this section is with `SpaCy` findings.

My goal with processing the UN Parllel corpus was to make lingusitic comparisons between six widely spoken, learned, and political languages based off of average word length, sentence length, etc. 

**Word Tokenization** 
Taking a look at the `pandas` dataframe created in [`DataProcessing.ipynb`](DataProcessing.ipynb) the first four columns show the [language, document, word_tokens, and word_token_length](https://nbviewer.org/github/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/DataProcessing.ipynb#Creating-DataFrame-for-Analyzation) of each language. 



## Conclusion

## Sources
Ziemski, M., Junczys-Dowmunt, M., and Pouliquen, B., (2016), The United Nations Parallel Corpus, Language Resources and Evaluation (LREC’16), Portorož, Slovenia, May 2016.


