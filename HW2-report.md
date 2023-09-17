# HW 2: Data Cleaning - CS 625, Fall 2023

Jenah Parman\
Due: September 20, 2023

## Introduction

This report provides an overview of the steps I took to clean the PetNames.tsv dataset for analysis. The survey was iniated on July 21, 2019 on Twitter by Dr. Jen Golbeck; it collected information about people's pets, including the type of pet, the pet's full name (excluding the owner's last name), the pet's everyday name, age, and breed. Interestingly, the main goal of gathering this data was to create a messy dataset intentionally for practicing data cleaning. In the following sections are the steps I took to accomplish this goal.

## Data Cleaning Process

### Dealing with Multi-Valued Cells

I started by using *Text facet* on the pet type column to see all the unique values and their frequencies.

Upon inspecting the different unique values, I noticed a row with multiple pets in one. I decided to find out if there were more of these instances and handle them before continuing.

To do this, I added a *Text filter* to the pet type column and searched for any entries that contained ",", ";", " and ", or "&". I flagged the ones that seemed like they represented more than one pet. Then, I considered the possibility of respondents who have more than one of the same kind of pet. I used a *Text filter* on the pet name column, searched for ",", ";", " and ", or "&" again, and flagged any conspicuous rows. I ended up finding four entries that represented more than one pet.

<p align="center">
<img src="HW2-screenshots/screenshot45.png" width="1000" alt="multi-valued cells">
</p>

To fix this, I seperated each pet attribute in the columns with a ";". Then, I used the *Split multi-valued cells* feature with the *Seperator* set to ";", giving each pet its own row.

<p align="center">
<img src="HW2-screenshots/screenshot50.png" width="1000" alt="multi-valued cells split incomplete">
</p>

I could not get the pet kind column to agree with the newly created rows for the different pets, so I had to manually enter in this column.

<p align="center">
<img src="HW2-screenshots/screenshot51.png" width="1000" alt="multi-valued cells split complete">
</p>

I assumed that this disagreement of populating existing rows had something to do with the first column being tied to the ID number. It seemed like the newly created rows were almost "sub-rows" of the originals, i.e., they did not have their own ID number. I thought that this seemed OK at first, but then I realized that this was affecting the overall count of items. In an attempt to mitigate this situation, I exported the file and then re-uploaded it to Open Refine. This ended up giving each row its own ID number and upped the count to match the new items. Problem solved.

<p align="center">
<img src="HW2-screenshots/screenshot53.png" width="1000" alt="new rows with ID numbers">
</p>

### Cleaning the "What Kind of Pet" Column

I began the data cleaning process by first reviewing the analysis questions. The first question pertained to the different kinds of pets, so this is where I decided to start cleaning.

I applied a *Text facet* on the pet type column. 

<p align="center">
<img src="HW2-screenshots/screenshot0.png" width="1000" alt="text faceting pet kind">
</p>
<br/>

I then used the *Cluster* feature to join any rows that convey the same information.

<p align="center">
<img src="HW2-screenshots/screenshot63.png" width="1000" alt="clustering pet kind">
</p>
<br/>

I was able to join several instances of misspellings or variations or  "Dog", "Cat", "Hamster", "Guinea Pig", etc.. I tried all of the different *Keying functions*, and was able to go from 83 unique values to 53 on the first round of clustering.

After inspecting the remaining unique values in the *Text facet*, I manually removed any rows that stuck out to me as "*definitely not a pet*", e.g., "Card board poster", "Robot", "Roomba", "Virus", and "Server".

I also handled things that stuck out to me as "*definitely not a pet*" but probably a typo:

<p float="left">
<img src="HW2-screenshots/screenshot55.png" width="499" alt="cat pet typo">
<img src="HW2-screenshots/screenshot56.png" width="499" alt="dog pet typo">
</p>
<br/>

When sorting the *Text facet* by count, I noticed a lot of respondents simply typed "Other", probably because of the nature of the question-- "What kind of pet is this (Dog, Cat, Bird, Other)". Respondents may have assumed that if it wasn't one of the first three mentioned to enter "Other". I wanted to see if the pet breed column gave any dead giveaways, and it did! I was able to figure out almost all of them from information provided by the breed column, so I manually entered these.

<p align="center">
<img src="HW2-screenshots/screenshot57.png" width="1000" alt="other facet before">
</p>
<p align="center">
<img src="HW2-screenshots/screenshot58.png" width="1000" alt="other facet after">
</p>
<br/>

I missed the "Winter white hamster" in this screenshot, but I ended up fixing this later.

I also noticed that some respondents would enter their pet kind but also include the word "Other" or "(other)" in their response. I used a GREL expression: `value.replace("Other","").replade("other","")` to get rid of the "Other" word. However, this still left some extraneous puntuation for some entries.

Then, I used a *Text filter* to find any instances of "kitty", "kitten", "kitty cat", etc.. I simply searched for "kit", and then transformed the selected cells to say "Cat".

<p align="center">
<img src="HW2-screenshots/screenshot60.png" width="1000" alt="kit to cat">
</p>

Then, I did for "puppy", "puppy dog", etc., and changed those to "Dog".  

After narrowing the unique values down to 40, I used *Cluster* again.

This helped get ride of the leftover punctuation from the entries containing "Other".

<p align="center">
<img src="HW2-screenshots/screenshot61.png" width="1000" alt="clustering pet kind again">
</p>

A few entries listed the pet name as it's kind. I was able to figure out that these were all dogs by looking at the breed. I used a *Transform* to make these all say "Dog", while ensuring that the pet name was in the right place.

<p align="center">
<img src="HW2-screenshots/screenshot1.png" width="1000" alt="dog names to dog">
</p>

After doing some research, I found out that geckos are lizards and all tortoises are turtles (but not all turtles are tortoises.) I wanted to narrow my list of unique values down more, so I decided to consolidate these by using a *Text filter*, searching for "gecko" and "tortoise", and using a cell *Transform* to change them to "Lizard" and "Turtle". I made sure to indicate the more specific animal type in the pet breed category before making the change. I repeated the same steps for any "goldfish" or "betta fish", simply changing these to "Fish" but mentioning the specificities in the breed column. I had a hard time deciding whether I should solidate the two chicken entries with the "Bird" category, but I ended up doing so. I noticed that the list had only two different kinds of insects (Bees and Spiney Leaf Insect), so I joined these under one "Insect" category.

<p align="center">
<img src="HW2-screenshots/screenshot5.png" width="1000" alt="consolidating pet kinds">
</p>

I finally narrowed the list down to something I was satisfied with, containing unique values that I thought weren't too specific or too broad.

<p align="center">
<img src="HW2-screenshots/screenshot80.png" width="300" alt="final list of pet kinds">
</p>

### Cleaning the "Pet's Breed" Column

Two of the questions ask about the pet's breed, more specifically, cat and dog breeds. This is where I decided to clean next.

#### Cat Breeds

I used a *Text facet* on the pet kind column and selected "Cats" to start working with just the cat breeds. I then applied another *Text facet* on the pet breed column.

Starting with 143 unique values, I decided to *Cluster* first, trying all of the *Keying functions*. 

There were many variations of "Domestic [short,medium, or long]-hair", so I joined all of these under one spelling and format. I did the same for any "[Place of Origin] [short,medium, or long]-hair"s.

<p align="center">
<img src="HW2-screenshots/screenshot6.png" width="1000" alt="cat breed cluster">
</p>

I had to do a lot of reading on cat breeds in comparison to cat coat and marking terminology. I also found it challenging to figure out how to classify the cats. *Should I only include breeds recognized by the CFA (Cat Fanciers' Association)? How should I handle mixed-breed cats? What even is a Domestic short-hair?*

I decided that I would remove any values in the pet breed column that solely listed a cat's coat color/marking name (e.g., Tabby, Calico, Tuxedo, Black, etc.). However, if it contained a cat coat color/marking AND "[short,medium, or long]-hair", then I would change these to "Domestic [short,medium, or long]-hair". I decided that if it wasn't a CFA recognized breed, but it did contain hair length, then it was probably a "Domestic". It seems like "**Domestic** [short,medium, or long]-hair" is like the "mutt" of cats, having an unknown lineage. I also found out that Domestic short-hairs are called "Moggies" in England, so I changed every instance of "Moggy" to "Domestic short-hair". 

I removed the values that were only coat color/marking name by applying a *Text filter* and searching for the color/marking name, while flagging any values that contained additional info hinting at a breed.

<p align="center">
<img src="HW2-screenshots/screenshot12.png" width="1000" alt="filtering tuxedo cat">
</p>

Then, I applied a *Flag facet*, filtered by *False*, and performed a cell *Transform*, just changing these values to an empty string.

<p align="center">
<img src="HW2-screenshots/screenshot13.png" width="1000" alt="replacing with empty string">
</p>

I then filtered by *True*, i.e., the flagged values, and performed a cell *transform* to make these say their breed.

<p align="center">
<img src="HW2-screenshots/screenshot14.png" width="1000" alt="changing values to cat breed">
</p>

I repeated these steps for remaining cat color coats/markings. For any "Part [cat breed]" or "[cat breed] Mix", I put under one category called "Mix". Lynx Point Siamese was a tricky one because it seems like it would be a type of Siamese. After doing some research, it seems that it is classified in many different ways, but they are bred from a Siamese and a tabby cat, so I just placed this in the "Mix" category.

These steps got my list of cat breeds down to something manageable with true unique values.

<p align="center">
<img src="HW2-screenshots/screenshot17.png" width="300" alt="cat breed cleaned list">
</p>

#### Dog Breeds

I followed a similar technique for cleaning up the list of dog breeds. By first applying a *Text Facet* for both pet kind (dog selected) and pet breed, I was able to narrow the messy list down significantly by using *Cluster* and trying all *keying functions*.

<p align="center">
<img src="HW2-screenshots/screenshot33.png" width="1000" alt="clustering dog breeds">
</p>

I noticed there were several mixed-breed dogs, so similarly to what I did for cat breeds, I created a "Mix" category. I then added a *Text filter* and searched for any instance of the word "mix" and changed these values using a cell *Transform* to say "Mix". I also did the same for any values that contained "mutt" or "cross".

<p align="center">
<img src="HW2-screenshots/screenshot34.png" width="1000" alt="mix category">
</p>

I cross-referenced the AKC (American Kennel Club) and UKC (United Kennel Club) list of dog breeds with my list of unique values, and for any that weren't listed and seemed like a mixed-breed (e.g., Goldendoodle, Yorkiepoo, Labradoodle, etc.), I performed a cell *Transform* to make these "Mix".

I narrowed the list of unique values down by maually tweaking a few things to line up with the AKC and UKC lists, and then clustering again. I repeated this a few times until I got a list that I was happy with.

### Cleaning the "Pet's Age" Column

There are two questions regarding pet's age, so I started working with this column next. I noticed these questions had involved sorting the ages by their numberical value, so I decided to try to get this column to exclusively numbers.

My thought process went like this: It appeared that most of the pets were over a year old, and when discussing age, humans typically refer to years unless talking about a newborn. Anything less than 12 months doesn't seem like a significant amount of time, so I decided to consider anything younger than one year old as 0. I aimed to simplify this to whole numbers (integers). In human age, we usually don't say, "I'm 23 years and 10 months old"; we simply say, "I'm 23." So, I rounded down (floored) any age that was expressed as a float or fraction. Additionally, a significant number of pets didn't specify their age in months or fractions of a year. To ensure consistency and impartiality, I opted to convert all ages into integers rounded down. Also, if there was an entry that mentioned more than one age or a range or ages, I went with the lowest value. For any deceased pet's, I used an empty string.

I started by applying a *Text filter* on the pet age column. I searched for "y", hoping to gather anyone who may have listed any variation of the word "years" or "years old". I flagged any records that had a "y" in it, but was not referring to years. Then, I filtered by values NOT flagged. I then used a GREL expression: `value.replace("years","").replace("year","").replace("yrs","").replace("y","").replace("YO","").replace("yo","")` to try to get rid of any text.

<p align="center">
<img src="HW2-screenshots/screenshot18.png" width="1000" alt="GREL expression to remove years text">
</p>

I repeated these steps for months, but this time the goal was to change these to values to "0". I first filtered for "m", flagging any values that either greater than 12 months or weren't related.

<p align="center">
<img src="HW2-screenshots/screenshot19.png" width="1000" alt="GREL expression to remove years text">
</p>

I filtered by NOT flagged values, and used a cell *Transform* to change these values to "0".

<p align="center">
<img src="HW2-screenshots/screenshot20.png" width="1000" alt="GREL expression to remove years text">
</p>

<p align="center">
<img src="HW2-screenshots/screenshot21.png" width="1000" alt="GREL expression to remove years text">
</p>

Then, I filtered by flagged values, and changed these to "1".

<p align="center">
<img src="HW2-screenshots/screenshot22.png" width="1000" alt="GREL expression to remove years text">
</p>
<p align="center">
<img src="HW2-screenshots/screenshot24.png" width="1000" alt="GREL expression to remove years text">
</p>

I repeated these steps for weeks, using "w" to filter.

<p align="center">
<img src="HW2-screenshots/screenshot24.png" width="1000" alt="GREL expression to remove years text">
</p>

Now I was left with 66 out of 1783 non-numeric values. I performed a GREL expression in an attempt to remove any extraneous text.

<p align="center">
<img src="HW2-screenshots/screenshot25.png" width="1000" alt="GREL expression to remove years text">
</p>

<p align="center">
<img src="HW2-screenshots/screenshot26.png" width="1000" alt="GREL expression to remove years text">
</p>

This fixed most of them, but I ended up having to go in and manually edit a few.

<p align="center">
<img src="HW2-screenshots/screenshot28.png" width="1000" alt="GREL expression to remove years text">
</p>

<p align="center">
<img src="HW2-screenshots/screenshot29.png" width="1000" alt="GREL expression to remove years text">
</p>

Finally, I transformed the age column into only numbers with no text.

<p align="center">
<img src="HW2-screenshots/screenshot30.png" width="1000" alt="GREL expression to remove years text">
</p>

I then used a GREL expression to floor the ages. This wasn't absolutely neccessary to answer the questions, but I still completed this step for uniformity.

<p align="center">
<img src="HW2-screenshots/screenshot32.png" width="1000" alt="GREL expression to remove years text">
</p>

### Cleaning the Pet's Names Columns

I wasn't too scrutinous with the name columns because anything can be a name, and names are spelt all different kinds of ways. I just performed some clustering to catch any variations in capitilization, punctuation, or spaces.

<p align="center">
<img src="HW2-screenshots/screenshot35.png" width="1000" alt="GREL expression to remove years text">
</p>

<p align="center">
<img src="HW2-screenshots/screenshot36.png" width="1000" alt="GREL expression to remove years text">
</p>











