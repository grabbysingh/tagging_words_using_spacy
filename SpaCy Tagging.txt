# -*- coding: utf-8 -*-
"""
Created on Mon Nov 30 12:37:49 2020

@author: gaura
"""

import spacy
import pandas as pd

dataset = pd.read_excel('Tagged devices_list_2.xlsx')
#from spacy.cli import download
#download('en_core_web_sm')
nlp = spacy.load('en_core_web_sm')

def tag(dataset, value):
    list_corpus_t = []
    for i in range(0, value):
        corpus_t = []
        j = dataset['Term as String'][i]
        doc = nlp(j)
        for ent in doc.ents:
            k = (ent.text, ent.label_)
            corpus_t.append(k)
        list_corpus_t.append(corpus_t)
    return list_corpus_t

maybetagged = tag(dataset, 2663)
maybetag = pd.DataFrame(maybetagged)
maybetag.to_excel('tagged_pubmed_all.xlsx')
