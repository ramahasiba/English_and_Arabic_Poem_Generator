# General Project Description
This project involves a comparative analysis between two generative models, one for a high-resource language (English) and one for a low-resource language (Arabic). The two generative models trained to generate poems in both languages.

# Corpus used for training 
The Arabic model and the English model were both trained on the "Poem Comprehensive Dataset (PCD)". The Arabic dataset contains a total of 1,831,770 poetic verses. Each verse in the dataset includes information such as the poet's name, the age it was written, and its meter. There are 22 different meters, 3701 poets, and 11 different ages represented in the dataset. However, due to limitations I had in the resources, only 50,000 verses were used for training and evaluation purposes in the Arabic model. 
Similarly, the English dataset which called “merged.csv” consists of 199,002 verses. Each verse in the English dataset is assigned to one of the following meters: iambic, trochee, dactyl, and anapestic. For the English model, a subset of 16,000 verses was used during the training and evaluation process. 

# Models used for training
In the case of the Arabic language, I fine-tuned the “aragpt-base” model which was published on HuggingFace. This model is pre-trained specifically for Arabic text, I tuned it using the corpus of Arabic poetry from the Poem Comprehensive Dataset (PCD). As for the English language, I fine-tuned the GPT-2 model using English peotry from the “merged.cvs” dataset for text generation task.

![Uploading image.png…](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuGFx6%2FbtqBikXQWUd%2FukdCybp6XnwDqzDBJmVzik%2Fimg.png)



# Embedding
GPT-2 model has an embedding layer. This layer automatically handles the task of converting the input into embedded representation before passing it to the mode.

As for the evaluation, I used the “Universal Sentence Encoder (USE)” to find semantic sentence embeddings to calculate the cosine similarity between the ground truth and the predicted verses for evaluation purposes. 


# Libraries Used
* Pyarabic: It was used to preprocess the Arabic text data, utilizing the “strip_tashkeel” function to remove diacritical marks from the verses.

* Transformers: it used to fine-tune the models, utilizing the following classes, or methods (for both languages):
    - AutoTokenizer.from_pretrained used to load the tokenizers to tokenize the data.
    - "DataCollatorForLanguageModeling" used for language modeling. Inputs are dynamically padded to the maximum length of a batch if they are not all of the same length.
    - "AutoModelWithLMHead.from_pretrained" used to initialize the pre-trained GPT-2 models to fine-tune them using poems.
    - "TrainingArguments" class used to specify the output directory, number of training epochs, batch size, and saving steps.
    - "Trainer" class was created with the specified model, training argument, and data collator. I used then its method train to train models with the available corpus.
    - "Pipeline" function used to create the generator which was configured for text generation and uses the specified model tokenizer.

* Tensorflow: from the tensorflow hub, I loaded the USE model to get sentence embeddings to      calculate the similarity to evaluate the model.


# Evaluation
For the evaluation I used the “Universal Sentence Encoder (USE)”  to calculate the textual similarity by calculating the contextual word embedding for each word in the sentence. To find the textual similarity between the verses, the model first computes the contextual word embeddings for each word in the verse, it then computes the verse embedding by performing the element-wise sum of all the word vectors and dividing by the square root of the length of the verse to normalize the verse lengths, after that I’ll be able to calculate the similarity.
Comparing the two models, the English one got an average similarity of 0.188, with a standard deviation of 0.107. On the other hand, the Arabic model demonstrated a significantly higher average similarity of 0.729, with a standard deviation of 0.16. These statistics suggest that the Arabic model tends to produce text that is more closely aligned with the ground truth compared to the English model. The lower standard deviation for the Arabic model indicates a higher consistency in generating text that closely matches the desired output. These findings highlight the effectiveness of the Arabic model in generating coherent and contextually relevant text in the domain of poetry. I suggest retraining the English one on more poet data so maybe it can generate better poems or increase number of epochs while training.


