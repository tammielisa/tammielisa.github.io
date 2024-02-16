---
layout: default
---

# Creating an R Shiny App to Display PyMOL Images.

I’ve been learning to use PyMol, and I had the idea to create a Shiny app to display some of the images I created. 
To save time, and also since I’m an idiot, I enlisted the help of none other than Chat GPT to show me how. I chose Shiny because 
I have some experience with it as well as R.

Chat GPT showed me two different ways to code the app; one worked for me and the other didn’t. 
The one that did not work used the addition of the ShinyJS package, and I’m curious to know if this way works for others and why. 
Following is the conversation we had. 

Me:
hi. I'm learning to use pymol and I want to display some images I made that show a molecule from different angles. 
Since R is the language I'm most familiar with, I was wondering if this is possible to do with a Shiny app?

Chat:
Yes, it is indeed possible to create a Shiny app in R that displays molecular structures using PyMOL images from different angles. 
Shiny is a web application framework for R, and you can integrate it with PyMOL images to create an interactive and dynamic app.

Here is a basic outline of the steps you can follow to achieve this:

-Create a basic structure for your Shiny app, including UI and server functions. 
This could include elements like sliders, buttons, or any other controls you want for selecting different angles.

-Use the shinyjs package to integrate PyMOL images into your Shiny app. You can use HTML tags to embed images or iframes within your Shiny app.

-Use Shiny's reactive features to respond to user inputs. For example, you might use sliders to control the orientation of the molecule.

<pre>
```
library(shiny)
library(shinyjs)

ui <- fluidPage(
  # UI components go here
   tags$img(src = "path/to/your/image.png", id = "pymolImage"),
  useShinyjs()
)

server <- function(input, output) {
  # Server logic goes here
  observe({
    # Update the PyMOL image source based on user inputs
    shinyjs::updateImage(id = "pymolImage", src = paste0("path/to/your/image_", input$angle, ".png"))
  })
}

shinyApp(ui, server)
```
</pre>

Remember to replace "path/to/your/image.png" with the actual paths to your PyMOL images. Also, ensure that your PyMOL images 
are generated and saved in a format that can be easily displayed within a Shiny app.
