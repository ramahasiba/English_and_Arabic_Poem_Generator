# Corpus used for training 
The Arabic model and the English model were both trained on the "Poem Comprehensive Dataset (PCD)". The Arabic dataset contains a total of 1,831,770 poetic verses. Each verse in the dataset includes information such as the poet's name, the age it was written, and its meter. There are 22 different meters, 3701 poets, and 11 different ages represented in the dataset. However, due to limitations I had in the resources, only 50,000 verses were used for training and evaluation purposes in the Arabic model. 
Similarly, the English dataset which called “merged.csv” consists of 199,002 verses. Each verse in the English dataset is assigned to one of the following meters: iambic, trochee, dactyl, and anapestic. For the English model, a subset of 16,000 verses was used during the training and evaluation process. 

# Models used for training
In the case of the Arabic language, I fine-tuned the “aragpt-base” model which was published on HuggingFace. This model is pre-trained specifically for Arabic text, I tuned it using the corpus of Arabic poetry from the Poem Comprehensive Dataset (PCD). As for the English language, I fine-tuned the GPT-2 model using English peotry from the “merged.cvs” dataset for text generation task.

# Embedding
GPT-2 model has an embedding layer. This layer automatically handles the task of converting the input into embedded representation before passing it to the mode.

As for the evaluation, I used the “Universal Sentence Encoder (USE)” to find semantic sentence embeddings to calculate the cosine similarity between the ground truth and the predicted verses for evaluation purposes. 

# Libraries Used
* Pyarabic: It was used to preprocess the Arabic text data, utilizing the “strip_tashkeel” function to remove diacritical marks from the verses.
