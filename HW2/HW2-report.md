# HW 2: Data Cleaning - CS 625, Fall 2023

Jenah Parman\
Due: September 20, 2023

## Introduction

This report provides an overview of the steps I took to clean the PetNames.tsv dataset for analysis. The survey was iniated on July 21, 2019 on Twitter by Dr. Jen Golbeck; it collected information about people's pets, including the type of pet, the pet's full name (excluding the owner's last name), the pet's everyday name, age, and breed. Interestingly, the main goal of gathering this data was to create a messy dataset intentionally for practicing data cleaning. In the following sections are the steps I took to accomplish this goal.

## I. Data Cleaning Process

### Dealing with Multi-Valued Cells

I started by using *Text facet* on the pet type column to see all the unique values and their frequencies.

Upon inspecting the different unique values, I noticed a row with multiple pets in one. I decided to find out if there were more of these instances and handle them before continuing.

To do this, I added a *Text filter* to the pet type column and searched for any entries that contained ",", ";", " and ", or "&". I flagged the ones that seemed like they represented more than one pet. Then, I considered the possibility of respondents who have more than one of the same kind of pet. I used a *Text filter* on the pet name column, searched for ",", ";", " and ", or "&" again, and flagged any conspicuous rows. I ended up finding four entries that represented more than one pet.

<p align="center">
<img src="/HW2/Resources/screenshot45.png" width="1000" alt="multi-valued cells">
</p>

To fix this, I seperated each pet attribute in the columns with a ";". Then, I used the *Split multi-valued cells* feature with the *Seperator* set to ";", giving each pet its own row.

<p align="center">
<img src="/HW2/Resources/screenshot50.png" width="1000" alt="multi-valued cells split incomplete">
</p>

I could not get the pet kind column to agree with the newly created rows for the different pets, so I had to manually enter in this column.

<p align="center">
<img src="/HW2/Resources/screenshot51.png" width="1000" alt="multi-valued cells split complete">
</p>

I assumed that this disagreement of populating existing rows had something to do with the pet kind column being tied to the ID number column. It seemed like the newly created rows were almost "sub-rows" of the originals, i.e., they did not have their own ID number. I thought that this seemed OK at first, but then I realized that this was affecting the overall count of items. In an attempt to mitigate this situation, I exported the file and then re-uploaded it to OpenRefine. This ended up giving each row its own ID number and upped the count to match the new items. Problem solved.

<p align="center">
<img src="/HW2/Resources/screenshot53.png" width="1000" alt="new rows with ID numbers">
</p>

In retrospect, I likely could have created a new column between the ID number and the pet kind column, performed the split on the pet kind column, and then deleted the new column instead of manually fixing the values.

### Cleaning the "What Kind of Pet" Column

I began the data cleaning process by first reviewing the analysis questions. The first question pertained to the different kinds of pets, so this is where I decided to start cleaning.

I applied a *Text facet* on the pet type column. 

<p align="center">
<img src="/HW2/Resources/screenshot0.png" width="1000" alt="text faceting pet kind">
</p>
<br/>

I then used the *Cluster* feature to join any rows that convey the same information.

<p align="center">
<img src="/HW2/Resources/screenshot63.png" width="1000" alt="clustering pet kind">
</p>
<br/>

I was able to join several instances of misspellings or variations or  "Dog", "Cat", "Hamster", "Guinea Pig", etc.. I tried all of the different *Keying functions*, and was able to go from 83 unique values to 53 on the first round of clustering.

After inspecting the remaining unique values in the *Text facet*, I manually removed any rows that stuck out to me as "*definitely not a pet*", e.g., "Card board poster", "Robot", "Roomba", "Virus", and "Server".

I also handled things that stuck out to me as "*definitely not a pet*" but probably a typo:

<p float="left">
<img src="/HW2/Resources/screenshot55.png" width="499" alt="cat pet typo">
<img src="/HW2/Resources/screenshot56.png" width="499" alt="dog pet typo">
</p>
<br/>

When sorting the *Text facet* by count, I noticed a lot of respondents simply typed "Other", probably because of the nature of the question-- "What kind of pet is this (Dog, Cat, Bird, Other)". Respondents may have assumed that if it wasn't one of the first three mentioned to enter "Other". I wanted to see if the pet breed column gave any dead giveaways as to what these animals were, and it did! I was able to figure out almost all of them from information provided by the breed column, so I manually entered these.

<p align="center">
<img src="/HW2/Resources/screenshot57.png" width="1000" alt="other facet before">
</p>
<p align="center">
<img src="/HW2/Resources/screenshot58.png" width="1000" alt="other facet after">
</p>
<br/>

I missed the "Winter white hamster" in this screenshot, but I ended up fixing this later.

I also noticed that some respondents would enter their pet kind but also include the word "other" in their response. I used a GREL expression: `value.replace("Other","").replace("other","")` to get rid of the "other" word. However, this still left some extraneous puntuation for some entries.

Then, I used a *Text filter* to find any instances of "kitty", "kitten", "kitty cat", etc.. I simply searched for "kit", and then transformed the selected cells to say "Cat".

<p align="center">
<img src="/HW2/Resources/screenshot60.png" width="1000" alt="kit to cat">
</p>

Then, I did for "puppy", "puppy dog", etc. and changed those to "Dog".  

After narrowing the unique values down to 40, I used *Cluster* again. This helped get ride of the leftover punctuation from the entries containing "Other".

<p align="center">
<img src="/HW2/Resources/screenshot61.png" width="1000" alt="clustering pet kind again">
</p>

A few entries listed the pet name as it's kind. I was able to figure out that these were all dogs by looking at the breed. I used a *Transform* to make these all say "Dog", while ensuring that the pet name was in the right place.

<p align="center">
<img src="/HW2/Resources/screenshot1.png" width="1000" alt="dog names to dog">
</p>

After doing some research, I found out that geckos are lizards[^1] and all tortoises are turtles (but not all turtles are tortoises.)[^2] I wanted to narrow my list of unique values down more, so I decided to consolidate these by using a *Text filter*, searching for "gecko" and "tortoise", and using a cell *Transform* to change any instances to "Lizard" and "Turtle". I made sure to indicate the more specific animal type in the pet breed column before making the change. 

I repeated the same steps for any "goldfish" or "betta fish", simply changing these to "Fish" but mentioning the specificities in the breed column. I had a hard time deciding whether I should consolidate the two chicken entries with the "Bird" category, but I ended up doing so. I noticed that the list had only two different kinds of insects (Bees and Spiney Leaf Insect), so I joined these under one "Insect" category.

<p align="center">
<img src="/HW2/Resources/screenshot5.png" width="1000" alt="consolidating pet kinds">
</p>

I finally narrowed the list down to something I was satisfied with, containing unique values that I thought weren't too specific or too broad.

<p align="center">
<img src="/HW2/Resources/screenshot80.png" width="300" alt="final list of pet kinds">
</p>

### Cleaning the "Pet's Breed" Column

Two of the questions ask about the pet's breed, more specifically, cat and dog breeds. This is where I decided to clean next.

#### Cat Breeds

I used a *Text facet* on the pet kind column and selected "Cats" to start working with just the cat breeds. I then applied another *Text facet* on the pet breed column.

Starting with 143 unique values, I decided to *Cluster* first, trying all of the *Keying functions*. 

There were many variations of "Domestic [short,medium, or long]-hair", so I joined all of these under one spelling and format. I did the same for any "[Place of Origin] [short,medium, or long]-hair"s.

<p align="center">
<img src="/HW2/Resources/screenshot6.png" width="1000" alt="cat breed cluster">
</p>

I had to do a lot of reading on cat breeds in comparison to cat coat and marking terminology. I also found it challenging to figure out how to classify the cats. *Should I only include breeds recognized by the CFA (Cat Fanciers' Association)? How should I handle mixed-breed cats? What even is a Domestic short-hair?*

I decided that I would remove any values in the pet breed column that solely listed a cat's coat color/marking name (e.g., Tabby, Calico, Tuxedo, Black, etc.). However, if it contained a cat coat color/marking AND "[short,medium, or long]-hair", then I would change these to "Domestic [short,medium, or long]-hair". I decided that if it wasn't a CFA recognized breed, but it did contain hair length, then it was probably a "Domestic". It seems like "**Domestic** [short,medium, or long]-hair" is like the "mutt" of cats, having an unknown lineage. I also found out that Domestic short-hairs are called "Moggies" in England, so I changed every instance of "Moggy" to "Domestic short-hair".[^3] 

I removed the values that were only coat color/marking name by applying a *Text filter* and searching for the color/marking name, while flagging any values that contained additional info hinting at a breed.

<p align="center">
<img src="/HW2/Resources/screenshot12.png" width="1000" alt="filtering tuxedo cat">
</p>

Then, I applied a *Flag facet*, filtered by *False*, and performed a cell *Transform*, just changing these values to an empty string.

<p align="center">
<img src="/HW2/Resources/screenshot13.png" width="1000" alt="replacing with empty string">
</p>

I then filtered by *True*, i.e., the flagged values, and performed a cell *transform* to make these say their breed.

<p align="center">
<img src="/HW2/Resources/screenshot14.png" width="1000" alt="changing values to cat breed">
</p>

I repeated these steps for remaining cat color coats/markings. For any "Part [cat breed]" or "[cat breed] Mix", I put under one category called "Mix". Lynx Point Siamese was a tricky one because it seems like it would be a type of Siamese. After doing some research, it seems that it is classified in many different ways, but they are bred from a Siamese and a tabby cat, so I just placed this in the "Mix" category.

These steps got my list of cat breeds down to something manageable with true unique values.

<p align="center">
<img src="/HW2/Resources/screenshot17.png" width="300" alt="cat breed cleaned list">
</p>

#### Dog Breeds

I followed a similar technique for cleaning up the list of dog breeds. By first applying a *Text Facet* for both pet kind (dog selected) and pet breed, I was able to narrow the messy list down significantly by using *Cluster* and trying all *keying functions*.

<p align="center">
<img src="/HW2/Resources/screenshot33.png" width="1000" alt="clustering dog breeds">
</p>

I noticed there were several mixed-breed dogs, so similarly to what I did for cat breeds, I created a "Mix" category. I then added a *Text filter* and searched for any instance of the word "mix" and changed these values using a cell *Transform* to say "Mix". I also did the same for any values that contained "mutt" or "cross".

<p align="center">
<img src="/HW2/Resources/screenshot34.png" width="1000" alt="mix category">
</p>

I cross-referenced the AKC (American Kennel Club) and UKC (United Kennel Club) list of dog breeds with my list of unique values, and for any that weren't listed and seemed like a mixed-breed (e.g., Goldendoodle, Yorkiepoo, Labradoodle, etc.), I performed a cell *Transform* to make these "Mix".

I narrowed the list of unique values down by maually tweaking a few things to line up with the AKC and UKC lists, and then clustering again. I repeated this a few times until I got a list that I was happy with.

### Cleaning the "Pet's Age" Column

There are two questions regarding pet's age, so I started working with this column next. I noticed these questions had involved sorting the ages by their numberical value, so I decided to try to get this column to exclusively numbers.

My thought process went like this: It appeared that most of the pets were over a year old, and when discussing age, humans typically refer to years unless talking about a newborn. Anything less than 12 months doesn't seem like a significant amount of time, so I decided to consider anything younger than one year old as 0. I aimed to simplify this to whole numbers (integers). In human age, we usually don't say, "I'm 23 years and 10 months old"; we simply say, "I'm 23." So, I rounded down (floored) any age that was expressed as a float or fraction. Additionally, a significant number of pets didn't specify their age in months or fractions of a year. To ensure consistency and impartiality, I opted to convert all ages into integers rounded down. Also, if there was an entry that mentioned more than one age or a range or ages, I went with the lowest value. For any deceased pet's, I used an empty string.

I started by applying a *Text filter* on the pet age column. I searched for "y", hoping to gather anyone who may have listed any variation of the word "years" or "years old". I flagged any records that had a "y" in it, but was not referring to years. Then, I filtered by values NOT flagged. I then used a GREL expression: `value.replace("years","").replace("year","").replace("yrs","").replace("y","").replace("YO","").replace("yo","")` to try to get rid of any text.

<p align="center">
<img src="/HW2/Resources/screenshot18.png" width="1000" alt="GREL expression to remove years text">
</p>

I repeated these steps for months, but this time the goal was to change these to values to "0". I first filtered for "m", flagging any values that either greater than 12 months or weren't related.

<p align="center">
<img src="/HW2/Resources/screenshot19.png" width="1000" alt="pets age filtered">
</p>

I filtered by NOT flagged values, and used a cell *Transform* to change these values to "0".

<p align="center">
<img src="/HW2/Resources/screenshot20.png" width="1000" alt="pets age filtered">
</p>

<p align="center">
<img src="/HW2/Resources/screenshot21.png" width="1000" alt="transforming cells based on age">
</p>

Then, I filtered by flagged values, and changed these to "1".

<p align="center">
<img src="/HW2/Resources/screenshot22.png" width="1000" alt="GREL pets filtered by age">
</p>
<p align="center">
<img src="/HW2/Resources/screenshot23.png" width="1000" alt="transforming cells based on age">
</p>

I repeated these steps for weeks, using "w" to filter.

<p align="center">
<img src="/HW2/Resources/screenshot24.png" width="1000" alt="transforming cells based on age">
</p>

Now I was left with 66 out of 1783 non-numeric values. I performed a GREL expression in an attempt to remove any extraneous text.

<p align="center">
<img src="/HW2/Resources/screenshot25.png" width="1000" alt="remaining rows">
</p>

<p align="center">
<img src="/HW2/Resources/screenshot26.png" width="1000" alt="GREL expression to remove text">
</p>

This fixed most of them, but I ended up having to go in and manually edit a few.

<p align="center">
<img src="/HW2/Resources/screenshot28.png" width="1000" alt="remaining rows">
</p>

<p align="center">
<img src="/HW2/Resources/screenshot29.png" width="1000" alt="manually edited rows">
</p>

Finally, I transformed the age column into only numbers with no text.

<p align="center">
<img src="/HW2/Resources/screenshot30.png" width="1000" alt="numeric values in age column">
</p>

I then used a GREL expression to floor the ages. This wasn't absolutely neccessary to answer the questions, but I still completed this step for uniformity.

<p align="center">
<img src="/HW2/Resources/screenshot32.png" width="1000" alt="flooring age values">
</p>

### Cleaning the Pet's Names Columns

I wasn't too scrutinous with the name columns because anything can be a name, and names are spelt all different kinds of ways. I just performed some clustering to catch any variations in capitilization, punctuation, or spaces.

<p align="center">
<img src="/HW2/Resources/screenshot35.png" width="1000" alt="clustering pet's full name">
</p>

<p align="center">
<img src="/HW2/Resources/screenshot36.png" width="1000" alt="clustering pet's everyday name">
</p>

### Links to Data and Operations Files

* [Cleaned Pet Names CSV File](/HW2/Resources/HW2-petnames.csv)
* [JSON Scripts of All Operations Performed](/HW2/Resources/HW2-petnames.json)

## II. Analyzing Cleaned Data

Now that the data has been cleaned, I can answer the following questions:

***1. How many types (kinds) of pets are there?***\
I found that there were <ins>23</ins> known types of pets. To find this, I used a combination of text faceting and clustering. There were also instances where I had to infer what the animal was by using the breed category. I removed any entries that were not an animal (e.g., virus, server, robot, cardboard poster, etc.). I also had to use judgement to decide which animals should be grouped together (e.g., putting Goldfish and Betta fish into one category).

***2. How many cats?***\
After cleaning up the "What kind of pet is this" column, it was easy to see, using a text facet, that <ins>501</ins> of the known pets were cats.

***3. How many breeds of cats?***\
Based on how I cleaned the cat breeds, I found that there were <ins>25</ins> different cat breeds; however, several of the cats' breeds were unknown. I used a combination of text facets, text filters, clustering, and manually editing to clean this column and arrive at 25. I also learned to differentiate between the terminology for cat fur color/markings and cat breeds. If only the cat's fur color/marking was mentioned, I did not consider these in the breed column. I consulted the Cat Fancier's Association for all other breeds.[^4]

***4. What's the most popular cat breed? How many cats are in that breed?***\
The most popular breed of cat was the <ins>Domestic short-hair</ins> with <ins>104</ins> cats. It is worth noting that for cases where only "short-hair" appeared in the breed column, I changed it to say "Domestic short-hair". (same for any medium- or long-hair entries). This decision was influenced by the fact that Domestic short-hairs are widely recognized as the common household cats in the United States[^5], often likened to "mutts." Therefore, when no specific place of origin (typically associated with purebred cats) was mentioned alongside "shorthair," it was assumed to be a domestic breed.

***5.What's the age range of the cats?***\
Cats ranged from <ins>less than 1 year to 24 years old.</ins> To streamline the data for better sorting accuracy, I used text faceting, clustering, and GREL expressions to eliminate unneccessary non-numeric text. Additionally, I aimed for simplicity and consistency by converting all age values into intergers. Rounding down to the nearest whole number was done to ensure uniformity, as many pet ownders may not have included months or fractions of years when reporting pet ages, even though they could have. After getting the list down to solely numeric integers, I transformed the column into numbers, rather than text, and sorted with smallest first to find the range.

***6. What's the age range of the rabbits? (Don't forget to look for bunny, too.)***\
Rabbits ranged from <ins>1 to 13 years old</ins>. After cleaning the pet age column (see process in previous answer), I used the text facet on the pet type column and selected "Rabbit" to find the age range.

***7. What is the oldest pet? Give the pet's name, kind, and age.***\
The oldest pet was <ins>Bruce Springsteen, a cat aged 24.</ins> After cleaning the pet age column (see process in answer to question 5), I was able to easily find the oldest pet by sorting entries by the pet age column.

***8. What are the top 5 most popular dog breeds? List the breed and number.***\
The number one dog breed was a mix of some sort with <ins>433 mixed-breed dogs</ins>. Following that was:
<ins>1. Golden Retriever (171), 2. Labrador Retriever (93), 3. Cocker Spaniel (22), 4. Shih Tzu (22), and 5. Beagle (20)</ins>. I consulted the American Kennel Club[^6] and United Kennel Club[^7] to narrow my list down to recognized dog breeds. I also gave listed any mix as its own category, "Mix".

***9. What's the most popular everyday name for a dog?***
<ins>Daisy</ins> is the most popular everyday name for a dog. I used text faceting and clustering on this column. It's important to note that I didn't delve too deeply into scrutinizing variations in spelling and punctuation, recognizing that names can often have numerous different forms.

***10. What's the most popular full name for any pet?***
<ins>Sophie</ins> is the most popular full name for any pet. I used text faceting and clustering on this column. It's important to note that I didn't delve too deeply into scrutinizing variations in spelling and punctuation, recognizing that names can often have numerous different forms.

# References

* Combining and Splitting Cells - OpenRefine - Subject & Research Guides at Connecticut College, https://conncoll.libguides.com/c.php?g=1125377&p=8209665
* General Refine Expression Language | OpenRefine, https://openrefine.org/docs/manual/grel
* The Ultimate Guide to Cat Fur Patterns, Colors and Markings, https://basepaws.com/blog/the-ultimate-guide-to-cat-fur-patterns-colors-and-markings
* What is a Lynx Point Siamese Cat?, https://www.siamesecatspot.com/lynx-and-tortie-point-siamese-cats/#:~:text=Lynx%20point%20Siamese%20cats%20(Or,part%20of%20the%20Siamese%20breed.
[^1]: Lizard & Gecko Facts, https://www.zillarules.com/pet-type/lizards-geckos#:~:text=Yes%2C%20geckos%20are%20lizards!%20What%20differentiates%20geckos%20from%20the%20group%20of%20lizards%20is%20that%20they%20lay%20eggs%20in%20pairs%20instead%20of%20large%20clutches%2C%20and%20they%20have%20the%20ability%20to%20vocalize%20with%20chirps%20and%20barking%20noises.%20Most%20geckos%20also%20lack%20eyelids%20and%20have%20sticky%20toes%20that%20enable%20them%20to%20climb%20walls.
[^2]: What’s the Difference Between a Turtle and a Tortoise? | Britannica, https://www.britannica.com/story/whats-the-difference-between-a-turtle-and-a-tortoise#:~:text=All%20tortoises%20are%20in%20fact%20turtles%E2%80%94that%20is%2C%20they%20belong%20to%20the%20order%20Testudines%20or%20Chelonia%2C%20reptiles%20having%20bodies%20encased%20in%20a%20bony%20shell%E2%80%94but%20not%20all%20turtles%20are%20tortoises.
[^3]: Domestic Shorthair Cat Facts | ASPCA Pet Health Insurance, https://www.aspcapetinsurance.com/resources/domestic-shorthair-cat-facts/#:~:text=Domestic%20Shorthair%2C%20or%20%E2%80%9Cmoggie%E2%80%9D%20in%20the%20United%20Kingdom%2C%20does%20not%20refer%20to%20an%20actual%20breed.%20These%20cats%20have%20mixed%20ancestry%2C%20which%20can%20vary%20from%20cat%20to%20cat%2C%20not%20unlike%20Mixed%20Breed%20dogs%20or%20%E2%80%9Cmutts.%E2%80%9D
[^4]: CFA Breeds – For Kids… About Cats, https://cfa.org/kids/breeds-and-colors/cfa-breeds/
[^5]: U.S. Pet (Dog and Cat) Population Fact Sheet, American Humane Association, https://web.archive.org/web/20130903060111/http://www.americanhumane.org/assets/pdfs/pets-fact-sheet.pdf
[^6]: Dog Breeds - Types Of Dogs - American Kennel Club, https://www.akc.org/dog-breeds/
[^7]: Recognized Breeds | United Kennel Club, https://www.ukcdogs.com/docs/showforms/breed-abbreviations.pdf
















