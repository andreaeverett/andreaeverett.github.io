---
layout: post
title: "What makes for a popular movie remake?"
categories: blog
---

Some movie remakes turn into beloved films, while others flop.  The 1983 remake of Scarface starring Al Pacino (original: 1932) has become a classic in its own right.  The 1998 remake of Psycho (original: 1960), on the other hand, was widely panned.  

<img src='{{ site.baseurl }}/images/Scarface.jpg' style="width:250px;height:400px;"/>
<img src='{{ site.baseurl }}/images/Psycho.jpg' style="width:250px;height:400px;"/>

What distinguishes such divergent outcomes?  In particular, which characteristics of an original film can help us predict how well a remake will do?  I set out to investigate these questions, beginning with a list of approximately 500 pairs of original films and associated remakes I scraped from the web using BeautifulSoup. I then gathered further data on these films through additional web scraping and by using the APIs of different movie databases.  

The films I examined were made between 1902 and 2015.  For this reason, financial data was only available for about half the sample.  I chose instead to focus on the IMDB user ratings of the remade films.  I initially considered a large number of feature variables, with an emphasis on the original film.  These included the original's IMDB user rating, its release year, indicators for nineteen distinct genres it may have belonged to, and the log of the total number of film awards and nominations it received.  Additional features based on the remake included the number of years since the original came out, indicators for whether the two films were from the same country and in the same language, and the remake's runtime in minutes.  

The best model I found for predicting user ratings on out-of-sample data was a linear regression containing 11 features (R-squared = .29). For comparison, a random forest model containing the same variables achieved an out-of-sample R-squared of .21.  What is more, the linear model highlights some interesting conclusions about the kinds of films that potential filmmakers should and should not choose to remake if they want to earn strong viewer ratings.

**Key Takeaways:**

*Dos*  
* Remake an original with a higher IMDB rating    
* Choose an older original…    
* Don’t wait too long to remake it, except for decades-old classics    
* Make a longer movie      
* Remake a Drama  

*Don'ts*  
* Remake an original with many nominations & awards    
* Remake an Adventure film  
* Remake a Horror film  
* Remake a Mystery  
* Remake a Romance  

*Surprisingly irrelevant*  
* Whether the remake and original are in the same language  
* Whether the remake and original are from the same country  

The most important features were the top four under 'Dos.' I thought it was likely that originals with stronger ratings would produce remakes with higher ratings as well: when controlling for other factors about these films, I thought ratings would probably reflect the quality of the story itself. However, it also seemed possible that films with higher ratings might be more difficult to live up to, or that the relationship between ratings of the original and the remake might be non-linear in some other way. I did try several non-linear specifications for this variable, but they did nothing to improve the model (or made it worse). The graph below shows the relationship between the IMDB ratings of the original and the remake.

<img src='{{ site.baseurl }}/images/ratings_orig_vs_remake.png' style="width:450px;height:300px;"/>

The variables incorporating time were somewhat interesting, and quite influential. The models included both a linear and a quadratic term for the number of years since the release of the original.  Overall, the number of years since the original had little apparent effect on the remake's ratings during the first decade.  Beyond this, additional years tended to depress the ratings of the remake, but only up until about 30 years had passed. After even more time, remake ratings start to tick up again, indicating that remakes of older classics tend to earn higher marks with viewers. Confirming this interpretation, originals made in earlier years also generally produced more highly rated remakes, as seen in this figure:

 <img src='{{ site.baseurl }}/images/year_orig_vs_remake_rating.png' style="width:450px;height:300px;"/>

There were a few results that surprised me. I didn't expect film length to have as strong of an impact on ratings as it did.  On the other hand, I did think that films might translate better to audiences who speak the same language or who share a similar cultural heritage.  For this reason I thought that remakes would probably rate higher if they were in the same language or from the same country as the original.  However, there was no evidence of this whatsoever in these data: even with a fair number of foreign films, these variables were not only statistically insignificant, but their coefficients were very close to zero.  It thus seems unlikely (though not impossible) that a larger sample would yield a substantially different result.          
