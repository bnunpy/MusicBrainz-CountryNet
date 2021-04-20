# MusicBrainz-CountryNet  
Scrape release group data from the MusicBrainz website and use it to create a network (Nodes: artists; Edges: Shared credit for release [Edge weights: Sum of the number of tracks credited together])
  
  
## Notebooks
### 1. test_scrape_releases.ipynb
* Use MusicBrainz IDs from csv file [[Dataset](https://www.kaggle.com/pieca111/music-artists-popularity)] to scrape (1) names of contributing artists for each release and (2) number of songs in the release
  * Currently set to scrape all artists with at least 100,000 listens on lastfm
* Writes a text file (delimiter: `'<--->'`) to cwd with each line repesenting the artists credited for a single release (e.g., a single, EP, or full album) with the last element being the number of songs in the release.  

### 2. df_extract_node_attrs.ipynb
* The goal here is to get the Country, Genre Tags, and Number of Listens for each artist so that each node (artist) can be assigned these attributes in the network.
* From the previously mentioned Dataset, we (1) deal with repeated artist names by keping only the first, (2) fill in missing mb column values with the lastfm values, (3) drop all columns except for 'artist_mb', 'country_mb', 'tags_mb', and 'listeners_lastfm', and (4) convert the dataframe to a dictionary with index orientation.
  * For parsing Country and Genre Tags, split on `';'`.  Some artists are attributed more than one Country, so only keep one.
  * For the purpose of network visualization, it may be best to normalize the number of listens:  
  `df['listeners_lastfm'] = df['listeners_lastfm'] /df['listeners_lastfm'].abs().max()`
 * Pickles the dictionary  

### 3. make_network.ipynb
* Reads artist release credit txt file and converts to list of lists (Ex: `[[artist1 ,artist2, num_tracks], [...]]`) 
* Also reads the picked dict from previous notebook
* **Creates a `networkx` Graph** by iterating over combinations (`r=2`) of artists for each release credit. Since the last element of each release credit is the number of songs in the release, makes the weight of the edge the number of songs (Defaults to dividing the number of songs in a release credit by the number of artists credited). 
  * Assigns Country, Genre Tags, and Number of Listens attributes to each node by look-up from dictionary
* **Visualization** with `pyvis.network` at the end of this notebook.
