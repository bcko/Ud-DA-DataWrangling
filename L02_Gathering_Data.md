# Gathering Data

## Introduction
ou've reached lesson two of our data wrangling course.
In lesson one, we walk through the whole wrangling process from gathering,
to assessing, to cleaning data,
and iterating if necessary.
In the next three lessons, you're going to dive deeper into each step of the process.
First, you're going to master gathering data.
Depending on your project,
gathering data varies a lot.
Data you need may be spread across dozens of sources and in different file formats,
which might be the most challenging part of working with data.
Not analyzing, not visualizing,
not even building fancy machine-learning models, simply gathering.
It's also glossed over in most data wrangling courses where
complete datasets are just provided for you. Not here.
In this lesson, you'll gather real data from several different sources and
file formats while learning about each and how to handle them using Python.
You'll combine them all to create a master dataset which we'll then use
to answer interesting questions and produce stunning visualizations.
You're going to leave this lesson with the gathering skills required
for the vast majority of your wrangling projects in the future.
So let's do this. This is going to be fun,
challenging, and is going to require a bit of creativity.

## Lesson Outline
Gathering data is the first step in data wrangling. Before gathering, we have no data, and after it, we do.

Gathering data varies from project to project. Sometimes you're just given data, or pointed to it like I do for you throughout this course. Sometimes you need to search for the right data for your project. Sometimes the data you need isn't readily available, and you need to generate it yourself somehow. When you do find your data, it's not unusual for it to be spread across several different sources and file formats, which makes things tricky when organizing the data in your programming environment.

For these reasons and more, gathering can be tricky. In this lesson, which is likely the most technically challenging lesson of the course, you'll acquire the coding skills and general craftiness required to conquer the vast majority of gathering scenarios you'll come across in the future. This is going to be hard sometimes, and that's okay. Stick with it and don't hesitate to reach out for help.

This lesson will be structured as follows:

- First, we'll pose a few questions.
- Then you'll explore the source of each piece of data we need to answer those questions, each piece from a different source - and in a different format.
- Then you'll learn about the structure of each file format.
- Then you'll learn how to handle that file format using Python and its libraries.
- Then you'll actually gather each piece of data to later join together to create your master dataset.

## Dataset: Finding the Best Movies
t's Sunday night. You just had a nice meal,
maybe some dessert, and you're on the couch with
some popcorn and you want to watch a movie.
How do you pick what to watch?
Being a data driven person,
I love to check the ratings and reviews on Rotten Tomatoes,
which is a popular movie rating website.
This list they have here is so useful.
The Rotten Tomatoes top 100 movies of all time list.
As written here, movies with 40 or more critic reviews are eligible for this list.
That's critic reviews, so ratings from
regular movie watchers like you and me aren't included in these calculations.
It's sorted by this adjusted score metric which combines
the rating and number of critic reviews for each movie to create this adjusted score.
The idea being that movies with fewer critic ratings have
an easier path to getting that 100% score or close to it.
Let's scroll a bit here.
Okay, so E.T., I've never actually seen
Steven Spielberg's 1982 masterpiece despite hearing lots about it.
It's currently 11th on this list with a 98% rating and 114 critic reviews.
Let's check it out. Okay, so there's that 98% rating.
This number is a bit deceiving though.
It's actually the Tomatometer score,
which is the percentage of
approved Tomatometer critics who have given the movie a positive review.
But okay, there's this audience score here, 72%.
That metric wasn't included in that top 100 list.
That's a pretty massive gap.
Maybe this movie isn't that amazing.
Also, wouldn't it be cool to compare this critic's score and also the audience score
for all of these movies to see which movie really truly is the best?
Also to find the worst best movie if you will.
I'm picturing a scatterplot with four quadrants,
like this one, but with different axis labels and values.
We'd have audience score on the horizontal axis and critics score on the vertical one.
That would put amazing movies with
high audience and critics scores in the top right quadrant
then critically underrated movies in the bottom
right quadrant with high audience scores and low critics scores,
and critically overrated movies in the top
left with low audience scores and high critics scores.
Also, I don't trust every single reviewer necessarily.
One person I do though,
the late great Roger Ebert.
For lots of people,
Roger Ebert's was the only review they needed because he explained the movie in
such a way that they would know whether they would
like it or not, his opinion notwithstanding.
Wouldn't it be neat if we had a word cloud for each of the movies in
that top 100 list with Roger Ebert's review text in that word cloud for each movie?
This cool little word cloud generator in Python can help us out.
Having a word cloud for each movie would give us
a snapshot of what makes each movie great.
This word cloud library also has the ability to use stencils,
so we could take the movie poster for each movie and surround it with
a stencil and then put the word cloud around the poster image.
That'd be really cool. So, to create both of these visualizations,
the data is in a few different spots and
it will require some craftiness to gather it all,
but you can definitely do it.
This is actually going to be so awesome.
I'm so excited for you to see the final products.

- [Rotten Tomatoes: Top 100 Movies of All Time](https://www.rottentomatoes.com/top/bestofrt/)
- [RogerEbert.com](http://www.rogerebert.com/)
- [Andreas Mueller: Word Cloud Generator in Python](https://amueller.github.io/word_cloud/)

## Navigating Your Working Directory and File I/O
Before you continue on with this lesson, make sure you are comfortable working with your computer's command line interface to access files and folders, and also with reading and writing to files (i.e. part of File I/O or input/output) in Python. It can be extremely frustrating getting bogged down in these seemingly trivial topics.

### Command Line
For the command line interface, here are three excellent resources that I recommend. Pick whichever suits you best:
- Our short [Linux Command Line Basics](https://www.udacity.com/course/linux-command-line-basics--ud595) course (for Linux and Mac users)
- [Navigating the Terminal: A Gentle Introduction](https://computers.tutsplus.com/tutorials/navigating-the-terminal-a-gentle-introduction--mac-3855) by Marius Masalar (for Mac users)
- [Command Prompt - How to use the simple, basic commands](http://www.digitalcitizen.life/command-prompt-how-use-basic-commands) by Codrut Neagu (for Windows users)

### File I/O
For reading from and writing to files in Python:
- The "Reading from a File" concept in Lesson 5 ("Files and Modules") of our [Introduction to Python](https://www.udacity.com/course/introduction-to-python--ud1110) course


## Source: Files on Hand
So the inspiration for our little project here,
was this Rotten Tomatoes top 100 movies of all time list. How do we get it.
Rotten Tomatoes doesn't give us a file to download unfortunately.
For this lesson, I'm just going to give it to you.
Gathering can be complicated,
but it can also be extremely easy.
Sometimes you are simply just given a file.
I've pre-gathered this dataset with its four columns; rank, title, rating,
and number of reviews, and it's 101 rows,
one for the headers and one for each of the top 100 movies.
I put the data in a flat file called a TSV file which stands for tab separated values.
There's a link for you to download it in the classroom.
Picture this as me e-mailing this file to you,
or giving it to you on a thumb drive,
or you accessing the file from your company's file storage system.
So point and click and download it, and we'll move on.
We don't need to do it programmatically in this case,
because we'll assume that this data is internal,
and can't be downloaded from the Internet.
You're going to learn about the structure of flat files next.

- [Rotten Tomatoes Top 100 Movies of All Time TSV File](https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ca594d_bestofrt/bestofrt.tsv) (Note: this file will be provided in a Jupyter Notebook workspace so you only need to download this file if you want outside of the Udacity classroom)
- Note: Internal data from a database can be downloaded programmatically from the file storage systems (like Google Drive) for some companies, though it is often trickier than downloading a file hosted on a web page. In practice, internal files aren't often downloaded programmatically for wrangling and analysis/visualization/modeling.

## Flat File Structure
lat files contain tabular data in plain text format with one data record per line and each record or line having one or more fields. These fields are separated by delimiters, like commas, tabs, or colons.

### Advantages of flat files include:
- They're text files and therefore human readable.
- Lightweight.
- Simple to understand.
- Software that can read/write text files is ubiquitous, like text editors.
- Great for small datasets.

### Disadvantages of flat files, in comparison to relational databases, for example, include:
- Lack of standards.
- Data redundancy.
- Sharing data can be cumbersome.
- Not great for large datasets (see "When does small become large?" in the Cornell link in More Information).

### More Information
- [Professor Excel: XML & ZIP: Explore Your Excel Workbooks File Structure](http://professor-excel.com/xml-zip-excel-file-structure/)
- [Cornell: Relational Databases - Not your Father's Flat Files](https://www.cac.cornell.edu/education/Training/DataAnalysis/RelationalDatabases.pdf)

## Flat Files in Python
Since flat files are human readable,
you can easily write your own code to parse or understand these files using Base Python.
Open the file, read the text line by line,
separate each line's content by the delimiter,
and store everything in your data structure of choice.
But people have come for us and solved this problem
and created libraries with a ton of additional functionalities,
especially for data wrangling, analysis, and visualization.
A library like pandas, for example.
Pandas can handle pretty much every file type imaginable,
and is especially well-suited for tabular data.
The code to read comma separated data into a data frame is super simple.
We use the read_csv function.
And there's our pandas data frame for the best of our t.CSV file.
But the file we wanted to use is actually a TSV file, bestofrt.TSV.
That's tab-separated, and that's okay.
Since there's no clear standard for flat files,
pandas has one main function for parsing them,
and it is read_csv.
Read_csv can handle all kinds of flat files, including TSV files.
You just need to change the parameters to fit your specific use case,
like changing the separator parameter set, for example.
Or whether or not entries are quoted and more.

### Quiz
In the Jupyter Notebook below, import the Rotten Tomatoes Top 100 Movies of All Time TSV file ('bestofrt.tsv') into a pandas DataFrame. Hint: read up on the sep parameter in the read_csv documentation.

```python
import pandas as pd
df = pd.read_csv('bestofrt.tsv', sep='\t')
```
Reading a tab separated values file into a Panda's data frame is
very similar to reading a CSV or a Comma Separated Values file.
We still use read_csv,
then put in the path to our file, which is bestofrt.tsv,
then the only difference is including the set parameter,
which we want to be a tab, which is \t.
It will process the cell and display our data frame.
And there it is.

- [pandas: Flat File Functions](https://pandas.pydata.org/pandas-docs/stable/api.html#flat-file)
