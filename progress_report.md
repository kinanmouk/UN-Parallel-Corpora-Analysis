
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

- Updated [`README.md`](README.MD)

- Updated [`LICENSE.md`](LICENSE.md) using [`UNv1.0.pdf`](UNv1.0.pdf) and MIT

 - Went with MIT because it does not overlap with U.N. Licensing requirements however I may change my mind.

- Created [`data_samples/`](data_samples/)

- Created [`image_files/`](image_files/)

## Decision on Licensin
### March 21st 2022


# 3rd Progress Report
### April 8th 2022
- Files Created 
     - [`SpaCyNLP.ipynb`](SpaCyNLP.ipynb)
     
- Files Updated
     -  [`README.md`](README.MD)
     -  [`LICENSE.md`](LICENSE.md)
     -  [`project_plan.md`](project_plan.md)
     -  [`UN_Data_Analysis.ipynb`](UN_Data_Analysis.ipynb) (EXISTING)
     -  [`UN_Data_Analysis.ipynb`](UN_Data_Analysis.ipynb) (EXISTING)
     -  [`.gitignore`](.gitignore)
