# inforet-notes

**Per andare a capo due spazi di fila**

Spacy Linguistic Features https://spacy.io/usage/linguistic-features  
Spacy 101 https://spacy.io/usage/spacy-101

nltk.tokenize package https://www.nltk.org/api/nltk.tokenize.html Ha due tokenizer uno per le parole e uno per le frasi. Se ho tante frasi prima uso il tokenizer per le frasi e poi quello per le parole

**Vector space model** https://towardsdatascience.com/vector-space-models-48b42a15d86d

Mapping documents to the vector space:
1. Tokenize
2. Normalize (considero tutti i termini nella stessa maniera, la maniera più banale per farlo è mettere tutte le parole in minuscolo)
3. Weight/Score (la maniera più banale per farlo è assegnare ad ogni parola il numero di volte che questa appare)
4. Indexing

Per processare una query: 
- trasformo il documento in vector space
- trasformo la query in vector space
- distanza tra query vector e documents vector
- sort documents by the closeness of the query
- the closest ones are the more relevant for the query

How can we do the transformation into the vector space?
- term frequency
- Idf
- TfIDf (migliore) (By combining term frequency and inverse document frequency we obtain a measure that takes into account the specific relevance of a terms with respect to a document)

How can we know if these are good answers or not?
