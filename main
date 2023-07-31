from wordcloud import WordCloud
from nltk import word_tokenize
from nltk.stem import WordNetLemmatizer
from nltk.corpus import stopwords

import matplotlib.pyplot as plt
from PIL import Image

import re
import random
import numpy as np
import pandas as pd


try:
    file = input("Address of file :")
    text = open(file, "r", encoding="utf-8")
    text_name = str(file)
    text_name.split("\\")[-1]
    great_expectations = text.read()

    img_add = str(input("Address of Image :"))
    img_name = img_add.split("\\")[-1]

    color = input("Enter significant colour :")

    word_cloud_text = great_expectations.lower()
    word_cloud_text = re.sub("[^a-zA-Z0-9]", " ", word_cloud_text)

    #Cleaning text
    tokens = word_tokenize(word_cloud_text)
    tokens = (word for word in tokens if word not in stopwords.words("english"))
    tokens = (word for word in tokens if len(word)>=3)

    #cleaning up text off stopwords
    stopwords_wc = set(stopwords.words("english"))
    alphabets = "([A-za-z])"
    prefixes = "(Mr|St|Mrs|Ms|Dr)[.]"
    suffixes = "(Inc|Ltd|Jr|Sr|Co)"
    starters = "(Mr|Mrs|Ms|Dr|Prof|Capt|Cpt|Lt|He\s|She\s|It\s|They\s|Their\s|Our\s|We\s|But\s|However\s|That\s|This\s|Wherever)"
    acronyms = "([A-z][.][A-z][.](?:[A-z][.])?)"
    digits = "([0-9])"

    text = " " + great_expectations + " "
    text = text.replace("\n","")
    text = re.sub(digits + "[.]" + digits, "", text)
    text = re.sub("\s" + alphabets + "[.] ","", text)
    text = re.sub (acronyms+" "+starters, "", text)
    text = re.sub (alphabets + "[.]" + alphabets + "[.]" + alphabets + "[.]","", text)
    text = re.sub(alphabets + "[.]" + alphabets + "[.]","", text)
    text = re.sub(" "+suffixes+"[.] "+starters,"", text)
    text = re.sub(" "+suffixes+"[.]","", text)
    text = re.sub (" "+ alphabets + "[.]","", text)
    if "\"" in text: text = text.replace(".\"", "")
    if "\"" in text: text = text.replace(".\"", "")
    if "!" in text: text = text.replace("!\"", "")
    if "?" in text: text = text.replace("2\"", "")
    text = text.replace(".", "")
    text = text.replace("?", "")
    text.replace("!", "")
    text.replace(".", "")

    #Creating sentence Dataframe
    sentences = text.split("\n")
    sentences = [s.strip() for s in sentences]
    sentences = pd.DataFrame(sentences)
    sentences.columns = ['sentence']

    sentences = sentences.reset_index(drop = True)
    if img_add == '':
        mask = None
    else:
        mask = np.array(Image.open(img_add))
        
    #Creating WordCloud
    def gray_color_func(word,  font_size, position, orientation, **kwargs):
        return "hsl(0, 0%%, %d%%)" % random.randint(60, 100)

    print(f"WordCloud:\nColour:{color}\nFile_Name:{text_name}\nImage_Name:{img_name}")
    wordcloud = WordCloud(background_color= color, mask = mask, color_func=gray_color_func , max_words=100, stopwords = stopwords_wc, random_state=1).generate(word_cloud_text)
    plt.figure(figsize=(8, 6))
    plt.imshow(wordcloud)
    plt.axis("off")
    plt.show()
except:
    print("Error Occured. Check if file paths are misspelled. ")
