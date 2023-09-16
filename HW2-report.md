# HW 2: Data Cleaning - CS 625, Fall 2023

Jenah Parman\
Due: September 20, 2023

## Introduction

This report provides an overview of the steps I took to clean the PetNames.tsv dataset for analysis. The survey was iniated on July 21, 2019 on Twitter by Dr. Jen Golbeck, and it collected information about people's pets, including the type of pet, the pet's full name (excluding the owner's last name), the pet's everyday name, age, and breed. Interestingly, the main goal of gathering this data was to create a messy dataset intentionally for practicing data cleaning. In the following sections are the steps I took to accomplish this goal.

## Data Cleaning Process

### Dealing with Multi-Valued Cells

I started by using *Text facet* on the pet type column to see all the unique values and their frequencies.

Upon inspecting the different unique values, I noticed a row with multiple pets in one. I decided to find out if there were more of these instances and handle them before continuing.
I added a *Text filter* to the pet type column and searched for any entries that contained ",", ";" " and ", and "&". I flagged the ones that seemed like they represented more than one pet. Then, I considered the possibility of respondents who have multiples on the same type of pet. I used a *Text filter* on the pet name column and followed the same search technique as before. I ended up finding four entries that represented more than one pet.

<p align="center">
<img src="HW2-screenshots/screenshot45.png" width="1000" alt="multi-valued cells">
</p>

To fix this, I seperated each pet attribute in the columns with a ";". Then, I used the *Split multi-valued cells* feature with a seperator, ";" giving each pet its own row.

<p align="center">
<img src="HW2-screenshots/screenshot50.png" width="1000" alt="multi-valued cells split incomplete">
</p>

I could not get the pet kind column to agree with the newly created rows for the different pets, so I had to manually enter in this column.

<p align="center">
<img src="HW2-screenshots/screenshot51.png" width="1000" alt="multi-valued cells split complete">
</p>

I assumed that this disagreement of populating existing rows had something to do with the first column being tied to the ID number. It seemed like the newly created rows were almost "sub-rows" of the originals, i.e., they did not have their own ID number. I thought that this seemed OK at first, but then I realized that this was affecting the overall count of items. In an attempt to mitigate this situation, I exported the file and then re-uploaded it to Open Refine. This ended up giving each row its own ID number and upped the count to match the new items. Problem solved.

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
<img src="HW2-screenshots/screenshot1.png" width="1000" alt="clustering pet kind again">
</p>



