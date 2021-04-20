# MusicBrainz-CountryNet  
Scrape release group data from the MusicBrainz website and use it to create a network (Nodes: artists; Edges: Shared credit for release [Edge weights: Sum of the number of tracks credited together])
  
  
## Notebooks
**1. test_scrape_releases.ipynb**
* Use MusicBrainz IDs from csv file [[Dataset](https://www.kaggle.com/pieca111/music-artists-popularity)] to scrape (1) names of contributing artists for each release and (2) number of songs in the release
  * Currently set to scape all artists with at least 100,000 listens on lastfm
* Writes a text file (delimiter: '<--->') to cwd with each line repesenting the artists credited for a single release (e.g., a single, EP, or full album) with the last elemet being the number of songs in the release.  

**2. df_extract_node_attrs.ipynb**
* 


**3. make_network.ipynb**
* Reads artist release credit text file and converts to list of lists (Ex: [[artist,artist,num_tracks],[...]]) 



