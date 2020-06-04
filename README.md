# Multimodal Analytics for Real-world News using Measures of Cross-modal Entity Consistency
This is the official GitHub page for the paper:

> Eric Müller-Budack, Jonas Theiner, Sebastian Diering, Maximilian Idahl, Ralph Ewerth:
"Multimodal Analytics for Real-world News using Measures of Cross-modal Entity Consistency".
Accepted for publication in: *International Conference on Multimedia Retrieval (ICMR)*, Dublin, 2020.

## News

###3rd June 2020: 

- **Pre-release** of the *TamperedNews* and *News400* dataset with links to news texts, news images, untampered and 
tampered entity sets, and reference images for all entities. 
- **Splits** for validation and testing
- **Download script** to crawl news texts

###4th June 2020:
- **Full release** of the *TamperedNews* and *News400* dataset including the visual and textual features used in the 
paper
- **Inference scripts** and config files including the parameters used in the paper to reproduce the results for context 
and entity verification. 
- **Word embedding class** to generate textual features

###Future Releases
- **Docker container** with required python libraries
- **Download script** that automatically generates the whole dataset with the intended project structure
- **Web-crawler** to obtain the news and reference images. 
- Source code for **visual feature extraction**

## Content

This repository contains links to the *TamperedNews* ([Link](https://doi.org/10.25835/0002244)) and 
*News400* ([Link](https://doi.org/10.25835/0084897)) datasets. Both datasets include:

- **```<datasetname>```.tar.gz**:
    - ```dataset.jsonl``` containing:
        - Web links to the news texts
        - Web links to the news image
        - Outputs of the named entity recognition and disambiguation (NERD) approach
        - Untampered and tampered entities
    - ```entity_type.jsonl``` file for each entity type containing the following information for each entity:
        - Wikidata ID
        - Wikidata label
        - Meta information used for tampering
        - Web links to all reference images crawled from Google, Bing, and Wikidata
    - splits for testing and validation
- **```<datasetname>```_features.tar.gz**:
    - Visual features of the news images for persons, locations, and scenes
    - Visual features of the reference images for persons, locations, and scenes
- **```<datasetname>```_wordembeddings.tar.gz**: Word embeddings of all nouns in the news texts

Based on the dataset we provide source code and config files the reproduce our results:

- [inference_context.py](https://github.com/TIBHannover/cross-modal_entity_consistency/blob/master/inference_context.py)
  to reproduce the results for context verification
- [inference_entities.py](https://github.com/TIBHannover/cross-modal_entity_consistency/blob/master/inference_entities.py)
  to reproduce the results for person, location, and event verification
- [Config files](https://github.com/TIBHannover/cross-modal_entity_consistency/blob/master/test_yml) including the
  parameters used for the experiments in the paper

## Usage

### Download News Texts

To download the text in the news articles run: 

```shell script
python download_news_text.py \
  -input <PATH/TO/dataset.jsonl> 
  -output <PATH/TO/OUTPUT/DIRECTORY> 
  -dataset <DATASET=[TamperedNews, News400]>
``` 

**Additional parameters:** Run the script with ```--debug``` to enable debugging console outputs.
The number of parallel threads can be defined with: ```--threads <#THREADS>```

**Outputs:** This step stores a variety of meta information for each article with an ID ```document_ID``` in a file: 
```<document_id>.json```. In addition, the news texts are stored along with all other dataset information in a new 
file: ```dataset_with_text.jsonl```.

**Tip:** The script checks whether an article has already been crawled. We recommend to run the script several times 
as some documents might be missing due to timeouts.

## LICENSE

This work is published under the GNU GENERAL PUBLIC LICENSE Version 3, 29 June 2007. For details please check the
LICENSE file in the repository.