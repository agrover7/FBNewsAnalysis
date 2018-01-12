# FBNewsAnalysis

First, if you've somehow got this without me having sent it to you for feedback, please reach out to me with any questions/comments/advice/suggestions at amangrover1000@gmail.com! I had a lot of fun creating this, so I'd love to hear what you think about it. 

Alright, here's the important stuff - 

Attributions:
I learned how to access the Facebook Graph API from an article by Max Woolf. This is a straightforward process that can't really be altered (unless you're changing how the information is stored), and so I utilized some of his code (appropriately as per its license). Most of scrapeStatus, processStatus, getStatusReactions, and all 12 lines of requestStatus are attributable to him (https://github.com/minimaxir/facebook-page-post-scraper/blob/master/get_fb_posts_fb_page.py)




Purpose:
This code (as is) can be used to determine whether there are statistically significant changes in the trend of positivity/negativity and subjectivity in the articles posted on Facebook pages.

It does this by scraping all the data from the posts of Facebook pages of interest between any span of dates given (minimum of one day between the two endpoints). It then extracts all articles URLs from these statuses (and discards statuses that link something other than an article or simply don't have links). Using these extracted URLs, the code will extract the text of the articles linked with the Newspaper module. Then, with the Textblob module, it will perform sentiment analysis (with regards to polarity and subjectivity) on all the articles. Linear regression is performed and statistical data (such as whether linear regression is even appropriate) is published alongside the scatterplots and line of best fit for the time range given.

The code is also easily adaptable for additional tests such as:
  1. Determine whether positive or negative statuses are more likely to be reacted to.
  2. Determine how the subjectivity of a post affects the number of likes it receives. 
  3. Determine whether the positivity/negativity of a post or the subjectivity of how it was written can result in more comments      `   (meaning more engaged users)

Those are just ones that I found fascinating and will likely explore shortly. That said, there are countless more possibilities!

To clarify (a question I have gotten a lot): Polarity vs. Subjectivity 
Polarity measures how positive or negative a sentence it is (on a scale from -1.0 to 1.0), while subjectivity measures how opinion-based a sentence is (on a scale from 0.0 to 1.0). 

A low, positive polarity score means the content is still overall evaluated as positive (but is likely on a negative topic). A negative polarity score of any form means the content is overall negative. 

I've included some sentences below as examples:

A polar sentence that is not subjective: The charity was able to help many people with all the generous donations it recieved.
A completely non-polar statement: The ball is blue.
Subjective sentences will undoubtedly affect polarity (saying "I am happy" or any word of feeling would affect the positivity or negativity based on the emotion).




Directions:
These directions are assuming you are looking to analyze sentiment before and after the election. 

First, make sure you have a Facebook Developer account. If not, it is free and easy to make! Without it, you can't access the API. To create one, go to https://developers.facebook.com/ , click "My Apps", and then click "Create New App". Once you've created an account (or if you already had one), find your app ID and access token. Paste these into the respective areas 

Once you have both scraper.py and main.py ready, open the main.py file. Here, edit any dates in the YYYY-MM-DD form to determine the start and end time points for the scraping. 

Next, edit the list pages_of_interest. This should be a list of strings that contains the "URL Extension" for each page.
For example, CNN's Facebook page is: https://www.facebook.com/cnn
Whatever comes after ".com/", which in this case is "cnn", would be added to the list.

Now, you're ready to hit run. Once you do, you will be prompted to name your file. Follow standard file name procedures 
(ex: no special characters or certain symbols). 

At points throughout the code's running, you may recieve notifications such as "You must download an article first!" or "Article Download Error." These are through the Textblob module, and do not mean the code has failed. Each notification represents an article that was not suitable for download. This is fine, and the code will run regardless.

At some point, the code will stop running and display a blank graph. You can close that (it serves to clear the graph for actual graphing). Then, the Polarity graph will be displayed. Save it if you'd like, and then go to your IDE or command line. Here, type and submit anything, and then the Subjectivity graphs will be displayed. Equations and relevant statistical data (for both subjectivity and polarity information) will be posted as well. 




Important things to note about this code:

1. Once it finishes running, you will find two Excel files on your computer (location depends on your IDE workspace setup). The one with the filename you indicated has all the information used prior to the beginAnalysis method. The other one has the first row numbered 1-20, and can help determine the keys for the list of dicts more easily if the code is being edited for another purpose (each row in the CSV file is one dict from a list of dicts). 
2. There will be occasional gaps in the dates of the posts collected (as in, some dates will be missing). This is a problem with the Facebook Graph API that the company has acknowledged (https://developers.facebook.com/bugs/1838195226492053/).
3. When calculating the degrees of freedom for statistical analysis, the regression equations each have the number of days as the number of data points. The regression lines are based on the scatter plot points which indicate the MEAN polarity/subjectivity for each day.
4. Negative number of days means the dates are before the election. This is fine, and intentional. The regression line is still accurate.
and it makes the data clearer when comparing before/after election results. 
5. The x axis will indicate the number of days before or after the 2016 presidential election unless you change it in the beginAnalysis method to indicate a different starting point as your date.
6. Each status will take 1 second to process, which can help you decide how long the code will take to run. This was done by design because the articles wouldn't finish parsing unless I let the code pause for at least one second, and data points were resultingly lost.
