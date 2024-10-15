# Dr-A-Clone


---

# Fine-Tuning LLaMA 3.2 for Dr. Patricia A. Alexander's Writing Style

## Project Overview

This project focuses on training and fine-tuning a LLaMA 3.2 model to generate text that mimics the writing style of Dr. Patricia A. Alexander, a renowned Educational Psychologist. By using a dataset constructed from her academic papers and articles, we aim to develop a model capable of generating text reflective of her scholarly tone, structure, and style.

## Motivation

Understanding and replicating an academic writing style can assist in a variety of research and educational applications. The goal of this project is to create a model that helps in generating coherent, scholarly text similar to Dr. Alexander’s, which can be useful for academic assistance, tutoring, and further research.

---

## Fine-Tuning Dataset Construction

### Step-by-Step Breakdown

1. **Find the Correct LLaMA Training Data Template**
   - We first identify and follow the official LLaMA training data template to ensure compatibility with the LLaMA 3.2 architecture.
   
2. **Collecting Dr. Patricia A. Alexander's Papers/Articles**
   - We gather as many of Dr. Alexander’s works as possible through sources like Google Scholar, ResearchGate, and institutional databases.
   - **Challenges**: 
     - Many papers are available only in PDF format, requiring efficient conversion.
     - Extracted data must be cleaned and standardized for model training.

3. **Script for Sentence Separation**
   - A Python script is written to split each paper into individual sentences using the `.split()` function. This helps break down the data into smaller training segments.

4. **Prompt Construction**
   - We construct relevant prompts for training. Each sentence in the dataset will have an associated prompt that reflects Dr. Alexander’s academic focus.
   - Example prompt stem:  
     `"You are Dr. A(I) Bot. You write like the renowned Educational Psychologist, Dr. Patricia A(I) Alexander. Write a sentence about [X], including [Y]."`

5. **Identifying Sentence Main Points and Subtopics**
   - A script using the LLaMA 3B model helps identify the main point of each sentence (`[X]`) and any subtopics (`[Y]`).
   - This information is crucial for prompt generation and for training the model to mimic complex academic writing structures.

6. **Integrating Data into Training Script**
   - Once sentences and prompts are prepared, we integrate the data into the LLaMA training script following the model’s requirements for prompt-based fine-tuning.

7. **System Prompt Development**
   - A system prompt is written to guide the LLaMA model during the generation process. This prompt tells the model to write as if it were Dr. Alexander, ensuring style consistency.

8. **Final Cleaning**
   - We remove any extra spaces, formatting errors, and perform a final cleaning to ensure the dataset is optimized for training.
   
---

## Goal

Our aim is to construct a fine-tuning dataset containing **10,000 unique sentences** written by Dr. Patricia A. Alexander or generated in her style. These sentences will be used to fine-tune LLaMA 3.2 to accurately replicate Dr. Alexander's writing across various topics and contexts.

---

## Tools & Technologies

- **Python** for data processing and prompt generation scripts.
- **LLaMA 3.2** for model fine-tuning.
- **pandas** for data manipulation and cleaning.
- **PDF Conversion Tools** (e.g., `PyPDF2`, `pdfminer`) for extracting text from PDF documents.
- **Regular Expressions** for data cleaning and standardization.

---

## Challenges

- **PDF Conversion**: Many academic papers are only available in PDF format, which presents challenges in text extraction and data consistency.
- **Data Cleaning**: Ensuring that extracted text is correctly cleaned and standardized before fine-tuning.
- **Sentence Tokenization**: Properly splitting long academic texts into meaningful sentences for better model training.
- **Fine tuning**:
- 
---

The notebook contains several important functions and scripts that are directly relevant to the data extraction and processing aspects of your project. Here’s how these parts can be integrated into the README to provide more clarity on the dataset construction:

---

### Fine-Tuning Dataset Construction

The dataset preparation for this project is a critical step in fine-tuning the LLaMA model. Here's a detailed breakdown of the process, with specific references to the scripts used:

1. **PDF Extraction and Text Processing**
   - We collect Dr. Patricia A. Alexander’s papers, some of which are in PDF format. Using `PdfReader`, we extract the text from the relevant pages of these PDFs.
   - A custom function `fix_text()` is applied to clean and standardize the text by removing excess spaces, fixing letter spacing issues, and cleaning punctuation.

   ```python
   from pypdf import PdfReader

   # Load PDF and extract pages
   reader = PdfReader(f'./PDFS/{title}.pdf')
   raw_text = page.extract_text()
   fixed_text = fix_text(raw_text)
   ```

2. **Sentence Separation**
   - We split the cleaned text into individual sentences using the `.split()` method. Only sentences with more than three words are retained for the dataset, as this improves the quality of training data.

   ```python
   split_sentences = fixed_text.split(". ")
   filtered_sentences = [sentence for sentence in split_sentences if len(sentence.split()) > 3]
   ```

3. **POS Tagging and Sentence Metrics**
   - We use the `spaCy` library to perform Part-of-Speech (POS) tagging for each sentence. Additional metrics such as sentence length, token length (number of words), and whether the sentence is a question are also calculated.

   ```python
   for sentence in sentences:
       doc = nlp(sentence)
       pos_tags = [token.pos_ for token in doc]
       sentence_length = len(sentence)
       token_length = len(sentence.split())
       is_question = "?" in sentence
   ```

4. **DataFrame Construction**
   - The processed data (sentence, length metrics, POS tags) is stored in a Pandas DataFrame for easy manipulation and further use in the training process. The DataFrame is then saved as a CSV file for use in model fine-tuning.

   ```python
   df_data.append({
       "Sentence": sentence,
       "Sentence Length": sentence_length,
       "Token Length": token_length,
       "Is Question": is_question,
       "POS Tags": pos_tags
   })
   df = pd.DataFrame(df_data)
   df.to_csv(output_file_path, index=False)
   ```

5. **Dataset Overview**
   - We calculate summary statistics such as average sentence length and token length. The dataset is stored as CSV files, and an aggregation script iterates over these files to count the total number of sentences.

   ```python
   total_rows = 0
   for filename in os.listdir(csv_directory):
       df = pd.read_csv(file_path)
       num_rows = len(df)
       total_rows += num_rows
   ```

---


## License

This project is licensed under the MIT License.

---

