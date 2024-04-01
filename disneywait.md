##Collecting Disney World Wait Time Data Using R

After a recent trip to Disney World using the app to see atrraction wait times, I felt I could do better. 
I wanted to create something that was a simple table that contained the top attractions all in one place. 
I found a useful api that can collect data from hundreds of theme parks, the Theme Park Wiki. 
Here's the link to the resource:

[Theme Park Wiki](https://api.themeparks.wiki/docs/preview/#/)

I had to use a unique Api for each Disney World park, as follows.

```{r}
library(jsonlite)
library(httr)
library(lubridate)

#store API URLs for park wait times
api1 <- "https://api.themeparks.wiki/preview/parks/WaltDisneyWorldAnimalKingdom/waittime"
api2 <- "https://api.themeparks.wiki/preview/parks/WaltDisneyWorldMagicKingdom/waittime"
api3 <- "https://api.themeparks.wiki/preview/parks/WaltDisneyWorldEpcot/waittime"
api4 <- "https://api.themeparks.wiki/preview/parks/WaltDisneyWorldHollywoodStudios/waittime"

#Call requests
request1 <- GET(api1)
request2 <- GET(api2)
request3 <- GET(api3)
request4 <- GET(api4)
```

ChatGPT showed me how to convert the data to text, and parse it into something readable,
using the 'fromJSON' function from the JSONlite package. Then it showed me how to only
include the necessary data columns for my purpose, which I then combined into a single
dataframe using 'rbind.'

```{r}
#Parse JSON data and convert to data frames
data1 <- fromJSON(content(request1, "text"))
data2 <- fromJSON(content(request2, "text"))
data3 <- fromJSON(content(request3, "text"))
data4 <- fromJSON(content(request4, "text"))

# Specify columns to include in the output
columns <- c("id", "name", "waitTime", "status", "lastUpdate")

# Subset the data frame to include only the columns of interest
df1 <- data1[, columns]
df2 <- data2[, columns]
df3 <- data3[, columns]
df4 <- data4[, columns]

#combine data frames into one
data <- rbind(df1, df2, df3, df4)
#data
```

