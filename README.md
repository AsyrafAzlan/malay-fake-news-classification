# malay-fake-news-classification
Malay Fake News Classification using:
</br>1.  CNN [3]
</br>2.  BiLSTM [4]
</br>3.  C-LSTM [5]
</br>4.  RCNN [6]
</br>5.  FT-BERT [7]
</br>6.  BERTCNN (A unique method in this project that uses the sequence output from the last BERT layer to be provided to CNN layers).

The result of this project produced a filtered Malay fake news dataset which can be downloaded from **malaya_fake_news_preprocessed_dataframe.pkl**.
</br>The news articles from the original dataset [1] that cannot be correctly classified by all the models are treated as outliers and filtered out.

The following command will load and display the dataset:
```bash
import pandas as pd
df_allnews_unpickled = pd.read_pickle("./malaya_fake_news_preprocessed_dataframe.pkl")
df_allnews_unpickled
```
<p align="center">
  <img src="https://github.com/AsyrafAzlan/malay-fake-news-classification/blob/main/model_architecture_imgs/dfss.PNG">
</p>
<p align="center">
  <img src="https://github.com/AsyrafAzlan/malay-fake-news-classification/blob/main/model_architecture_imgs/preprocess_tokens.PNG">
</p>

**Column descriptions:**
</br> **news**: Original news articles that have been cleaned minimally - lowercased, added space between specific symbols, "hb" & "th" e.g. 4th/13hb -> 4 th/ 13 hb.
</br> **tokens**: Tokenized words from **news** column.  Changed numbers from digits to ordinal spellings.  (See image above)
</br> **rejoined**: Rejoined sentences from **tokens** column.  Mostly used for BERT models as they have their own tokenizer.
</br> **length**: Length of sentences based on **tokens**.
</br> **label**: Class label. 1 for real news. 0 for fake news.
</br> **real**: One-hot encoding column for real news.
</br> **fake**: One-hot encoding column for fake news.
</br> Further information regarding this dataset can be found in the following table.

<p align="center">
  <img src="https://github.com/AsyrafAzlan/malay-fake-news-classification/blob/main/model_architecture_imgs/dfinfo.PNG">
</p>


-----------------

The following experiments/modifications were done before filtering the outliers to achieve the best result:
* **Normal**:  All fake news articles originally from [1] are considered.
* **<1000**:  Only news articles with less than 1000 words are considered because those with more are very few in numbers.
* **Trunc128**:  All news articles are truncated to have a maximum sequence length of 128 (the standard for BERT models in this project).
* **Summarized**:  News articles with more than 200 words are first summarized using TF-IDF scores and Hopfield Network and are then truncated at 128 sequence length.  The summarization method can be found in my "article-summarization" project.
* **Filtered**:  All news articles that cannot be classified by all models are considered as outliers and removed from the original dataset.

<p align="center">
  <img src="https://github.com/AsyrafAzlan/malay-fake-news-classification/blob/main/model_architecture_imgs/models_f1_flipped_resized_prcnt.png">
</p>


-----------------

**Disclaimer:**  The "how-to" files may display some old results though with accurate process and methodology.

The original dataset, toolkit and pre-trained BERT model are provided by:
</br>[1] Zolkepli, Husein. “Malaya-Dataset.” Github-huseinzol05/Malaya-Dataset: Text corpus for Bahasa Malaysia. https://github.com/huseinzol05/Malaya-Dataset (accessed April 29, 2019).
</br>[2] Zolkepli, Husein. “Malaya.” Github-huseinzol05/Malaya: Natural-Language-Toolkit for Bahasa Malaysia. https://github.com/huseinzol05/Malaya (accessed April 29, 2019).

The chosen model architectures for this project are applications of the following papers:
</br>[3] Kim, Yoon. "Convolutionalneural networks for sentence classification." arXivpreprint arXiv:1408.5882 (2014).
</br>[4] Nowak, Jakub, Ahmet Taspinar, and Rafał Scherer. "LSTM recurrent neural networks for short text and sentiment classification." In International Conference on Artificial Intelligence and Soft Computing, pp. 553-562. Springer, Cham, 2017.
</br>[5] Zhou, Chunting, Chonglin Sun, Zhiyuan Liu, and Francis Lau. "A C-LSTM neural network for text classification." arXivpreprint arXiv:1511.08630(2015).
</br>[6] Lai, Siwei, LihengXu, Kang Liu, and Jun Zhao. "Recurrent convolutionalneural networks for text classification." In Twenty-ninth AAAI conference on artificial intelligence. 2015.
</br>[7] Devlin, Jacob. "Github-google-research/bert: TensorFlowcode and pre-trained models for BERT.” Github.com. https://github.com/google-research/bert (accessed March 09, 2020).
