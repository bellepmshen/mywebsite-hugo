---
title: Language Translator
description: This is the description of our sample project
date: "2023-03-20T19:47:09+02:00"
jobDate: 2023
work: [ChatGPT, NLP, API Call]
techs: [ChatGPT, NLP, API Call]
# designs: [Photoshop]
thumbnail: loan-credit/chatgpt.jpg
projectUrl: https://github.com/bellepmshen/translator_ChatGPT
# testimonial:
#   name: John Doe
#   role: CEO @Example
#   image: loan-credit/loan-1.jpeg
#   text: Prow scuttle parrel provost Sail ho shrouds spirits boom mizzenmast yardarm. Pinnace holystone mizzenmast quarter crow's nest nipperkin
---

<!-- This would be a description of your sample project. You can add any content you'd like. -->

<font><b><u>Project Goal</b></u></font><br>
The goal of this project was to translate a given PDF file (ex: academic paper) into the language you'd like by using ChatGPT 3.5 via API call.<br> 
Note: When this project was developed, ChatGPT 4 API call was unavailable.<br> 

<font><b><u>Library</b></u></font><br>
Here are the main libraries I used for this projects:
I used pypdfium2 for extracting texts from a PDF file, NLTK for tokenizing sentences, Pandas for saving the API call log mainly, Pickle for saving
the translation results, openai for API call.

<font><b><u>API Call</b></u></font><br>
Since openai API call had request, okens limit and for better translation results, I broke down a document into paragraphs level and here I selected 5 sentences as a paragraph and save it as a txt file. <br>
Then, iterated all the text files and made API calls to ask ChatGPT to translate each paragraph, and saved it as a pickle.
The final output txt file would be a single file with all the translated results.<br>

<font><b><u>Note</b></u></font><br>
I found out with clear prompt messages, ChatGPT would perform better.<br>

For detail codes and graphs, please check the GitHub link above :point_up_2:<br>

<font size = "-3"><i>photo credit: https://www.pcmag.com/news/more-workers-are-using-chatgpt-and-theyre-not-telling-their-bosses</i></font>