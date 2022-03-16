
# Progress Report
### February 14th 2022
- Github repository created
- Markdown files commited to repository 
     -  README.md
     -  LICENSE.md
     -  project_plan.md
     -  progress_report.md
     -  .gitignore
### February 28th 2022
- Data is Analyzed however files are too large to anaylze on my computer safely at this time
- I sliced each file to the first [:10000000] so that I can work with it safely and without Juypter Notebook crashing
- UN website says the files are XML however they are not. They are plain text I am still looking for ways to seperate each UN file within each Langauge File
- This gve me a lot of trouble, I do not know how to safely analyze the data. It keeps saying kernel has appeared to of died and then restarts however due to timing you can see that this makes it really hard to work with the data. 
- I am also not really sure how to save the segemented data to my computer so that I can upload it. Need to go to office hours.
### March 16th 2022

- Updated [`UN_Data_Analysis.ipynb`](UN_Data_Analysis.ipynb)

     - Since the files took to long to upload into juypter and my personal laptop was unable to compute the size of the decompressed UN archive files I created smaller portions of data for each language in command line. Each langauge file now has 100k characters so that I can analyze the data safely without my computer crashing. I created subheadings for each langauge and uploaded all analyzed data into a pandas dataframe both for presentation and for easy access.

- Updated [`README.md`](README.MD)

- Updated [`LICENSE.md`](LICENSE.md) using [`UNv1.0.pdf`](UNv1.0.pdf)

- Created [`data_samples/`](data_samples/)

- Created [`image_files/`](image_files/)
-
