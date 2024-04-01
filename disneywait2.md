## Collecting Disney World Wait Time Data Using R, Part 2

Now that I had all the data from the four APIs in a single data frame,
I wanted to limit the rows just to certain attractions. I included the ones
I was particulary interested in. Others I included were ones that are 
especially popular, and/or usually have particularly long wait times. 

With ChatGPT's help, I filtered the data frame by this shortlist of 
attractions, and then used a function from the lubridate package to convert 
the times stamps in the 'lastUpdated' column to a more readable form. 

```{r}
# List attractions of interest
  rides <- c("Expedition Everest - Legend of the Forbidden Mountain", 
             "Avatar Flight of Passage", "DINOSAUR", "Kilimanjaro Safaris",
             "TRON Lightcycle / Run", "Seven Dwarfs Mine Train", 
             "Big Thunder Mountain Railroad", "Pirates of the Caribbean",
             "Space Mountain", "Haunted Mansion", "Jungle Cruise", "Mad Tea Party", 
             "The Magic Carpets of Aladdin", "Peter Pan's Flight", 
             "Guardians of the Galaxy: Cosmic Rewind", "Frozen Ever After",
             "Remy's Ratatouille Adventure", "Mission: SPACE", "Spaceship Earth",
             "Test Track", "The Twilight Zone Tower of Terror™", "Toy Story Mania!", 
             "Star Wars: Rise of the Resistance", "Millennium Falcon: Smugglers Run",
             "Mickey & Minnie's Runaway Railway", "Alien Swirling Saucers")

# Filter data frame to include only entries for attractions of interest,
# Convert date-time fields to Eastern Time (ET) with both date and time components
df <- data[data$name %in% rides, ]
df$lastUpdate <- ymd_hms(df$lastUpdate, tz = "US/Eastern")
```

Next, I added a column to the table to show which parks the listed attractions 
are found in, then slightly altered the order of the columns. 

```{r}
#create a 'park' object
park <- c("Animal Kingdom", "Animal Kingdom", "Animal Kingdom", "Animal Kingdom", 
           "Magic Kingdom", "Magic Kingdom", "Magic Kingdom", "Magic Kingdom", 
           "Magic Kingdom", "Magic Kingdom", "Magic Kingdom", "Magic Kingdom", 
           "Magic Kingdom", "Magic Kingdom", "Epcot", "Epcot","Epcot","Epcot","Epcot",
           "Epcot", "Hollywood Studios", "Hollywood Studios","Hollywood Studios", 
           "Hollywood Studios","Hollywood Studios","Hollywood Studios")

#append 'park' object to dataframe
#df <- cbind(df, park)

#reorder columns to put 'park' before 'lastUpdate'
df <- df[, c(1, 2, 3, 4, 6, 5)]
view(df)
```

