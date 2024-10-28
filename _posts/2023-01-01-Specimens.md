---
layout: post
title: Machine Learning & NER
subtitle: Enhancing the Museum Data Ecosystem
---
A 2022 LEADING Fellowship & Smithsonian Institution collaboration project. 

Harnessing the capabilities of Named Entity Recorgnition (NER) machine learning tools, this project demonstrates the research output of scholars utilizing Smithsonian museum specimens.

<div align="center">
    <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Arteaga_snail_eating_snakes.png" alt="Fig 1" width="50%">
</div>

In this project, we attempt to demonstrate the scholarly impact of natural history specimen collections through citation analysis and bibliometrics.  Of the obstacles we encountered, the most notable was the inconsistent ways in which specimens are cited in literature, which necessitated the use of named entity recognition machine learning tools to find and isolate specimen citations from the research publications. 

In our research output, we illustrate:
- The efficacy of a trained named entity recognition machine learning model compared to pattern recognition and other popular AI tools.
- The frequency of specimen citations from a specific collection out of 1,300 publications.

I partnered with:<br>
Richard Naples, Smithsonian Libraries and Archives<br>
Sara Lafia, University of Michigan, School of Information<br>
Andrea Thomer, Assistant Professor at the University of Arizona School of Information



### Source Data
For this project, we collected full text PDFs of scholarly papers that have been collected by the collections and library staff at the University of Michigan Museum of Zoology and the Smithsonian Institution. The combined corpus was 1,308 papers total.

We parsed the papers using GROBID, a machine learning python library for extracting structured text (JSON) from semi-structured PDFs. We then tokenized the text into sentences and captured metadata for each paper’s unique identifier, its title, and the section of the article where the sentence appeared. 

To establish a baseline estimate for specimen citation we manually reviewed and validated a subset of 375 sentence segments from 146 papers, which we refer to as the “truth deck.”

### Extracting specimen references
We used three approaches for extracting specimen references: 1) pattern matching with regular expressions (RegEx); 2) a custom named entity recognition (NER) model; and 3) queries to a large language model (GPT-3). We compared the predictions using each approach to the label in the truth deck.

The custom NER model was trained using the spaCy library in Python. We extracted ~2,000 sentences out of 400 papers with potential specimen citations to create training and validation data. The candidates were manually vetted in Prodigy version 1.11.8, an annotation tool based on the spaCy library. The vetting yielded over 1,000 unique specimen annotations in the training set and 728 in the validation set. We also extracted over 126,000 sentences and used those to create custom word vectors for our model. 

<div align="center">
    <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/prodigy_screenshot.jpg" alt="Fig 2" width="50%">
</div>


The pipeline was trained with spaCy using a blank English language model and a custom NER component. The best model had a precision score of 92, recall score of 95, and combined F-score of 94.

The model was trained on examples that we found using RegEx, using a predetermined list of known museum prefixes and numbering schema, and the examples were weighted heavily towards the UMMZ and USNM collections. But the NER model was able to generalize from the examples used in training to extract specimens with numbers and prefixes that were not included in training. 

The NER model was also able to overcome the common pitfalls that befell a pattern matching or RegEx algorithm. The scholarly papers were rife with dozens of other complex numbers describing genes, camera lenses, zip codes, grant funded projects, and all manner of other metadata. The trained NER model was able to avoid extracting these numbers based on context words. 


### Results
By comparing our results from the three different methods against the truth deck, we found that the custom NER model was the most successful, owing to its flexibility and adaptability with common edge cases.

Below are some results from using the NER model to mine specimen citations from the entire corpus of 1308 papers in the UMMZ and USNM bibliographies. The results from the NER model were cleaned in sql and the graphs created using the seaborn and matplotlib libraries in python.

#### Specimens by Paper Section
![frequency_by_section](https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/frequency_by_section.png)

#### Journals with the highest number of specimen citations
![frequency_by_journal](https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/frequency_by_journal.png)

#### Frequency of Specimen Citations by Year of Publication
![frequency_by_year](https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/frequency_by_year.png)

<br>
<br>
<br>




Citations:
Figure 1: Arteaga, A., Mebert, K., Brito, J., Salazar-Valenzuela, D., & Torres-Carvajal, O. (2021). *Systematics of South American snail-eating snakes Dipsas (Serpentes: Colubridae), with the description of three new species from the Pacific lowlands of northwestern Ecuador*. Zootaxa, 4920(1), 1-41. https://doi.org/10.11646/zootaxa.4920.1.1




