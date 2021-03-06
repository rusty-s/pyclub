PyClub 
*******
This is a repository of supporting material for PyClub, a work-time meetup about Python and data science at MRCagney.


Introduction
=============
- Motivation: Upskill on Python for data science. Python is useful, data science is useful, and the two together are a powerful combination.

- Focus: Tools and processes for analyzing transit and geospatial data, because that's our main work at MRCagney

- Assumption: You have Python proficiency at the level of, say, the `Codeacademy Python 2 tutorial <https://www.codecademy.com/learn/python>`_. We will be using Python 3, but they're not too different.

- Third-party Python libraries that we will use a lot:

  * NumPy for numerical computing
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


Homework 1
===========
Theme: Set up and warm up

1. On your computer, install Python 3.5, a virtual environment manager, and a Python package manager. You can do all this at once in a straightforward and cross-platform way by installing `Anaconda <https://www.continuum.io/downloads#windows>`_. Here is some `Reddit cheer for Anaconda <https://www.reddit.com/r/Python/comments/3t23vv/what_advantages_are_there_of_using_anaconda/>`_.  Alternatively on OS X, you can use Homebrew to install Python 3.5, virtualenv, virtualenvwrapper, and pip. Alternatively on Linux, you can use apt to install these.

  Update: I hear that using the current Anaconda for Windows and Python 3.4 one can install more of the third-party libraries above than Anaconda for Windows and Python 3.5. In that case, use Python 3.4. It will do for our purposes.

2. Create a directory and virtual environment for your PyClub work. In the virtual environment install the `Jupyter Notebook <https://jupyter.org/>`_. Open a Jupyter notebook.

3. In a Jupyter notebook, write some Python code to solve the following problem, which i took from *Think Python* by Allen B. Downey. "Give me a word with three consecutive double letters. I’ll give you a couple of words that almost qualify, but don’t. For example, the word committee, c-o-m-m-i-t-t-e-e. It would be great except for the ‘i’ that sneaks in there. Or Mississippi: M-i-s-s-i-s-s-i-p-p-i. If you could take out those i’s it would work. But there is a word that has three consecutive pairs of letters and to the best of my knowledge this may be the only word. Of course there are probably 500 more but I can only think of one." Here is a `sufficient wordlist <http://greenteapress.com/thinkpython2/code/words.txt>`_.

4. In a Jupyter notebook, solve the following problem, which i took from *Think Python* by Allen B. Downey. Write a program that reads a list of words and returns a collection of all lists of words that are anagrams of each other, where the collection is sorted from the longest list of anagrams to the shortest list and where the shortest list is of size at least 2.

  Here is an example of what some of the output might look like::

      [
      ['deltas', 'desalt', 'lasted', 'salted', 'slated', 'staled'],
      ['resmelts', 'smelters', 'termless'],
      ['retainers', 'ternaries'],
      ['generating', 'greatening'],
      ]

  Use your function to find all the anagrams in the word list given in problem 3 above. 
  Hint: you might want to build a dictionary that maps a collection of letters to a list of words that can be spelled with those letters.


Homework 2
===========
Theme: Pandas and GTFS

1. In your PyClub virtual environment install `Pandas <http://pandas.pydata.org/>`_. Complete the Pandas tutorial `here <synesthesiam.com/posts/an-introduction-to-pandas.html>`_, ignoring the first installation step, which you already did. The tutorial uses an older version of Pandas than yours, so some function APIs might have changed. If you encounter errors, check the `Pandas documentation <http://pandas.pydata.org/pandas-docs/stable/>`_ for the current correct usage.

2. Read the `Wikipedia page on GTFS <https://en.wikipedia.org/wiki/GTFS>`_, and for more information see the `GTFS reference <https://developers.google.com/transit/gtfs/>`_. 

3. Download a cleaned version of Auckland's latest GTFS feed from ``data/homework_02``. Working in a Jupyter notebook, complete the following function and test it.

  .. code-block:: python

      def read_gtfs(path):
          """
          Given a path (string or pathlib object) to a (zipped) GTFS feed,
          unzip the feed and save the files to a dictionary whose keys are
          named after GTFS tables ('stops', 'routes', etc.) and whose
          corresponding values are Pandas data frames representing the tables.
          Return the resulting dictionary.

          NOTES:
              - Ignore files that are not valid GTFS; see https://developers.google.com/transit/gtfs/reference/.
              - Ensure that all ID fields that could be strings ('stop_id', 'route_id', etc.) are parsed as strings and not as numbers.    
          """
          pass

  Hint: Use the functions ``shutil.unpack_archive`` and ``pandas.read_csv`` with the 'dtypes' keyword argument.

4. Using the Auckland GTFS feed and the output of your ``read_gtfs`` function, find the bus route with the longest trip and the length of that trip and find the route with the shortest trip and the length of that trip. By the way, the distances in the Auckland feed are measured in kilometers. 


Homework 3
===========
Theme: Shapely, GeoJSON, and GTFS

1. In your PyClub virtual environment install Shapely. Then read the 'Introduction' section of the `Shapely user manual  <http://toblerity.org/shapely/manual.html>`_. 

2. Recall your GTFS reader from Homework 2.3, and let us call the output of it a *GTFS feed object*. Implement the following function that converts GTFS shapes to Shapely LineString objects.

  .. code-block:: python

      def build_geometry_by_shape(feed, shape_ids=None):
          """
          Given a GTFS feed object, return a dictionary with structure 
          shape ID -> Shapely LineString representation of shape,
          where the dictionary ranges over all shapes in the feed.
          Use WGS84 longitude-latitude coordinates, the native coordinate system of GTFS.

          If a list of shape IDs ``shape_ids`` is given, 
          then only include the given shape IDs in the dictionary.
          
          NOTES:
              - Raise a ValueError if the feed has no shapes
          """
          pass

3. Read the `Wikipedia page on GeoJSON <https://en.wikipedia.org/wiki/GeoJSON>`_. Read also the 'Interoperation' section of the Shapely user manual, and notice that Shapely plays nicely with GeoJSON via the functions  ``shapely.geometry.mapping` and ``shapely.geometry.shape``.

4. Implement the following function that converts GTFS trips to GeoJSON features (as Python dictionaries).

  .. code-block:: python

      def trip_to_geojson(feed, trip_id):
          """
          Given a GTFS feed object and a trip ID from that feed, 
          return a GeoJSON LineString feature (as a Python dictionary) 
          representing the trip's geometry and its metadata 
          (trip ID, direction ID, headsign, etc.).
          Use WGS84 coordinates, the native coordinate system of GTFS.

          NOTES:
              Raise a ``ValueError`` if the appropriate GTFS data does not exist.
          """
          pass

  Hint: Use the function ``shapely.geometry.mapping`` to quickly convert a Shapely geometry into a GeoJSON geometry. Also, replace ``numpy.nan`` data values with a string such as ``'n/a'`` to avoid hassles when dumping to JSON.

  As a way to test your function's output, convert it to a JSON string via Python's built in ``json.dumps`` function, and then paste that feature collection into `geojson.io <http://geojson.io>`_ as one of the elements in the ``features`` list. You can also test your output at `GeoJSONLint <http://geojsonlint.com/>`_.

5. Use your functions above to create a simple screen line counter:

  .. code-block:: python

    def compute_screen_line_counts(feed, linestring):
        """
        Find all trips in the given GTFS feed object that intersect the given Shapely LineString 
        (given in WGS84 coordinates), and return a data frame with the columns:

        - ``'trip_id'``
        - ``'route_id'``
        - ``'route_short_name'``
        - ``'direction_id'``
        """
        pass


6. Use your screen line counter to count the number of trips that cross the Auckland Harbour Bridge. Hint: draw your screen line with GeoJSON IO and convert it to a Shapely LineString with the help of the ``shapely.geometry.shape`` function.

  What basic feature(s) is the screen line counter missing to make its output useful to transit analysts? How could you speed up your function?


Homework 4
===========
Theme: Git

This homework assignment is not about data analysis per se, but understanding the content herein ---version control in general and Git in particular--- will help you tremendously on all your data analysis and programming projects.

1. Read the beginning of the `Wikipedia article on Git <https://en.wikipedia.org/wiki/Git>`_. Read `this conceptual Git tutorial <https://www.sbf5.com/~cduan/technical/git/>`_. Do `this interactive, command-driven Git tutorial <https://try.github.io/levels/1/challenges/1>`_. For more practice, work through `these Lyndia tutorials <https://www.lynda.com/Git-tutorials/Git-Essential-Training/100222-2.html>`_.

2. Initialize a Git repository in your PyClub directory and use Git from now on to track its changes.

3. If you work on PyClub on more than one computer or on a team, create a Github account (free public repositories) or a Gitlab account (free public *and* private repositories) to host your PyClub Git repository on the web. Practice syncing your local Git repository with this remote Git repository. 

4. Read `this tutorial on collaborative workflows <https://www.atlassian.com/git/tutorials/comparing-workflows>`_.


Homework 5
===========
Theme: GeoPandas

1. `Read about GeoPandas <http://geopandas.org/index.html>`_ and then `install it <http://geopandas.org/install.html>`_.

2. Create a GeoPandas geodataframe of Auckland roads from the appropriate file in the ``data`` directory. I got this data from `Mapzen metro extracts IMPOSM format here <https://mapzen.com/data/metro-extracts/metro/auckland_new-zealand/>`.  Reproject the data from the WGS84 projection (EPSG 4326) to New Zealand Transvere Mercator projection (EPSG 2193) so that the units will be meters.

3. Create a GeoPandas geodataframe of New Zealand crash point locations from the appropriate file in the ``data`` directory. I got this data from `NZTA <http://www.nzta.govt.nz/safety/safety-resources/road-safety-information-and-tools/disaggregated-crash-data/>`_.  Set the project for the geodataframe to the New Zealand Transvere Mercator projection (EPSG 2193). Restrict the crashes to Auckland locations.

4. Plot the crashes overlaid on the roads in your notebook.

5. Compute Auckland's crashy roads. Do this by scoring each road according to the sum of its number of crashes divided by its length in meters.

  Hint: Buffer the crash points by 10 meters, say, and spatially join them with the roads. 
  Aggregate the result to calculate the crash score for each road.
  
6. Plot the result using GeoJSON IO, color-coding the roads by crash score.

  Hint: Add to your geodataframe from step 5 the extra columns "stroke" (line color as a HEX color code) and "stroke-width" (line weight in number of pixels) and then export to GeoJSON. Using the `Spectra library <https://github.com/jsvine/spectra>`_, say, for smoothly blending colors is a nice extra touch.


Resources
==========
- `The Hitchhiker's Guide to Python <http://docs.python-guide.org/en/latest/>`_
- `PEP8 <http://pep8.org/>`_
