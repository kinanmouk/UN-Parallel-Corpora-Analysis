
# Progress Report
### February 14th 2022
- Github repository created
- Markdown files commited to repository 
     -  [`README.md`](README.MD)
     -  [`LICENSE.md`](LICENSE.md)
     -  [`project_plan.md`](project_plan.md)
     -  [`progress_report.md`](progress_report.md)
     -  [`.gitignore`](.gitignore)
   
### February 28th 2022
- Created [`UN_Data_Analysis.ipynb`](UN_Data_Analysis.ipynb)
     -   Data is Analyzed however files are too large to anaylze on my computer safely at this time
     - I sliced each file to the first [:10000000] so that I can work with it safely and without Juypter Notebook crashing
     - UN website says the files are XML however they are not. They are plain text I am still looking for ways to seperate each UN file within each Langauge File
     - This gve me a lot of trouble, I do not know how to safely analyze the data. It keeps saying kernel has appeared to of died and then restarts however due to timing you can see that this makes it really hard to work with the data. 
     - I am also not really sure how to save the segemented data to my computer so that I can upload it. Need to go to office hours.

# 2nd Progress Report
## "Found" Portion of Data

### March 16th 2022

- Updated [`UN_Data_Analysis.ipynb`](UN_Data_Analysis.ipynb) (EXISTING)

     - Since the files took to long to upload into juypter and my personal laptop was unable to compute the size of the decompressed UN archive files I created smaller portions of data for each language in command line. Each langauge file now has 100k characters so that I can analyze the data safely without my computer crashing. I created subheadings for each langauge and uploaded all analyzed data into a pandas dataframe both for presentation and for easy access.
     - There is do data/ section for me because my data files are too large. [`data_samples/`](data_samples/) should suffice.
     
### March 21st 2022
- Files Created 
     - [`data_samples/`](data_samples/)
     - [`image_files/`](image_files/)
     - 
- Files Updated
     -   [`README.md`](README.MD)
     -   [`LICENSE.md`](LICENSE.md) using [`UNv1.0.pdf`](UNv1.0.pdf) and MIT

# 3rd Progress Report
### April 8th 2022
- Files Created 
     - [`SpaCyNLP.ipynb`](SpaCyNLP.ipynb) (NEW REPLACEMENT)
         
         Okay so this file now has a lot of new NLP using [`SpaCy`](https://spacy.io/) which is a linguistics tool that parses langauges and processes them best based off of the strucure of the language. It is better than using NLTK bc it truly represents each langauge accurately because NLTK is mostly English focused. My data portion of this project is not completed however at this stage I believe that this is okay due to the fact that Arabic is difficult to process and [`SpaCy`](https://spacy.io/) presents many processing issues. I need help with figuring out what my next steps are in this process.
         There are a few problem as of right now:
        -   There is no SpaCy module to process Arabic.
         -  Arabic is a very difficult langauge to parse.
        -   [`SpaCy`](https://spacy.io/) only processes a small amount of text, meaning I might have to process in chunks in order to do this with a huge portion of data.
         -  I might have to use the [`Pitt CRC`](https://crc.pitt.edu/) in order to process these files.
     
- Files Updated
     -  [`README.md`](README.MD)
     -  [`LICENSE.md`](LICENSE.md)
     -  [`project_plan.md`](project_plan.md)
     -  [`UN_Data_Analysis.ipynb`](UN_Data_Analysis.ipynb) (EXISTING)
     -  [`.gitignore`](.gitignore)
