# ChatGPT Shiny App Part 3: Adding a Slider (ChatGPT Got This Wrong!)

Now that I got the image to display correctly at launch, I next wanted to add interactivity. 
For now, I just wanted to add a small slider that changed between a few different images of the molecule at different angles.
The following method shown to me did not work, and you'll see why in the next part. Spoiler: the code is wrong!
Be advised, I am using the free version here.

**Me:**
"Can you show me how to use a slider to change the view. I have four separate pngs"

***Chat:***
*Certainly! To use a slider to change the view and display different images based on the slider's value,* 
*you can modify your Shiny app to include a sliderInput and update the displayed image dynamically in the server logic.*

*Here's an example using a slider to cycle through four different images:*

```r
library(shiny)
library(shinyjs)

ui <- fluidPage(
  sliderInput("view_slider", "Select View:", min = 1, max = 4, value = 1),
  tags$img(src = "scene1.png", id = "pymolImage"),
  useShinyjs()
)

server <- function(input, output) {
  observe({
    # Update the PyMOL image source based on the view selected by the slider
    shinyjs::updateImage(id = "pymolImage", src = paste0("scene", input$view_slider, ".png"))
  })
}

shinyApp(ui, server)
```

*In this example:*

*sliderInput is used to create a slider named "view_slider" with values ranging from 1 to 4, representing the different views.
tags$img displays the initial image with an id of "pymolImage".
observe in the server logic is used to reactively update the image source based on the value selected by the slider.
Make sure that you have the images named "scene1.png", "scene2.png", etc., in your www folder.*

At this point the app seemed to work, but the functionality was not there. What I got was a page that displayed a slider with the first image
beneath it. I was able toggle the slider, but image did not change.

**Me:** 
"Ok. So I'm moving the slider but it isn't updating, it keeps displaying the static first image"

***Chat:***
*I see, it seems there is an issue with the observe block not correctly updating the image. 
The problem is likely with the paste0 function, which is not separating the slider value and the file extension properly. 
Let's correct that:*

```r
library(shiny)
library(shinyjs)

ui <- fluidPage(
  sliderInput("view_slider", "Select View:", min = 1, max = 4, value = 1),
  tags$img(src = "scene1.png", id = "pymolImage"),
  useShinyjs()
)

server <- function(input, output) {
  observe({
    # Update the PyMOL image source based on the view selected by the slider
    shinyjs::updateImage(id = "pymolImage", src = paste0("scene", input$view_slider, ".png"))
  })
}

shinyApp(ui, server)
```

*Ensure that you have the images named scene1.png, scene2.png, scene3.png, and scene4.png in your www folder. This code should dynamically update 
the displayed image based on the selected slider value.*

**Me:**
Still the same problem. And I just keep getting that same warning that I mentioned before. 
I guess I should just give up. Thanks for your help anyway

**[On to part 3.](pymolshiny4.md)**
