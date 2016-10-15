---
layout: post
title: "What makes for a popular movie remake?"
categories: blog
---

Some movie remakes turn into beloved films, while others flop.  The 1983 remake of Scarface starring Al Pacino (original: 1932) has become a classic in its own right.  The 1998 remake of Psycho (original: 1960), on the other hand, was widely panned.  
<img src='{{ site.baseurl }}/images/Scarface.jpg' align='left'/>
<img src='{{ site.baseurl }}/images/Psycho.jpg' align='right'/>

What distinguishes such divergent outcomes?  And can we predict how well a remake will do based on characteristics of the original?  This week I set out to investigate these questions, beginning with a list of approximately 500 pairs of original films and associated remakes I scraped from the web using BeautifulSoup. I then gathered further data on these films through additional web scraping and by using the APIs of different movie databases.  

The films I examined were made between 1902 and 1915.  As a result, financial data was only available for about half of the sample.  I chose instead to try to explain the IMDB user ratings of the remade films.  I initially considered a large number of feature variables.  Those based on the original film included its own IMDB user rating, year, indicators for nineteen distinct genres it may have belonged to, and the log of the total number of film awards and nominations it received.  Additional features based on the remake included the number of years since the original came out, indicators for whether the two films were from the same country and in the same language, the runtime in minutes, and the log of the number of film awards and nominations it received.  

The best model I found for predicting user ratings on out-of-sample data was a linear regression containing 11 features (R-squared = .29). While a random forest model containing the same variables performed very well on in-sample data (R-squared = .87), it was overfit for predicting how future remakes will fare (R-squared = .21).  What is more, with the linear model I was able to draw some interesting conclusions about the kinds of films that potential filmmakers should and should not choose to remake if they want to earn strong viewer ratings.

**Key Takeaways:**

*Dos*  
+ Remake an original with a higher IMDB rating    
+ Choose an older original…    
+ But don’t wait too long to remake it    
+ Make a longer movie    
+ Earn award nominations & wins  
+ Remake a Drama  

*Don'ts*  
+ Remake an original with many nominations & awards    
+ Remake an Adventure film  
+ Remake a Horror film  
+ Remake a Mystery  
+ Remake a Romance  

*Surprisingly irrelevant?*  
+ Whether the remake and original are in the same language  
+ Whether the remake and original are from the same country  

The most important features were the top four under 'Dos.' I thought it was likely that originals with stronger ratings would produce remakes with higher ratings as well: when controlling for other factors about these films, I thought ratings would probably reflect the quality of the story itself. However, it also seemed possible that films with higher ratings might be more difficult to live up to, or that the relationship between ratings of the original and the remake might be non-linear in some other way. I did try several non-linear specifications for this variable, but they did nothing to improve the model (or even made it worse).  

The two variables incorporating time were somewhat interesting, and both were quite important to the model. On the one hand, originals made in earlier years produced more highly rated remakes. On the other hand, a shorter timespan between the original and the remake was also associated with more popular remakes. This obviously isn't all that helpful in terms of practical implications for those who would make films in the future (at least until we have mastered time travel). But a deeper look into the data may be able to yield further insights into the tradeoff between remaking older films and putting out a remake before too much time has passed.

There were a few results that surprised me. I didn't expect film length to have as strong of an impact on ratings as it did.  On the other hand, I did think that films might translate better to audiences who speak the same language or who share a cultural heritage.  For this reason I thought that remakes would probably rate higher if they were in the same language or from the same country as the original.  However, there was no evidence of this whatsoever in these data: even with a fair number of foreign films, these variables were not only statistically insignificant, but their coefficients were very close to zero.  It thus seems unlikely (though not impossible) that a larger sample would yield a substantially different result.          
