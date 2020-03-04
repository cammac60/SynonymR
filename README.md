# SynonymR

[Live Site](http://synonymr.surge.sh/) 
[Project Board](https://github.com/cammac60/SynonymR/projects/1)

### Overview

  SynoymR is an app built to help you find synonyms using the Merriam Webster Collegiate Thesaurus API. 
  
### How to Use: 

After navigating to the live site, simply enter a word and recieve back it's synonyms. 

Once some synonyms populate you can click on one of the rendered words to find synonyms for _that_ word. 

### Dev Setup

- Fork and clone down this repo.
- Cd into the repo.
- `npm i` || `npm install`
- `npm run dev`
- Open the app in localhost. 

### Notes

- The Thesaurus API can be slow at times which may cause some timeout issues. There is an error message displayed when this occurs but unfortunately there isn't really any way to solve this on my end besides waiting for the API to open some ports and speed up. When running in the development environment you will get a 503 error in the console if this problem is occurring. 
