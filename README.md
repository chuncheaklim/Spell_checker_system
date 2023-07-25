# Spell checker system

My friends, Justin Ng and Wengie Wong, and I collaborated on a university NLP project to develop a spell checker system. This system aims to identify and rectify two types of errors, namely non-word errors and real word errors, found in GUI input texts.

Non-word errors refer to misspelled words that do not exist in the dictionary, while real word errors occur when a word is misspelled but still exists in the dictionary, resulting in altered contextual information. As a result, our system was designed to correct both types of errors in the input text.

The primary focus of this system is to address spelling errors related to astrological terms. To achieve this, we utilized a book titled "The Only Astrology Book You'll Ever Need" as the corpus for our system. We preprocessed the corpus by removing non-English words, punctuation, URLs, and digits. Then, we created text files containing unique tokens from the corpus and calculated bigram probabilities, which were later exported for use in the spell check system.

To detect non-word errors, we check if the input text contains misspelled words that are not present in the corpus. However, due to the limited number of unique tokens in the corpus, we cross-reference with words from the English dictionary to avoid flagging valid English words as non-word errors simply because they are absent from the corpus. Once non-word errors are detected, we use the Damerau Levenshtein edit distance to generate potential word candidates to replace the incorrect words. The Damerau Levenshtein distance accounts for single-character insertions, deletions, substitutions, and transpositions of adjacent characters.

To refine the candidate words generated for non-word errors, we use an edit distance of 1 for words with a length less than 7, and an edit distance of 2 for longer words. This decision is based on the assumption that spelling mistakes are generally fewer in shorter words compared to longer words. Additionally, to rank the candidates, we calculate the probability of each candidate appearing before the misspelled word using bigram probabilities. This allows us to prioritize the candidate with the highest probability, ranking it at the top of the list.

Meanwhile, concerning real word errors, a word will be marked if the product of the bigram probability for the word with the preceding and succeeding words is below a specified probability threshold (0.00001). Apart from using the Damerau Levenshtein distance to suggest candidates based on the same assumption, we also employ the "eng_to_ipa" function to generate possible candidates with the same pronunciation as the erroneous words. This ensures that misspelled words existing in the dictionary but pronounced the same, such as "two" and "too," are properly handled.

Regarding the GUI design, we opted for the tkinter library to streamline the creation and layout of the GUI. Our GUI consists of a text box for input texts, which may contain words with errors, a candidate listbox to display generated candidates, and a dictionary listbox to exhibit the unique tokens in the corpus.

Upon pasting their desired input text, the user can click the "Check" button to identify words with errors. Non-word errors are highlighted in red, while real word errors are highlighted in yellow. By clicking on a highlighted word, the user can generate a list of candidates displayed in the candidate listbox. Once the candidates are available, the user can select the correct candidate to replace the erroneous word.

Additionally, if the user wishes to check whether a specific word exists in the corpus, they can type the word in the textbox below the dictionary listbox and press the "Search" button to find it.

In future, we would like to consider Parts of Speech (POS) tagging to categorize words into nouns, verbs, adjectives and adverbs, based on the contextual information about the word in a given text. By considering the POS tags of words, the system can suggest corrections that are align with the grammatical structure of the sentence. 

Next, information retrieval could also be used to retrieve relevant information from various sources such as dictionaries, corpora, or linguistic databases to enable the system to expand its knowledge base and improve its accuracy in suggesting candidate words. GloVe and FastText word embedding models could also be used to capture semantic meanings of words for candidate generation and ranking, by incorporating the similarity between words based on their distances in the semantic vector space.




