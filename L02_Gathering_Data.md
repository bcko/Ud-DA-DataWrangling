# Gathering Data

## Introduction
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

## Source: Web Scraping

### Introduction
All right. So we want to grab this audience score here to add to our data
set and number of audience reviews to match our number of critic reviews.
Unfortunately, Rotten Tomatoes hasn't made this easily accessible for us.
One way we can get these pieces of data though, web scraping.
Web scraping is a fancy way of saying extracting data from web sites using code.
It's actually one of the first magical things that drew me to programming.
Behind the scenes though, web scraping is actually quite simple.
The data that lives on web pages is called HTML, HyperText Markup Language.
It's made up of these things called tags which give the web page structure.
Because HTML code is just text,
these tags and the content within them can be accessed using parsers,
and in Python, there is an awesome one called Beautiful Soup.
We can download HTML and access it offline,
or we can do it in real time over the Internet.
For this lesson, we're going to download
the HTML files and parse them using Beautiful Soup.
Before we do though, let's explore the structure of HTML files.

- [Rotten Tomatoes: E.T. the Extra-Terrestrial (1982)](https://www.rottentomatoes.com/m/et_the_extraterrestrial)
- [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/)

### Saving HTML

The first step of web scraping is getting the web page's data,
which is stored in a format called,
HTML, HyperText Markup Language.
One way of getting the HTML is by saving it to your computer manually,
going to your web page,
then to your browser's menu,
and clicking save or hitting command or control
S. But that's not the best way to do it for data analysis.
There are two better ways,
and they're both done programmatically,
which is best for scalability and reproducibility,
which is key in this case.
Because we have 100 HTML files to access,
and multiple people, i.e.,
every student that takes this class is going to access them.
Okay, so the first is actually downloading
the HTML file programmatically to your computer.
Here's all the code you need.
You'll learn how this code works under the hood later in the lesson,
when you download files from the internet programmatically.
This is just the code to download one file.
To download all 100 files,
we just need to put this code in a loop.
The second programmatic way to access
HTML data is done by not saving a file to your computer at all,
and simply working with the response content live in your computer's memory.
You can use the BeautifulSoup HTML parser
to help you work with the response content directly.
You're going to dive into this BeautifulSoup library shortly.

The two main ways to work with HTML files are:

- Saving the HTML file to your computer (using the [Requests](http://docs.python-requests.org/en/master/) library for example) library and reading that file into a `BeautifulSoup` constructor
- Reading the HTML response content directly into a `BeautifulSoup` constructor (again using the Requests library for example)

You'll learn how this Requests code works under the hood shortly in “Downloading Files from The Internet.”

For this lesson, you’re going to do neither of these. I've downloaded all of the Rotten Tomatoes HTML files for you and put them in a folder called rt_html in the Jupyter Notebooks in the Udacity classroom. If you want to work outside of the classroom, download [this zip file](https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ca6b7b_rt-html/rt-html.zip) and extract the rt_html folder. I recommend that you do and open the HTML files in your preferred text editor (e.g. [Sublime](https://www.sublimetext.com/), which is free) to inspect the HTML for the quizzes ahead.

The rt_html folder contains the Rotten Tomatoes HTML for each of the Top 100 Movies of All Time as the list stood at the most recent update of this lesson. I'm giving you these historical files because the ratings will change over time and there will be inconsistencies with the recorded lesson videos. Also, a web page's HTML is known to change over time. Scraping code can break easily when web redesigns occur, which makes scraping brittle and not recommended for projects with longevity. So just use these HTML files provided to you and pretend like you saved them yourself with one of the methods described above.

### More Information
- [Towards Data Science: Ethics in Web Scraping](https://medium.com/towards-data-science/ethics-in-web-scraping-b96b18136f01)
- [David Venturi: Screen scraping was the first "magical" thing that drew me to programming](https://twitter.com/venturidb/status/734757220525715456)

## HTML File Structure

## HTML Files in Python
Displayed here is the E.T.
Rotten Tomatoes HTML data.
HTML files are text files that can be opened and
inspected in text editors, like Sublime here.
This means you can write your own code to parse or understand the text.
Sure, there's some confusing code at the top here,
but the actual text content of the web page,
like the title and the critic and audience scores for example, that's pretty simple.
Like to get our audience score metrics,
we could find all instances of the span tag in the text using something like Python
str.find function or a fancier tool called regular expressions,
to search for and extract patterns in text.
But, once again, people have come before us
and solved this problem in a spectacular fashion.
Beautiful Soup is a HTML parser written in the Python programming language.
The name is derived from the tag soup term,
in reference to the unstructured and almost unparsable HTML found on most web sites.
Pause the video and take a second to read
the library's rather convincing testimonials if you'd like.
So, let's use this to extract the title of the movie from our E.T.
HTML page. We'll need this later when we're joining all of out gathered pieces of data.
So we'll go to the documentation.
The first thing you need to do is make the soup.
That means passing the path to your HTML file into a file handle,
then passing that file handle into the Beautiful Soup constructor, like so.
That's after importing the Beautiful Soup library of course.
And let's try this with our Rotten Tomatoes E.T.
HTML which is stored in this rt_html folder.
So, there's our file path,
and we passed it into this file handle, file.
They have FP as file handle,
but we've been using files so, let's stick with this.
So, Beautiful Soup throws this warning which is
telling us that we didn't specify a specific parser.
Pause the video and take a second to read this if you'd like.
By default, they actually picked the most popular parser for us which is called lxml,
and we'll actually pass this in here to get rid of this warning.
And we have our Soup, our Beautiful Soup.
This looks exactly like an HTML document, but in actuality,
we can use methods in the Beautiful Soup library to
easily find and extract data from this HTML.
One of the most popular methods is the find method.
Let's find the title of our movie using this method.
Pause the video and take a second to read the first paragraph here.
It might not all make sense right away, but shortly it will.
I promise you. Okay, so let's use find to get the title of our movie from our HTML.
Think of Beautiful Soup's find method,
like the find feature in a text editor.
For example, i.e.
Control+F or Command+F.
And if we search for our title tag,
we'll find that there's only one in this whole HTML document.
And within that tag is the movie title that we want.
E.T. the Extra-Terrestrial, 1982.
And here's how that looks in Beautiful Soup code, and there it is.
This title is actually the title of the web page and
not the title of the movie which you can see up here.
To get the movie title only,
we'll have to do some simple string slicing to remove that and bit there.
The space - space rotten space tomatoes.
No worries, we can do that. Okay. So, to access the contents of this tag, i.e.
whatever's within these opening and closing tags,
we can use dot contents.
Dot contents returns a list of the tags children and there's the list.
Because there's only one thing within this tag,
the list is one item long and we can never access it using the index 0.
And here's what string slicing looks like to just get
the movie title and the year the movie was released.
This string splicing just grabbed everything from the first character in
our string to the 18th last character.
The length of the string space dash space rotten space tomatoes, being 18 characters.
So, this xa0 thing is unicode for non-breaking space.
Unicode stuff is something we'll cover shortly.
So, don't worry if it doesn't make sense to you right now.
The reason why I'm bringing this up is because
the original Top 100 TSV file actually doesn't have a non-breaking space here,
in between the end of the movie and the year of the movie release,
it just has a regular space.
So we'll have to standardize these when cleaning,
so we can later join data frames on the title column.
We actually won't do any cleaning in this lesson,
so just keep this in mind for now.

### Quiz
With your knowledge of HTML file structure, you're going to use [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/) to extract our desired Audience Score metric and number of audience ratings, along with the movie title like in the video above (so we have something to merge the datasets on later) for each HTML file, then save them in a pandas DataFrame.

The Jupyter Notebook below contains template code that:
- Creates an empty list, df_list, to which dictionaries will be appended. This list of dictionaries will eventually be converted to a pandas DataFrame (this is the [most efficient way of building a DataFrame row by row](https://stackoverflow.com/a/28058264)).
- Loops through each movie's Rotten Tomatoes HTML file in the rt_html folder.
- Opens each HTML file and passes it into a file handle called file.
- Creates a DataFrame called df by converting df_list using the [`pd.DataFrame` constructor](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html).

Your task is to extract the title, audience score, and number of audience ratings in each HTML file so each trio can be appended as a dictionary to df_list.

The Beautiful Soup methods required for this task are:
- find()
- find_all

There is an excellent tutorial on these methods ([Searching the tree](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#searching-the-tree)) in the Beautiful Soup documentation. Please consult that tutorial if you are stuck.

### Solution
So the empty list of dictionaries,
df_list, is already there for you,
as well as the for loop that loops through every file in our rt_html folder.
The first thing to do is make the soup,
which we do by passing in the file handle file,
or whatever you named your file handle.
The first thing to grab from the HTML was the title,
the movie title, which was already done previously.
Again, using the find method to get the only title tag in the document,
then accessing the contents of that file using.contents,
and grabbing the first item in that tag and slicing off that last ' - Rotten Tomatoes'.
Let's take a look here and debug a bit,
just in case something has gone wrong.
So we'll loop through this loop once,
then print out the title variable as we have it here,
then break from the loop.
This is good practice. Okay, and there's the title.
I actually forgot to specify the lxml parser,
which is actually okay, but I'll specify it anyways.
Okay, there we go, no warning.
The next thing to grab was the audience_score.
Let's take a look at our HTML code to see where that's at.
So there's that 72% and it's actually within
a div with the class titled audience-score meter.
If you look closer, you'll see that the 72% is
within the only span tag within this outermost div tag,
the outermost one being this div with,
again, the class audience-score meter.
Because it's the first span tag,
we can use the.find method,
a beautiful soup, to get the first tag of whatever tag we search using find.
But first, we'll actually have to identify the div with the class audience-score meter,
which is done like so.
Note that class has to have an underscore after it.
That's because class is a reserved key word in Python.
And we'll find this first span tag within this div and
lt's just take a break here again and look where we're at with this code.
We'll loop through this code once,
print out the audience score,
then break from the loop again. Okay, it's all looking good.
It will access the contents of this tag
using.contents and because it's the first and only item within this tag,
we'll use the 0 index, i.e.
the first item of the list returned from.contents, and we're almost there.
We actually don't want this percentage sign.
So, we'll get rid of that with some basic string slicing.
Grabbing everything in the string except the last character in it, and great.
We've got our audience score.
Now, to grab the number of audience ratings.
This one's a bit more complicated.
Let's take a peek at the HTML code once again.
If we scroll down a bit, we'll see the user ratings
here or the number of audience ratings.
This is for the E.T.
movie HTML page, but this structure applies to all of the files we downloaded.
So, it's a bit hard to see here,
but the outermost div tag is this one here with
the class audience-info hidden-xs superPageFontColor.
So let's zoom in on that using BeautifulSoup.
That's quite a bit to type out, so I'll copy and paste this here.
Again, let's use the loop and print and break strategy.
That's a bit more clear.
Here's the outermost div with the class we specified,
audience-info hidden-xs superPageFontColor,
and within that div tag is two other div tags,
and the number of audience ratings is in the second div tag.
We can use find all and take the second item in that returned list.
The second item being index number 1.
Then if we look at the contents here,
we'll see our number of audience ratings,
third item index number 2.
There's a bunch of white space here we'll strip out using the Python strip function,
and we're almost done.
This is currently in string form.
We'll later have to convert to an integer and to do that,
we'll actually have to remove these commas.
So, we'll do that using Python's replace function,
replacing commas with the empty character.
And there we go and now,
all that's left to do is convert our list of dictionaries,
df_list, to a Pandas dataframe.
First, we'll make sure that the Pandas library is imported and aliased as PD,
and we'll specify the column order,
and that should be it.
Let's process this cell.
This may take a bit of time to run.
For me, around 15 seconds or so.
And great, no errors.
Let's take a look at this dataframe.
And perfect, there we go.

```python
from bs4 import BeautifulSoup
import os
import pandas as pd

# List of dictionaries to build file by file and later convert to a DataFrame
df_list = []
folder = 'rt_html'
for movie_html in os.listdir(folder):
    with open(os.path.join(folder, movie_html)) as file:
        soup = BeautifulSoup(file, 'lxml')
        title = soup.find('title').contents[0][:-len(' - Rotten Tomatoes')]
        audience_score = soup.find('div', class_='audience-score meter').find('span').contents[0][:-1]
        num_audience_ratings = soup.find('div', class_='audience-info hidden-xs superPageFontColor')
        num_audience_ratings = num_audience_ratings.find_all('div')[1].contents[2].strip().replace(',', '')
        # Append to list of dictionaries
        df_list.append({'title': title,
                        'audience_score': int(audience_score),
                        'number_of_audience_ratings': int(num_audience_ratings)})
df = pd.DataFrame(df_list, columns = ['title', 'audience_score', 'number_of_audience_ratings'])
```

### More Information
- [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/)
- [Stack Overflow: Beautiful Soup and Unicode Problems](https://stackoverflow.com/questions/19508442/beautiful-soup-and-unicode-problems)
- [Stack Overflow: Python: Removing \xa0 from string](https://stackoverflow.com/questions/10993612/python-removing-xa0-from-string)

## Flashforward 1
So at this point, you've actually gathered
enough data to produce one of the goal visualizations,
to scatterplot with quadrants with audience score
on the horizontal axis and critics score in the vertical axis.
Since this lesson is on gathering data,
let's get past the assessing and cleaning steps of the data wrangling process,
which includes joining our two dataframes,
and let's flashforward to the final product, the visualization.
So here's what the data frame looks like with
your newly gathered audience score and number of audience ratings.
You can use matplotlib to create a simple visualization like this one,
a pretty basic scatterplot,
but this is where something interactive like Tableau really shines.
And here's what it looks like in Tableau. Pretty amazing.
So, you've got audience score on the horizontal axis ranging from 70% to 100%,
critics score in the vertical axis ranging from 91% to 100%,
well technically, 101, but that's just for visual purposes.
Then you've got these reference lines.
The vertical one being the median of audience score, which is 90%,
and the horizontal reference line is the median of critics score, 98%.
In the top right corner of the screen,
we've even got number of audience ratings and number
of critic ratings represented visually, too.
Lighter shades of blue mean small number of
audience ratings and darker shades of blue means a larger number.
And smaller circles mean a smaller number of critic ratings
and larger circles mean a larger number of critic ratings.
And okay, so in the top right corner of the screen,
we've got universally loved movies.
High audience scores, high critics scores.
One of them being The Godfather, 1972,
which if we hover over this dot,
we can see the 99% critics score and the 98% audience score.
And in the bottom right corner,
we've got critically underrated movies.
Audience scores above the median audience score for this top 100 list
and critics scores below the median critics score for this top 100 list.
One movie being The Dark Knight,
2008, audience score and critics score of 94%.
And in the top left, we have critically overrated movies.
Audiences didn't like these movies as much as critics did, basically.
Compared to the median audience and critic rating,
the most notable point, 1940's, Pinocchio.
A 100% critics score over 45 reviews but only a 72% audience score.
And then in the bottom left quadrant,
we've got movies that didn't have
particularly high critic or audience scores in reference to the movies on this list.
One notable one, Lala Land, 2016,
an audience score of 82% and a critics score of 92%,
both well below the median scores for each.
And here's E.T., right on the median critics score line,
a 98% critics score and there's that low 72% audience score.
So, this Best of Rotten Tomatoes critic versus audience score visualization
required gathering data from two different sources: Accessing files on hand,
and scraping data from web pages and that data was in two different formats,
a flat file, or a TSV file specifically,
and HTML. Great job.

-[Best of Rotten Tomatoes: Critic vs. Audience Scores (Tableau Public Viz)](https://public.tableau.com/views/BestofRottenTomatoesCriticvs_AudienceScores/BestofRottenTomatoesCriticvs_AudienceScores?:embed=y&:display_count=yes)

## Source: Downloading Files from the Internet
Okay, so now we can start the Roger Ebert review word cloud.
So the first thing you need,
the text from each of his reviews,
for each of the movies on the Rotten Tomatoes Top 100 Movies of All Time list.
They live on his website.
Lucky for you I've pre-gathered all of this text in the form of 100.txt files.
I put them on this Udacity hosted web page
and you're going to download them all programmatically.
Yes, you can point and click and download each file manually but that would take forever,
especially if someone else wants to reproduce your analysis.
If they want to check your work, for example,
they can download all of the files with the execution of a few lines of code.
So downloading files from Internet programmatically
is best for scalability and reproducibility.
In practice you really only need to know one thing
to download files like this, Python's request library.
Knowing a bit of HTTP aka
Hypertext Transfer Protocol will help you understand what's going on under the hood here.
So next you'll learn the basics of HTTP along with Python's request library.

### HTTP (Hypertext Transfer Protocol)
HTTP, the Hypertext Transfer Protocol, is the language that web browsers (like Chrome or Safari) and web servers (basically computers where the contents of a website are stored) speak to each other. Every time you open a web page, or download a file, or watch a video, it's HTTP that makes it possible.

HTTP is a request/response protocol:

- Your computer, a.k.a. the client, sends a request to a server for some file. For this lesson: "Get me the file 1-the-wizard-of-oz-1939-film.txt", for example. GET is the name of the HTTP request method (of which there are multiple) used for retrieving data.
- The web server sends back a response. If the request is valid: "Here is the file you asked for:", then followed by the contents of the 1-the-wizard-of-oz-1939-film.txt file itself.

![clinet_server](https://developer.mozilla.org/files/4291/client-server.png)

If you'd like to learn more, or are feeling like there are knowledge gaps you'd like to fill in, I encourage you to check out the following videos in our free [Web Development course](https://www.udacity.com/course/web-development--cs253): concepts 2-5 and 24-30 in Lesson 1 ("How the Web Works").

### Requests: HTTP for Humans
Python for Quest library makes HTTP requests easy.
It has a method called get which will send the request for us,
return the contents of the file we requested, which for us,
is a text file, which we can then save to a file.
This is how we programmatically download a file from the Internet.
Here's how it's done. It's super simple.
We import the request library,
and we'll actually import the OS library,
too, so we can store the downloaded file in a folder called ebert_reviews.
This bit of code here just creates the folder ebert_reviews if it doesn't exist already.
Here comes the actual bit of request code.
We use requests.get on a URL,
and that returns a response.
And I'll give you this you this URL here.
Here is the URL for the Roger Ebert reviews
text file that I saved on new Udacity's servers.
So we haven't actually saved the response to anything yet,
but let's take a look at what this response variable looks like.
And we see response 200.
200 being the HTTP status code for the request has succeeded.
So that's good. So this response returned from the requests.get method.
You can't see it currently,
but all the text in our text file is actually in
our computer's working memory right now within this response variable.
It's stored in the body of the response which we can access using.content,
as shown in the request library documentation. Let's check it out.
And okay, there it all is.
It's in bytes format.
Using this and some basic file IO,
we're going to save this file to our computer.
So we'll open a file called 11-e.t-the-extra-terrestrial.txt, i.e.
everything after the last slash in this URL.
And to get everything after that last slash,
we'll use Python's split function,
and select the last item in the list returned.
And we need to open this file which
will then write the contents of the response variable to.
We have to open this in WB mode, Write Binary.
That's because response.content is in bytes and not text. But don't worry.
When we open these files in a text editor or in Pandas later,
the bytes will be rendered as human readable text.
Then we write to the file handle we've opened, file.write response.
content. And that should do it.
That's how you download one file programmatically.
Let's check the contents of our folder ebert_reviews
to make sure this worked. And there it is.
This.DS_Store is a hidden file that
stores the attributes of our folder. Ignore that for now.
And if you go to your Jupyter Notebook dashboard,
and open that file,
you'll see that the entirety of it was correctly downloaded.
So again, that's how you download one file.
But if we have lots of files to download though,
like we do for all of these Ebert reviews for the top 100 Rotten Tomatoes movie list,
writing a lot of these statements would be annoying.
Luckily, downloading files programmatically scales well.
You can use a for loop over all of the file URLs to minimize code repetition.
Lucky for you, I've provided the URLs for you here.
Your task now is to write this loop,
and download all of the Roger Ebert review files programmatically.

### Quiz
In the Jupyter Notebook below, programmatically download all of the Rogert Ebert review text files to a folder called ebert_reviews using the Requests library. Use a for loop in conjunction with the provided ebert_review_urls list.

Here is the [Requests documentation](http://docs.python-requests.org/en/master/) for easy reference. It is excellently clear relative to similar libraries, like [urllib](https://docs.python.org/3/howto/urllib2.html).


### Solution
```python
import requests
import os

folder_name = 'ebert_reviews'
if not os.path.exists(folder_name):
    os.makedirs(folder_name)
    
ebert_review_urls = ['https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9900_1-the-wizard-of-oz-1939-film/1-the-wizard-of-oz-1939-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9901_2-citizen-kane/2-citizen-kane.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9901_3-the-third-man/3-the-third-man.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9902_4-get-out-film/4-get-out-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9902_5-mad-max-fury-road/5-mad-max-fury-road.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9902_6-the-cabinet-of-dr.-caligari/6-the-cabinet-of-dr.-caligari.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9903_7-all-about-eve/7-all-about-eve.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9903_8-inside-out-2015-film/8-inside-out-2015-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9903_9-the-godfather/9-the-godfather.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9904_10-metropolis-1927-film/10-metropolis-1927-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9904_11-e.t.-the-extra-terrestrial/11-e.t.-the-extra-terrestrial.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9904_12-modern-times-film/12-modern-times-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9904_14-singin-in-the-rain/14-singin-in-the-rain.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9905_15-boyhood-film/15-boyhood-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9905_16-casablanca-film/16-casablanca-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9905_17-moonlight-2016-film/17-moonlight-2016-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9906_18-psycho-1960-film/18-psycho-1960-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9906_19-laura-1944-film/19-laura-1944-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9906_20-nosferatu/20-nosferatu.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9907_21-snow-white-and-the-seven-dwarfs-1937-film/21-snow-white-and-the-seven-dwarfs-1937-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9907_22-a-hard-day27s-night-film/22-a-hard-day27s-night-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9907_23-la-grande-illusion/23-la-grande-illusion.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9908_25-the-battle-of-algiers/25-the-battle-of-algiers.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9908_26-dunkirk-2017-film/26-dunkirk-2017-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9908_27-the-maltese-falcon-1941-film/27-the-maltese-falcon-1941-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9909_29-12-years-a-slave-film/29-12-years-a-slave-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9909_30-gravity-2013-film/30-gravity-2013-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9909_31-sunset-boulevard-film/31-sunset-boulevard-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990a_32-king-kong-1933-film/32-king-kong-1933-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990a_33-spotlight-film/33-spotlight-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990a_34-the-adventures-of-robin-hood/34-the-adventures-of-robin-hood.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990b_35-rashomon/35-rashomon.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990b_36-rear-window/36-rear-window.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990b_37-selma-film/37-selma-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990c_38-taxi-driver/38-taxi-driver.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990c_39-toy-story-3/39-toy-story-3.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990c_40-argo-2012-film/40-argo-2012-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990d_41-toy-story-2/41-toy-story-2.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990d_42-the-big-sick/42-the-big-sick.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990d_43-bride-of-frankenstein/43-bride-of-frankenstein.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990d_44-zootopia/44-zootopia.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990e_45-m-1931-film/45-m-1931-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990e_46-wonder-woman-2017-film/46-wonder-woman-2017-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990e_48-alien-film/48-alien-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990f_49-bicycle-thieves/49-bicycle-thieves.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990f_50-seven-samurai/50-seven-samurai.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad990f_51-the-treasure-of-the-sierra-madre-film/51-the-treasure-of-the-sierra-madre-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9910_52-up-2009-film/52-up-2009-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9910_53-12-angry-men-1957-film/53-12-angry-men-1957-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9910_54-the-400-blows/54-the-400-blows.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9911_55-logan-film/55-logan-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9911_57-army-of-shadows/57-army-of-shadows.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9912_58-arrival-film/58-arrival-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9912_59-baby-driver/59-baby-driver.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9913_60-a-streetcar-named-desire-1951-film/60-a-streetcar-named-desire-1951-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9913_61-the-night-of-the-hunter-film/61-the-night-of-the-hunter-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9913_62-star-wars-the-force-awakens/62-star-wars-the-force-awakens.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9913_63-manchester-by-the-sea-film/63-manchester-by-the-sea-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9914_64-dr.-strangelove/64-dr.-strangelove.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9914_66-vertigo-film/66-vertigo-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9914_67-the-dark-knight-film/67-the-dark-knight-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9915_68-touch-of-evil/68-touch-of-evil.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9915_69-the-babadook/69-the-babadook.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9915_72-rosemary27s-baby-film/72-rosemary27s-baby-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9916_73-finding-nemo/73-finding-nemo.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9916_74-brooklyn-film/74-brooklyn-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9917_75-the-wrestler-2008-film/75-the-wrestler-2008-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9917_77-l.a.-confidential-film/77-l.a.-confidential-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9918_78-gone-with-the-wind-film/78-gone-with-the-wind-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9918_79-the-good-the-bad-and-the-ugly/79-the-good-the-bad-and-the-ugly.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9918_80-skyfall/80-skyfall.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9919_82-tokyo-story/82-tokyo-story.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9919_83-hell-or-high-water-film/83-hell-or-high-water-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9919_84-pinocchio-1940-film/84-pinocchio-1940-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad9919_85-the-jungle-book-2016-film/85-the-jungle-book-2016-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad991a_86-la-la-land-film/86-la-la-land-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad991b_87-star-trek-film/87-star-trek-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad991b_89-apocalypse-now/89-apocalypse-now.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad991c_90-on-the-waterfront/90-on-the-waterfront.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad991c_91-the-wages-of-fear/91-the-wages-of-fear.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad991c_92-the-last-picture-show/92-the-last-picture-show.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad991d_93-harry-potter-and-the-deathly-hallows-part-2/93-harry-potter-and-the-deathly-hallows-part-2.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad991d_94-the-grapes-of-wrath-film/94-the-grapes-of-wrath-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad991d_96-man-on-wire/96-man-on-wire.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad991e_97-jaws-film/97-jaws-film.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad991e_98-toy-story/98-toy-story.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad991e_99-the-godfather-part-ii/99-the-godfather-part-ii.txt',
                     'https://d17h27t6h515a5.cloudfront.net/topher/2017/September/59ad991e_100-battleship-potemkin/100-battleship-potemkin.txt']
                     
folder_name = 'ebert_reviews'
if not os.path.exists(folder_name):
  os.makedirs(folder_name)

for url in ebert_review_urls:
  response = requests.get(url)
  with open(os.path.join(folder_name, url.split('/')[-1]), mode = 'wb') as file:
    file.write(response.content)
```
Given this Ebert review URL's list,
the first thing to do is loop through it.
Then, we'll get the HTTP response via request.get.
On whatever URL, we are currently on the iteration of that loop.
Then, the bit of code to open a file and write the
response.content to that file is the same.
And that's it, we'll process the cell and this may take a bit of time to do,
downloading these files takes some time.
It took my computer roughly five seconds and let's check the contents of this folder.
And the're all of the text files.
There should be 88, and there are.
12 movies in the top 100 Rotten Tomatoes list didn't have reviews on Roger Ebert's site.

### More Information
- A text file is downloaded in this example. Binary files (images, for example) are best read and wrote to [other ways](http://docs.python-requests.org/en/latest/user/quickstart/#binary-response-content).
- [Stack Overflow: What is the 'wb' mean in this code, using Python](https://stackoverflow.com/questions/2665866/what-is-the-wb-mean-in-this-code-using-python)?
