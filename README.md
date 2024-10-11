EXPLANATION

Text Processing
The preprocess_text function employs several steps to clean and standardize text data, crucial for 
effective natural language processing:
1. Library Utilization:
• WordNetLemmatizer (NLTK) : Used for lemmatization, converting words to their base
form.
• String and re libraries: Employed for punctuation removal and text manipulation.
2. Punctuation Removal and Lowercasing:
• Text is stripped of punctuation and converted to lowercase, ensuring uniformity and
focusing on meaningful text.
3. Tokenization:
• The cleaned text is tokenized into individual words using NLTK's word_tokenize, enabling
word-level analysis.
4. Stopword Removal and Lemmatization:
• Stopwords (common words like "the", "is", "in") are removed.
• Lemmatization: Words are reduced to their dictionary form (e.g., "running" to "run"),
consolidating different forms of the same word.
5. Output :
• The function outputs a list of clean, lemmatized tokens, free from punctuation, stopwords, 
and casing inconsistencies.
This preprocessing enhances the analysis quality by focusing on the most relevant and standardized
textual elements.
Changing BM25 parameters
The BM25 parameters k1 and b are used to control term frequency normalization and document length 
normalization respectively.
The best parameters after ranking with Word2Vec are: bm25_k1 =3 and bm25_b= 0.80.
The best parameters after ranking with BERT are: bm25=1.5 and bm25_b=0.75.
Reranking
-------------------------------------------------------------------------------------
1. Reranking with Bert
Reranking with BERT involves refining the initial document ranking obtained from BM25 
by incorporating semantic understanding through BERT embeddings. BERT, or
Bidirectional Encoder Representations from Transformers, captures contextual
1.2 BERT Embeddings:
Generated using a pre-trained BERT model that called «paraphrase-minilm-l6-v2 », 
these embeddings encode contextual information and semantic relationships within the
text.
1.3 Cosine Similarity:
Measures the similarity between BERT embeddings of the query and each document. It
is used to rerank the initially retrieved documents.
1.4 Reranking Process :
• For each query, BM25 retrieves an initial set of documents (top 5 in this case).
• BERT embeddings are obtained for both the query and retrieved documents.
• Cosine similarity scores are calculated, allowing reranking based on semantic 
relevance.
1.5 Evaluation Metric - NDCG@5:
Normalized Discounted Cumulative Gain is used as an evaluation metric to assess the
quality of the reranked documents. It considers both the relevance and position of 
documents in the ranking.
1.6 Conclusion:
The combination of BM25 for initial retrievel and reranking with BERT embeddings 
represents a two-step approach that capitalizes on the strenghs of both methods.
While BM25 efficiently handlesterm-based matching and document ranking, BERT brings 
contextual and semantic insights, contributing to a more nuanced and accurate final
ranking. The reranking process is evaluated using NDCG, providing a quantitative 
meseaure of the improvement achieved through the incorporation of
BERT embeddings.

2. Semantic Reranking with Word2Vec
The integration of Word2Vec into the BM25 retrieval process represents an advanced
approach to enhance the relevance of search results
2.1 Vectorization:
For each query, its vector representation is generated using the Word2Vec model.
2.2 Reranking: 
The top documents (top 5 in this case) as ranked by BM25 are reranked based on the
cosine similarity between their vector representations and that of the query. This step
aims to enhance the relevance of the search results by considering the semantic
relationships captured by Word2Vec.
2.3 Error Handling and Evaluation
• Error Handling : The code includes a mechanism to handle missing document IDs
during reranking, ensuring robustness.
• Evaluation Metric - NDCG@5: The effectiveness of this combined approach (BM25
followed by Word2Vec reranking) is evaluated using the Normalized Discounted Cumulative 
Gain at rank 5 (NDCG@5), focusing on the quality of the top search results.
2.4 Conclusion
By integrating Word2Vec, the retrieval system not only leverages the keyword-based
strengths of BM25 but also enhances the ranking with semantic understanding from
Word2Vec. This approach aims to surface more contextually relevant documents in
response to user queries, potentially improving the overall search experience as evaluated
by NDCG@5.
