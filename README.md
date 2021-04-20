# MusicBrainz-CountryNet  
Scrape release group data from the MusicBrainz website and use it to create a network (Nodes: artists; Edges: Shared credit for release [Edge weights: Sum of the number of tracks credited together])
  
  
## Notebooks
1. test_scrape_releases.ipynb
* Use MusicBrainz IDs from kaggle artist.csv ([Dataset](https://www.kaggle.com/pieca111/music-artists-popularity)) to scrape (1) names of contributing artists for each release and (2) number of songs in the release
* Writes a text file (delimiter: '<--->') with each line 
