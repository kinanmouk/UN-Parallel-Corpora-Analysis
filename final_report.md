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

Here is a `matplot` graph showing the comparison in **word token length** for each langauge. 
![Word Tokens](https://github.com/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/new_image_files/Word_Tokens.png)

Taking a look at the `pandas` dataframe created in [`DataProcessing.ipynb`](DataProcessing.ipynb) the first four columns show the [language, document, word_tokens, and word_token_length](https://nbviewer.org/github/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/DataProcessing.ipynb#Creating-DataFrame-for-Analyzation) of each language. 

It is shown through these columns the word tokenizaiton process of English, Spanish, French, Russian, and Mandarin. Mandarin has the largest Word Token count out of each official language at **553748** words, Russian has the lowest at **153964** words.

This means that with a slice of 1 million characters, `SpaCy` obtained 553748 words from the Mandarin `doc` and 153964 words from the Russian `doc`. This shows that Mandarin has shorter words in character count than Russian as well as the other languages. Mandarin words are short, and variance in word length is reduced relative to that of latin languages. 

Despite shorter words, the process of [word tokenizing](https://nbviewer.org/github/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/DataProcessing.ipynb#Word-Tokenizing-Mandarin-Document) the Mandarin doc using `SpaCy` took 2 seconds in comparison to that of [French](https://nbviewer.org/github/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/DataProcessing.ipynb#Word-Tokenizing-French-Document) which took only .4 seconds. 

This can be attributed to many lingusitic differences, which then can highlight many functions in NLP. Mandarin for example does not use spaces in order to seperate words, whereas French and other languages do. This difference in lingusitic word usage can highlight why `nltk` was unable to properly process Mandarin, there was no whitespace " " between tokens in the documents, and therefore processing in langauges without spaces such as Japanese and Mandarin may present issues in time processing.



**Sentence Tokenization**

Here is a `matplot` graph showing the comparison in **sentence token length** for each langauge. 
![Sent Tokens](https://github.com/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/new_image_files/Sentence_Length.png)

In [sentence tokenization](https://nbviewer.org/github/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/DataProcessing.ipynb#Sentence-Tokenizing-Mandarin-Document) of each language it is shown that `SpaCy` tokenizes each sentence differently.

For example SpaCy sentence tokenizes the [English sentence](https://nbviewer.org/github/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/DataProcessing.ipynb#Sentence-Tokenizing-English-Document) as "Demands that all parties to the conflict immediately cease hostilities, agree to a cease-fire, and bring an end to the mindless violence and carnage engulfing Rwanda;
2."

And then tokenizes the same sentence in [French](https://nbviewer.org/github/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/DataProcessing.ipynb#Sentence-Tokenizing-French-Document) as "Exige que toutes les parties au conflit cessent immédiatement les hostilités, acceptent un cessez-le-feu et mettent fin à la violence et au carnage insensés dans lesquels est plongé le Rwanda;"

In English sentence tokenization, the semi-colon is not seen as an end of sentence boundary, which can be seen as "2." is the marked end of the sentence, however in French tokenization, the semi-colon does act as the end of the sentence. In French grammar the semi-colon can complete a sentence but never ends a text. Despite this grammatical rule, the sentence tokenization slighlty differs linguistically in English and French tokenization.

[Here](https://nbviewer.org/github/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/DataProcessing.ipynb#Sentence-Tokenizing-Mandarin-Document) is a representation of how `SpaCy` sentence tokenized the same sentence in each langauge.

Now taking a look at the [dataframe](https://nbviewer.org/github/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/DataProcessing.ipynb#Creating-DataFrame-for-Analyzation) columns **Sentence_Tokens** and **Sentence_Token_Length** we see that Mandarin has the highest sentence token length at **23363** sentences and Spanish has the lowest at **4861** sentences. This again highlights the character count limit significantly impacting the parallel lingusitic analysis of each langauge due to the fact that Mandarin, unlike Spanish, does not use whitespace characters to seperate words.


**POS Tagging**

Here is a `matplot` graph showing the comparison in **POS Count** for each langauge. 
![POS](https://github.com/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/new_image_files/POS_Count.png)

As you can see from this as well as the [dataframe](https://nbviewer.org/github/Data-Science-for-Linguists-2022/UN-Parallel-Corpora-Analysis/blob/main/DataProcessing.ipynb#Creating-DataFrame-for-Analyzation) is that Mandarin has a **POS_Count** of 553748 with a set of {'INTJ', 'SCONJ', 'DET', 'VERB', 'NOUN', 'SPACE', 'PRON', 'ADV', 'CCONJ', 'ADJ', 'X', 'PART', 'NUM', 'ADP', 'PUNCT', 'PROPN'} 

Russian has the lowest count of 153964 with a set of {'INTJ', 'SYM', 'SCONJ', 'DET', 'VERB', 'SPACE', 'NOUN', 'PRON', 'CCONJ', 'ADV', 'AUX', 'X', 'PART', 'NUM', 'ADP', 'PROPN', 'PUNCT', 'ADJ'} 

Russian has two more POS taggers in its `SpaCy` module than Mandarin, however they do vary. This shows that `SpaCy` takes into account the different POS languages can have in comparison to others. Although a cross lingusitic comparison can not be made on empiracally or statistically with this specific data it can show how different languages absolve the need for ceratin POS over others. 

For instance, `SpaCy`'s Mandarin module does not have the POS tag label "SYM," however Russian does. "SYM" means symbol = $, %, §, ©, +, −, ×, ÷, =, :), 😝

The Mandarin module also does not have "AUX" or auxillary such as is, has (done), will (do), should (do) in English, but Mandarin Chinese does use auxillary verbs such as 能 and 能够, 能夠, 会, 會, and 可以. This highlights a slight NLP difference in `SpaCy`'s modules.

**Dependency Tagging**
`SpaCy`'s Dependency Tagger was the most exciting tool to work with. Using the `displacy` tool I was able to render a dependency visualization of the same tokenized sentences above for each langauge. 


## Conclusion

Although there were many bumps in the road in moving forward with this parallel corpora analysis. I feel that I have learned valuable skills in Data Science for Linguists, the most important of those being cross-lingusitic comparison in numerical and empirical linguistic data, using different NLP modules for processing such as `nltk`, `SpaCy`, and `CAMeL`, data collection and cleaning, and finally the use of ethical data sources. This project is one of the many first steps towards Data Science success that I will be making as I progress towards a more parallell analysis in the future. 

## Sources
Ziemski, M., Junczys-Dowmunt, M., and Pouliquen, B., (2016), The United Nations Parallel Corpus, Language Resources and Evaluation (LREC’16), Portorož, Slovenia, May 2016.


