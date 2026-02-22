# Automated Intelligence Topic Modeling and Interpretive Analysis of Global Social Media Conversations
## Project Overview
This project presents a scalable, unsupervised Natural Language Processing (NLP) framework for discovering and interpreting large-scale global social media conversations.
Using transformer-based embeddings, density-based clustering, and a custom stance-analysis module, the system identifies coherent discussion topics and uncovers internal viewpoint structures within each topic.
The pipeline was designed to operate on high-volume, unstructured social media data without requiring manual labels.
## Problem Statement
How can we autonomously detect, cluster, and interpret large-scale global online discussions without supervised labels?
Social media data presents several challenges:
* Massive data volume
* Short, noisy text
* Overlapping semantic themes
* Polarized and contradictory viewpoints
* Multidimensional emotional tone
This project addresses these challenges using a structured unsupervised modeling approach.
## Dataset
**Source:** Global social media corpus (~65 million posts)
**Modeled subset:** 70,000 English-language posts
**Fields included:**
* Raw text
* Sentiment scores
* Emotion labels
* Metadata (language, timestamps)
The subset was selected due to computational constraints while preserving topic diversity.
## Architecture Overview
The system consists of two main modules:
### 1. Topic Modeling Pipeline
**Step 1:** SBERT Embeddings
* **Model:** all-MiniLM-L6-v2
* 384-dimensional semantic embeddings
* Optimized batch processing
* Embeddings persisted to disk for reuse
**Step 2:** UMAP Dimensionality Reduction
* Reduced embeddings to 10 dimensions
* Preserved semantic structure
* Parameters tuned for clustering stability
**Step 3:** HDBSCAN Clustering
* Density-based clustering
* Automatically determined number of topics
* Resulted in ~871 distinct topics
* Outliers labeled as noise
**Step 4:** BERTopic Interpretation
* Class-based TF-IDF (c-TF-IDF)
* Extracted representative keywords
* Generated interpretable topic labels
### 2. Stance and Viewpoint Analysis Module
Topic modeling reveals what people discuss.
The stance module reveals how they discuss it.
For each topic:
* Topic slicing (max 500 posts)
* PCA reduction (384 → 20 dimensions)
* KMeans clustering (k = 3) to identify stance groups
* Local contrastive TF-IDF to extract distinctive vocabulary
* Sentiment aggregation per stance cluster
This produced structured, interpretable viewpoint partitions such as:
* Approval / Support
* Disapproval / Criticism
* Curiosity / Inquiry
* Skepticism
* Neutral / Analytical
The stance module provides deterministic, scalable interpretation without relying on generative summarization models.
## Key Results
* Discovered 871 coherent global discussion topics
* Identified consistent multi-stance patterns within high-traffic topics
* Extracted distinctive vocabulary per stance cluster
* Quantified sentiment distribution across viewpoints
* Demonstrated scalable architecture for large-scale discourse analysis
Topics spanned:
* Geopolitics
* Elections and governance
* Public health
* Cryptocurrency markets
* Economic policy
* Cultural movements
* Technology and AI
## Storage and Reproducibility Strategy
Due to computational cost:
* SBERT embeddings (~1 hour computation) were persisted
* BERTopic model was saved
* Processed dataframe stored in columnar format
This design ensured reproducibility and eliminated re-computation across sessions.
## Technical Stack
* Python
* Sentence-BERT (all-MiniLM-L6-v2)
* UMAP
* HDBSCAN
* BERTopic
* Scikit-learn
* TF-IDF
* PCA
* Pandas
* NumPy
## Limitations
* 70k subset used due to compute constraints
* English-only modeling
* No temporal topic evolution modeling
* Short social posts may lack semantic richness
## Future Work
* Multilingual expansion (XLM-R or mBERT)
* Supervised stance classification
* Temporal trend analysis
* Interactive dashboards for real-time monitoring
* Scalable deployment architecture
