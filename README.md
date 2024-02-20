# Sentiment-Analysis-of-Financial-Documents
Quantifying the emotions of financial documents has been considered one of the tedious task. But thanks to the two main dictionaries which made our tasks easier, fast, and accurate. We will basically use Loughran-McDonald and harvard iv-4 sentiment dictionary to quantify the tone of our financial text. 
These both dictionaries use lists of words called lexicons. In these lists, the words have been pre-scored for sentiment (e.g., positivity/negativity) as well as the strength of the sentiment. But for us there is no need to be worried about the backend work. We will simply two important pacakages and run the code step by step. 

#STEP 1: First we will install pysentiment2 which is a library for sentiment analysis in dictionary framework.

'''ruby
!pip install pysentiment2
'''

#Step 2: Make a separate directory and save your input files in it. Your input files has to be in .txt formate. And each has a specific name. So, that after finding the tone it will be easy to identify the tone of each document. 
'''ruby
!mkdir input
'''

#Step 3: Import necessary packages 
'''ruby
import os
import pandas as pd
import pysentiment2 as ps
'''

#Step 4: Create an instances for LM or Harvard Dictionary
'''ruby
lm = ps.LM()
'''
Or
'''ruby
hiv4 = ps.HIV4()
'''

Now the rest of the code is same for both of the dictionaries

#Step 5:  Specify the directory containing your text files

'''ruby
directory = 'Your input directory path'
'''

# Initialize a list to store the results
'''ruby
results = []
'''
#Step 6
# The below code will run on the entire directory and quantify the tone.
# Iterate over all files in the directory
'''ruby
for filename in os.listdir(directory):
    if filename.endswith('.txt'):
        # Open the file
        with open(os.path.join(directory, filename), 'r', encoding='cp1252') as f:
            text = f.read()
'''

#Tokenize the text
'''ruby
tokens = lm.tokenize(text)
'''

# Get the sentiment score
'''ruby
score = lm.get_score(tokens)
'''

# Add the filename and score to the results
'''ruby
results.append((filename, score['Positive'], score['Negative'], score['Polarity'], score['Subjectivity']))
'''

#Step 7: Convert the results to a DataFrame
'''ruby
df = pd.DataFrame(results, columns=['Filename', 'Positive', 'Negative', 'Polarity', 'Subjectivity'])
'''

#Step 8: Save the DataFrame to an Excel file
df.to_excel('your output file.xlsx', index=False)


If you have just one single file, simply give the directoty of that single file. If you have just a paragraph, you can simply modify the code like below.

'''ruby
import pandas as pd
import pysentiment2 as ps
'''

# Create an instance of the LM dictionary
'''ruby
lm = ps.LM()
def get_sentiment_analysis(text):
'''

# Tokenize the text
'''ruby
tokens = lm.tokenize(text)
'''

# Get the sentiment score
 '''ruby
 score = lm.get_score(tokens)
'''

# Return the results

'''ruby
return score['Positive'], score['Negative'], score['Polarity'], score['Subjectivity']
'''

# Example paragraph text
'''ruby
paragraph_text = "This is an example paragraph. It has both positive and negative sentiments."
'''
# Get sentiment analysis results for the paragraph

'''ruby
positive, negative, polarity, subjectivity = get_sentiment_analysis(paragraph_text)
'''
# Display the results
'''ruby
print("Positive: {}".format(positive))
print("Negative: {}".format(negative))
print("Polarity: {}".format(polarity))
print("Subjectivity: {}".format(subjectivity))
'''



