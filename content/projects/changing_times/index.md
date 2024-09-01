+++
title = 'Changing Times - Tracking Edits to Online News Articles'
date = 2024-05-31
draft = false
+++
The Internet has brought dramatic changes to the media landscape, allowing newspapers to reach viewers more easily and on a greater scale than ever before through digital publication. One capability that this digital revolution has brought to news publishers is the ability to edit articles at any time. While this has the benefit of allowing publishers to provide corrections and updates to articles more easily, it can also lead to people who read the article at different times getting a very different picture of events, which may contribute to a decreasing level of trust in news publishers. For more background on this subject, you can read the research paper that motivated this project [here](https://www.securitee.org/files/changing_times_oakland24.pdf).

I worked as a research assistant to a project by the Stony Brook Computer Science department aiming to track edits to online news articles and to provide an application allowing users to view these changes. We built a system to track new articles released by prominent news publishers and periodically revisit them to check for any edits. The main page of the application shows the articles that have been most recently edited.
{{<figure src="images/article_selection.png" caption="The article selection screen of the application. It shows two articles from Yahoo News and one article from the New York Times that have been recently edited. A menu at the top left allows the user to filter for a specific news publisher.">}}

Selecting an article allows the user to view the edits that have been made to the article. We modeled our display after how edits to Wikipedia articles are displayed in order to make the changed sections easily identifiable. 
{{<figure src="images/diff_display.png" caption="Paragraphs that have been edited are highlighted in red for the old version of the article and highlighted in green for the new version. The specific words that have been changed within each paragraph are further highlighted.">}}

We also used natural language models based on RoBERTa to determine if the edits affected the sentiment of the paragraph, as well as if there is entailment[^1] between the original and modified versions of the paragraph. The scores for sentiment and entailment can be viewed by hovering over each modified paragraph. If the sentiment of a paragraph changes with an edit, or the modified paragraph does not entail the original, then it is possible that a reader who views the original version of an article gets a different message from a reader who views the modified version. A spelling or grammar fix is unlikely to affect the meaning of an article, but a correction, update, or other change may do so. As a result, it may be best for news publishers to acknowledge such edits for the sake of transparency.

Hopefully, this research can help news readers learn more about what they read and start a discussion on creating a more transparent media landscape.

[^1]: Entailment is a measure of whether one section of text logically "follows" another. If the modified version of a paragraph does not "follow" the original, it indicates that the overall meaning of the paragraph has changed.