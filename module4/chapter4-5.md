# Activity: Text analysis and visualisation with R

## Text analysis and visualisation with R

Wordclouds are one way to visualise word collections e.g. a document (or collection of collections = corpus).

If your text is not clean & tidy then you may have to transform or ‘clean’ it.

There are many transformations that can be made to raw text e.g.:

* Convert the text to lower case
* Remove numbers
* Remove common stopwords (e.g. ‘the’)
* Remove your own stop words (e.g. for a specific topic)
* Remove punctuation
* Remove extra white space
* Text stemming (common root words, not necessarily real words)
* Lemmatisation (common dictionary root words)
* Special characters e.g. replacing “/”, “@”
* Really special characters like ü ö ä Ä Ü Ö (and those are just the umlauts)
* Really, really special characters like unprintable whitespace, unicode, emoticons

Based on: http://www.sthda.com/english/wiki/text-mining-and-word-cloud-fundamentals-in-r-5-simple-steps-you-should-know

Data file download: [WordCloud.txt](diagrams_datasets/section5/WordCloud.txt)


```r
# we need the following libraries
library("tm") # for text mining
library("SnowballC") # for text stemming
library("wordcloud")
library("RColorBrewer")
 
# Read the text file
filePath <- "WordCloud.txt" # or get your own this is one of subject chapters
text <-readLines(filePath) # Load the data as a corpus and save a copy as 'input'
input <- Corpus(VectorSource(text))
docs <- input
```

You can ‘inspect(docs)’ but it’s messy. Just open the file “WordCloud.txt” to inspect.

Or look at the source (may have changed): https://www.alexandriarepository.org/reader/making-sense-of-relational-and-textual-data/76218

<mark class="big">**Do some processing**</mark>

We want to isolate all the words, convert to a matrix, count them, sort them, dump them into a DataFrame
(for display and for wordclouds)


```r
dtm <- TermDocumentMatrix(docs)
m <- as.matrix(dtm)
v <- sort(
  rowSums(m),
  decreasing = TRUE
)
d <- data.frame(
  words = names(v),
  freq = v
)
nrow(d) # how many 'words'
head(d,10) # look at top 10
```

<mark class="big">**How many ‘words’ are there?**</mark>

<mark class="big">**Have a look at the tail too, not so pretty…**</mark>


```r
tail(d ,10) 
# or look at all the words with
# d$word
# generate the raw word cloud, OK here because it's 'reasonably' tidy text
# up to you if you want to try this with e.g. tweetsset.seed(1234)
# so that the cloud is reproducible, optional
 
wordcloud(
  words = d$words,
  freq = d$freq,
  min.freq = 1,
  max.words = 200,
  random.order = FALSE,
  rot.per = 0.35,
  colors = brewer.pal(8,"Dark2")
)
```

Your turn, change the min.freq then the max.words and run a few times to test

What’s the difference between the two parameters?

We can see from the frequency table and the wordcloud, that ‘the’ is a winner.

**Do the common words (e.g. ‘the’) distort our analysis?**

These common words are referred to as ‘stop words’

So, before we remove them… who are these stopwords anyway?


```r
stopwords("english")
stopwords("french") # c'est la vie...
stopwords("romanian") # why not...
stopwords("swahili") # no... boo
 
docs <- tm_map(docs, tolower) # make all letters to lowercase
docs <- tm_map(docs, removeWords, stopwords("english")) 
# this is destructive, you may need to start again or use the copy 'input'
# and process again
 
dtm <- TermDocumentMatrix(docs)
m <- as.matrix(dtm)
v <- sort(rowSums(m),decreasing=TRUE)
d <- data.frame(words = names(v), freq=v)
nrow(d)
head(d, 10)
 
# and display again, 'the' should be gone
set.seed(1234)
wordcloud(
  words = d$words, freq = d$freq, min.freq = 1,
  max.words=200, random.order=FALSE, rot.per=0.35, 
  colors=brewer.pal(8, "Dark2")
)
```

use `?TermDocumentMatrix` to have a look at the data you used.

Notice above ‘word’ and ‘words’ (‘document’ & ‘documents’ etc.)…. how to fix that?


```r
stemCompletion(c("visualis","techniqu","identifi"), d$words) 
stemCompletion(c("visualis","techniqu","identifi"), d$words, type = "prevalent") 
stemCompletion(c("visualis","techniqu","identifi"), d$words, type = "random")
```

Also try to run the above code a few times to see what happens.

This is called **stemming**, which is finding the word stem of an input.

Is stemming reversible?

What does ‘prevalent’ mean/do?

Let’s go ahead and stem the doc.


```r
docs <- tm_map(docs, stemDocument)
dtm <- TermDocumentMatrix(docs)
m <- as.matrix(dtm)
v <- sort(rowSums(m),decreasing=TRUE)
d <- data.frame(words = names(v),freq=v)
nrow(d)
head(d, 10)
set.seed(1234)
wordcloud(
  words = d$words, freq = d$freq, min.freq = 1,
  max.words=200, random.order=FALSE, rot.per=0.35, 
  colors=brewer.pal(8, "Dark2")
)
```

The more fixes you make, the more the anomalies rise from the depths http://stackoverflow.com/questions/24311561/how-to-use-stemdocument-in-r

<br><br>

**Consider also the order in which you perform these transformations (e.g. stemming, stopwords), is any repetition required?**

Try stemming first?

Note also that punctuation confuses wordStem so you would have to take them out as well.

http://stackoverflow.com/questions/7263478/snowball-stemmer-only-stems-last-word 

**Stemming first, input is original data.**


```r
# stemming first, input is original
docs <- tm_map(input, stemDocument, language = "english")  
# docs <- tm_map(docs, stemDocument)
dtm <- TermDocumentMatrix(docs)
m <- as.matrix(dtm)
v <- sort(rowSums(m),decreasing=TRUE)
d <- data.frame(words = names(v),freq=v)
nrow(d)
head(d, 10)
set.seed(1234)
wordcloud(words = d$words, freq = d$freq, min.freq = 1,
          max.words=200, random.order=FALSE, rot.per=0.35, 
          colors=brewer.pal(8, "Dark2"))
 
 
# Remove common English stopwords (e.g. 'the')
docs <- tm_map(docs, removeWords, stopwords("english"))
dtm <- TermDocumentMatrix(docs)
m <- as.matrix(dtm)
v <- sort(rowSums(m),decreasing=TRUE)
d <- data.frame(words = names(v),freq=v)
nrow(d)
head(d, 10)
set.seed(1234)
wordcloud(words = d$words, freq = d$freq, min.freq = 1,
          max.words=200, random.order=FALSE, rot.per=0.35, 
          colors=brewer.pal(8, "Dark2"))
```

#### Associations {-}

Which words occur with, or alongside others


```r
findAssocs(dtm, terms = "kimbal", corlimit = 1) # ha (and note lowercase, must be automated)
```

<mark class="big">What does corlimit mean here?</mark>


```r
findAssocs(dtm, terms = "text", corlimit = 0.5) #
```

## Lemmatizers {-}

Note that lemmas differ from stems in that a lemma is the root form of the word, while a stem may not be a real word.

There are a few Lemmatizers about e.g.

* Stanford NLP
* Treetagger
* koRpus # seems better to install locally…
* Wordnet
* NLTK (Python)

Here’s one that works:

http://stackoverflow.com/questions/22993796/lemmatizer-in-r-or-python-am-are-is-berequire

You may find the url is different, it is because the Northwestern University update their URL for this service.


```r
require(httr) # may have to install these two
require(XML)
 
lemmatize <- function(wordlist) {
  get.lemma <- function(word, url) {
    response <- GET(url,query=list(spelling=word,standardize="",
                                   wordClass="",wordClass2="",
                                   corpusConfig="ncf",    # Nineteenth Century Fiction
                                   media="xml"))
    content <- content(response,type="text")
    xml     <- xmlInternalTreeParse(content)
    return(xmlValue(xml["//lemma"][[1]]))    
  }
   
  # here's the code
  url <- "http://classify.at.northwestern.edu/maserver/lemmatizer" 
  return(sapply(wordlist,get.lemma,url=url))
}
 
words <- c("is","am","was","are")
lemmatize(words)
# is am  was  are 
# "be" "be" "be" "be" 
# 'to be'
words <- c(
  "walk","walking","walked","walk",
  "Walker", "walks", "Walker Texas Ranger",
  "sidewalk"
  )
lemmatize(words)
words <- c("Walker Texas Ranger","range","ranger","ranged","rangy","Ranger") 
# so ranger as in rang a bell!? <sigh> English </sigh>
lemmatize(words)
```

## Text networks

We can apply network analysis to text, or more precisely terms or words in text and their connections

e.g. ‘data’ and ‘mining’ may commonly occur together

Below is a selection of terms from a document with connections between them represented as a matrix

Data file download: [termDocMatrix.rdata](diagrams_datasets/section5/termDocMatrix.rdata)


```r
# load termDocMatrix
load("termDocMatrix.rdata")
# inspect part of the matrix
termDocMatrix[5:10,1:20]
# Transform Data into an Adjacency Matrix
# change it to a Boolean matrix
termDocMatrix[termDocMatrix>=1] <- 1
# transform into a term-term adjacency matrix
termMatrix <- termDocMatrix %*% t(termDocMatrix)
# inspect terms numbered 5 to 10
termMatrix[5:10,5:10]
```

Why is ‘data’ most commonly associated with ‘data’ i.e. what does ‘data’ 53 mean?

Inspect the diagonal (top left to bottom right)

Build a graph from the matrix:


```r
library(igraph)
 
g <- graph.adjacency(termMatrix, weighted=T, mode = "undirected")
 
# remove loops
g <- simplify(g)
 
# set labels of vertices
V(g)$label <- V(g)$name
 
# set seed to make the layout reproducible
set.seed(3952)
layout1 <- layout.fruchterman.reingold(g)
plot(g, layout=layout1)
# plot(g, layout=layout.kamada.kawai)
```

How many times did ‘r’ occur in the text?

Try other layouts.

Which is better to learn about relationships between data, the matrix or the graph?

***




