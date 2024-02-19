# Part 6: More Tabs, Images and Source Links

**Me:**
"how can I add a different image to the other tab?"

***Chat:***
*To display a different image in the "Molecule Info" tab compared to the "Molecule Viewer" tab, 
you can create a separate uiOutput and renderUI for each tab.
I added a new uiOutput called "infoImage" in the "Molecule Info" tab.
The corresponding renderUI block generates the image for the "Molecule Info" tab.
Adjust the src attribute to the path of the image you want to display in the "Molecule Info" tab.
This way, you can have different images for each tab. Ensure that you have the appropriate images 
(e.g., "info.png" and "scene1.png") in your www folder or adjust the paths accordingly.*

**Me:**
"awesome! just one more thing, I would like to include a link to my information source, 
the protein data bank, at the bottom of the entire app"

***Chat:***
*Certainly! You can add a hyperlink to the Protein Data Bank (PDB) at the bottom of your app. 
You can use the tags$a function to create a hyperlink. In this example, I added a new tab named "Information Source" with a hyperlink 
to the Protein Data Bank. You can customize the text and link URL according to your preferences. 
The tags$a function is used to create the hyperlink.*

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
          p("Additional information about the molecule goes here."),
          uiOutput("infoImage")
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
    ),
    tabPanel(
      "Information Source",
      fluidRow(
        column(
          width = 12,
          h3("Information Source"),
          p("For more information, visit the "),
          tags$a(href = "https://www.rcsb.org/", "Protein Data Bank (PDB)"),
          p(".")
        )
      )
    )
  )
)

server <- function(input, output) {
  output$infoImage <- renderUI({
    # Replace "info.png" with the image you want for the "Molecule Info" tab
    tags$img(src = "info.png", id = "infoImage")
  })

  output$pymolImage <- renderUI({
    img_src <- paste0("scene", input$view_slider, ".png")
    tags$img(src = img_src, id = "pymolImage")
  })
}

shinyApp(ui, server)
```
