# In no particular order.

-**Building a better neighborhood:**
- *Features:* strave heat map and crime data base joined on geodata. [Strava](https://www.strava.com/heatmap).
- *Target:* crime, housing price, some social/econ variable
- *Resources:* ATX crime database (1 gb json) w/ geo metadata, python geolibrary.
- *Obstacles:* It will be tricky to get the data from the heat map. It's built on/in/with mapbox [Mapbox](https://www.mapbox.com/about/maps/).

~~-**The Sweet Spot** 
- *Features:* gun laws, gun sales, gun registration, gun ownership
~~- *Target:* gun violence
- *Resources:* a small csv. *Could I build a decision tree w/ state gun laws?* *Could I figure out which laws are most effective?*
~~- *Obstacles:* the small database is kinda weak. I also don't really like this one because I don't think more guns helps lower gun violence at all. but I could still build a model that includes it. Another idea is to ONLY use gun laws, categoriezed by similiarity of function, to predict the most effective combination of laws to reduce gun violence.

-**Bias detection** 
- *Features:* NLP of articles posted on twitter and facebook.  I want to focus on certain type of words that tend to be highly biased, for example "absolutes"  (i.e. 'totally', 'finally', 'all', 'every') for language that is more "nuanced" (i.e. idk. not those words?). OR I could pull all articles from a newspapers and analyze articles from op-ed, editorial, and new desks.
- *Target1:* predicitng if an article is "fake" based on words used
- *Target2:* measure the bias of an article based on the words with some threshold of bias vs. opinion. it to NLP of podcasts and youtube channels.
- *Target3:* model that correctly guesses whether an article is from an op-ed section or not. These are all a similar idea.
- *Resources:* Twitter or Facebook API w/ articles flagged as "fake". NYTimes op-ed vs news desk.
- *Obstacles:* It feels like a big project and I'm not sure if it's in my skill set. 

-**Beating the Odds** 
- *Features:* educational level, educaitonal field, technical experience, age, race, gender, campus location, remote vs local, staff.
- *Target:* Will a student get a job in 6 months?
- *Resources:* Galvanize DSI Entry survey data. webscrapping the linkedin galvanize alum page.
- *Obstacles:* Can I have that data? All the data I've seen is already aggregated.

-**Free BI analysis** 
- *Features:* some data from a small business
- *Target:* any BI analysis they don't have the budget to explore
- *Resources:* I'd have to find a business owner or BI team leader. I know a few, but haven't initiated.
- *Obstacles:* Can I do this? I know Josh has don't that? Could I offer that for free? Is that weird?

-**Nate Silver idea**
- *Features:* historical polling and election data for incumbant presidents
- *Target:* what is the advantage of being the incumbant in presidential elections. How much does an incumbant beat his odds?
- *Resources:* historical polling and election date
- *Obstacles:* I'm interested in the election/polling data that is available on 538. I wanted to do something about voter supressiong and comparting polling sentament of communities vs. how they vote. Is there a similar trend based on communities that historically experience voter supression? I'm not sure how legit the data would be for how communities actually voted. that may be based on exit polling which may not be iid of polling data like election data might be.

-**Covid**



