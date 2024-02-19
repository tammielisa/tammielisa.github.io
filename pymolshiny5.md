# Part 5: Navbar and Subscript Text

Continuing with adding more functionality, I next wanted to add some tabs, text and links to the app. To keep this part shorter, 
I will show the conversation first and the entire code at the bottom. I wanted to include the chemical 
formula for the molecule shown in my images, so I asked how to do subscript. The way Chat told me to do it didn't work, so I had to 
search Google for that. The way I ended up doing it was using "tag$sub" as follows:

```r
p("Chemical Formula: H", tags$sub("2"), "O"),
```

**Me:**
"I'm ready to continue developing this shiny app. Building on the most recent code example you provided above, please provide 
padding on the top and sides, as well as some some space for text above the slider to show a title and information 
for the molecule shown in the images"

***Chat:***
*Certainly! To add padding, a title, and information text above the slider, you can modify the UI code. 
I'll add a navbarPage to organize the layout and include a title and a text box for additional information. 
Adjust the placeholder text as needed.*

*This code uses the navbarPage layout with a title, information text, and the slider for the molecule viewer. 
The CSS in the tags$head section adds padding to the body of the page. Adjust the padding values as needed to achieve the desired spacing.*

**Me:**
"looks pretty good. how can I show subscripted numbers for a chemical formula, where it says 'information about molecule'"

***Chat:***

*To display subscripted numbers for a chemical formula in Shiny, you can use the HTML function to include HTML tags for subscript formatting. 
For example, to display H₂O as a chemical formula, you can use H<sub>2</sub>O.*

**Me:**
"can you rewrite the above code with an extra tab on the navbar please? and make it come before the one above"

***Chat:***
*Certainly! Here's the modified code with an additional tab on the navbar... 
In this modification, I added a new tab named "Molecule Info" before the "Molecule Viewer" tab. You can customize 
the content of each tab as needed. The tabPanel function is used to create individual tabs within the navbarPage.*

```r
library(shiny)

ui <- fluidPage(
  tags$head(tags$style(HTML("
    body {
      padding-top: 20px; /* Adjust as needed */
      padding-left: 20px; /* Adjust as needed */
      padding-right: 20px; /* Adjust as needed */
    }
  "))),
  
  navbarPage(
    "Your Shiny App",
    tabPanel(
      "Molecule Info",
      fluidRow(
        column(
          width = 12,
          h3("Molecule Information"),
          p("Chemical Formula: H<sub>2</sub>O"),
          p("Additional information about the molecule goes here.")
        )
      )
    ),
    tabPanel(
      "Molecule Viewer",
      fluidRow(
        column(
          width = 12,
          h3("Molecule Viewer"),
          p("Chemical Formula: H<sub>2</sub>O"),
          sliderInput("view_slider", "Select View:", min = 1, max = 4, value = 1),
          uiOutput("pymolImage")
        )
      )
    )
  )
)

server <- function(input, output) {
  output$pymolImage <- renderUI({
    img_src <- paste0("scene", input$view_slider, ".png")
    tags$img(src = img_src, id = "pymolImage")
  })
}

shinyApp(ui, server)
```

**[On to part 6](pymolshiny6.md)**
