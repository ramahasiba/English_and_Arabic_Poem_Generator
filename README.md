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

* Transformers: it used to fine-tune the models, utilizing the following classes, or methods (for both languages):
    - AutoTokenizer.from_pretrained used to load the tokenizers to tokenize the data.
    2. "DataCollatorForLanguageModeling" used for language modeling. Inputs are dynamically padded to the maximum length of a batch if they are not all of the same length.
    3. "AutoModelWithLMHead.from_pretrained" used to initialize the pre-trained GPT-2 models to fine-tune them using poems.
    4. "TrainingArguments" class used to specify the output directory, number of training epochs, batch size, and saving steps.
    5. "Trainer" class was created with the specified model, training argument, and data collator. I used then its method train to train models with the available corpus.
    6. "Pipeline" function used to create the generator which was configured for text generation and uses the specified model tokenizer.
