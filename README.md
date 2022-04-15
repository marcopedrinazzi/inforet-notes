# inforet-notes

**Per andare a capo due spazi di fila**

## Lezione 2

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

## Lezione 3

How can we know if these are good answers or not?

La nozione di qualità dipende dal task che vogliamo fare. 
Non basta avere un sistema e un dataset. Se il sistema è l'unico modo per valutare il dataset non c'è nessun altra maniera di sapere se la qualità è ok.

**Serve un terzo componente.** => ground truth => list of documents from the dataset che sono gli expected documents for a given query. La ground truth è QUERY, ASSOCIATA CON LA RIGHT ANSWER. Così posso far andare queste query sul mio sistema e vedere se ho il risultato che mi aspetto grazie alla ground truth. 

Per costrutire la ground truth: grazie a dataset di ground truth, grazie a un grande numero di utenti che lo fanno manualmente. Importante avere le risposte corrette e anche le risposte FALSE corrette. "No, non è questo documento".

**Context annotation** la maggior parte dei tweets sono annotati: con domain e entity. Il domain indica la categoria del tweet. La context annotation è usata per creare la ground truth

Run the query, rank the documents and then select the top x OPPURE (ed è meglio) si può usare una soglia 

**The notion of quality**
Definition 1: when the documents contained in Aq,C are relevant to q. We can measure the quality of our system according to this notion of quality, called **Precision**.  
**Precision = relevant retrieved/retrieved***

Precision is necessary but not sufficient property of a good search system. *Many relevant documents CAN MISS despite having a precision of one.*  
SERVE UN'ALTRA MISURA 
Definition 2: when all the relevant documents contained in C are retrieved by q **si chiama RECALL = relevant retrieved/relevant** 

*in Web: download subset of data, creare ground truth e poi valutare dati su questo sample*

RECALL NON è ABBASTANZA, SERVE UN'ALTRA MISURA. Inoltre bisogna bilancare con precision, buona precisione e buon recall. In alcune applicazioni recall è piu importante di precision e viceversa.  
Definition 3: we aim at a system with a good tradeoff between precision and recall; this can be measured by
the **f1-score**

positive/negative = retrieved/not retrieved by the system  
True = correct  
False = not correct  

Possiamo definire Precision, Recall e F1 grazie a TP e FP.

The accuracy is how many true (TP o TN) things i did in the whole dataset. Non buono. Meglio lavorare su TP, FP, FN (FP e FN sono gli errori e TP è il positive correct result)
 
Confusion matrix. Permette di avere una visione d'insieme.

Il mapping nell'esempio di tweet search è la ground truth. Variabile M.

Importante avere più di una/due query su cui lavorare.

The domain e entity data corrispondono a due diversi information needs.

Una maniera per rappresentare la ground truh è tramite in set. Oppure tramite un vettore con dimensione pari a quella di tutto il dataset. Ogni elemento del vettore corrisponde ad un documento (come posizione) e ogni elemento è 0/1. Quindi è una variabile casuale RISPETTO alla query. 0 è falso 1 è vero.

Pseudo cosine

Per settare un threshold si fanno dei calcoli statistici.

# Lezione 4

In tweet search mostra l'implementazione di ciò che è stato fatto from scratch in l3 ma con funzioni di scikit learn.

support = numero di documenti in quella classe rispetto al totale del sistema. Guardando la confusion matrix ci si fa una idea di come performare il sistema.

Settare threshold diversi cambia completamente le performance del sistema

Cosa ci si aspetta dai ranking systems? che i top results siano corretti.  
i_precision = interpolated precision

Una slope nella pr curve è negativa 
----
Consideriamo parole indipendenti dalle altre.

Feedback e si usa il feedback per migliorare le query. (query expansion)

Rocchio algorithm: The idea is to push the new query towards the centroid of the true positive results, according to the relevance feedback, and far from the false positive ones. 

Il grafico su Rocchio Algorithm dice come far ottenere un migliore risultato. Query => revised queyr.

Ground truth as feedback => wrong

# Lezione 5 (continua argomenti lezione 4 all'inizio)

WordNet è organizzato come un dizionario. https://www.nltk.org/howto/wordnet.html
Synset sono i significati.
WordNet è una knowledge base => devo curare e stare attento ai significati diversi. "WORD DISAMBIGUATION". Si ha anche su wikipedia => se cerco su wikipedia Berlin appaio tanti risultati.

Wikidata is a free and open knowledge base that can be read and edited by both humans and machines.
Wikidata acts as central storage for the structured data of its Wikimedia sister projects including Wikipedia, Wikivoyage, Wiktionary, Wikisource, and others.

query.wikidata.org => a way to add knowledge

ConceptNet è un'altra maniera per aggiungere knowldge. E' una via di mezzo/mix tra wordnet e wikidata. https://conceptnet.io

# Lezione 6 (slide p1-5)

Slide 7

# Lezione 7 (slide p1-5)

(fine probabilistic)

**TOPIC MODELING**: il problema di dare un significato è difficile. Cosa vuol dire "meaning"? Il meaning dipende dal contesto. Ogni parola ha un contesto ma devo tenere in considerazione il contesto in cui viene usata.

Problemi vector space model: high dimensionality, synonymy, ambiguity.

Capire il topic del documento => per dare risposta alla query.

LSI è l'idea originale, non molto usata attualmente ma comunque effective

# Lezione 8

LSI for topic modelling: trovare latent variable che rappresentano il significato di collezione di documenti. le latent variable sono i topics. I topic possono migliorare la ricerca, non cerchiamo per parole specifiche ma trasformiamo la query in latent variable information e usiamo queste informazione per la ricerca
-------
Topic modeling: extracts topic associated with a terminology. The topic is a latent variable, it doesnt have an interpretation per se, you have to see the most relevant words for the topic to understand its meaning.
Second one: it is an alternative way to vectorize a document, alternative to tfidf

# Lezione 9

**Text classification**: la classificazione può essere supervised or unsupervised. (a lezione vediamo unsupervised). La classificazione è basata solo sui documenti in questo caso.  

Overlapping classes: each document can be in more than one class

soft binary: è una delle due ma con una certa probabilità (fuzzy classification)

# Lezione 10

DOC => Tokenization => vectorization

fit and predict

**Ex** - ANOTHER STRATEGY to describe clusters: Take the centroid and extract the most representative doc per ogni cluster

**SUPERVISED TEXT CLASSIFIFICATION**

# Lezione 11

**LINEAR CLASSIFIERS** non ha fatto slide. Solo il notebook.