PyClub 
*******
A work-time meetup about Python and data science at MRCagney.


Introduction
=============
- Motivation: Upskill on Python for data science. Python is useful, data science is useful, and the two together are a powerful combination.
- Focus on: Tools and processes for analyzing transit and geospatial data, because that's our main work at MRCagney
- Third-party Python libraries that we will use a lot:
    * NumPy for numerical computing. 
    * Pandas for tabular data
    * Shapely and Fiona for geospatial data
    * Geopandas, which combines Shapely with Pandas
    * GTFSTK for GTFS feeds
- Other notable third-party Python libraries for data science:
    * SciPy for scientific/engineering computing
    * Matplotlib and Seaborn for plotting and (static) visualization.
    * Statsmodels for statistical modeling
    * Scikit-Learn for machine learning
    * Requests for API calls
    * Scrapy for web crawling and scraping


Exercises
===========
1. (due 2016-11-01) On you computer, install Python 3.5, a virtual environment manager, and a Python package manager. I recommend doing this by installing `Anaconda <https://www.continuum.io/downloads#windows>`_, which is a straight-forward and cross-platform solution. `Here <https://www.reddit.com/r/Python/comments/3t23vv/what_advantages_are_there_of_using_anaconda/>`_ is some Reddit cheer for Anaconda. Alternatively, on OS X, you can use `Homebrew <http://brew.sh/>`_ to install Python 3.5, virtualenv, virtualenvwrapper, and pip. On Linux, you can use apt to install these.

2. (due 2016-11-01) Create a directory and virtual environment for your PyClub work. In the virtual environment install the `Jupyter Notebook <https://jupyter.org/>`_. Open a Jupyter notebook.

3. (due 2016-11-01) In a Jupyter notebook, write some Python code to solve the following problem, which i took from the Think Python book by Allen B. Downey. "Give me a word with three consecutive double letters. I’ll give you a couple of words that almost qualify, but don’t. For example, the word committee, c-o-m-m-i-t-t-e-e. It would be great except for the ‘i’ that sneaks in there. Or Mississippi: M-i-s-s-i-s-s-i-p-p-i. If you could take out those i’s it would work. But there is a word that has three consecutive pairs of letters and to the best of my knowledge this may be the only word. Of course there are probably 500 more but I can only think of one. What is the word?" `Here <http://greenteapress.com/thinkpython2/code/words.txt>`_ is a sufficient list of English words for you.