# A Shiny App That Makes Visulations from PDB Files

**Prompt:**
I want to make a Shiny app that does this. I want it to read in 3 different pdb files of hemoglobin 
from 3 different animal types, canine, equine and bovine. I want the app to extract the amino acid sequences
And produce visualizations of the amino acid frequencies using ggplot2. I want to switch between 
The visualizations using a drop down menu in a side bar. The graphs should display on the right side.

Note: I replaced the line "pdb2seq(pdb, oneletter = TRUE)" with "pdbseq(pdb, aa1 = FALSE)"
There is no function 'pdb2seq', I don't know why ChatGPT thinks there is.

**ChatGPT Code**

```r
# Install and load necessary packages
install.packages(c("shiny", "bio3d", "ggplot2"))
library(shiny)
library(bio3d)
library(ggplot2)

# Define the UI
ui <- fluidPage(
  titlePanel("Hemoglobin Amino Acid Frequencies"),
  
  sidebarLayout(
    sidebarPanel(
      selectInput("animal", "Select Animal Type", 
                  choices = c("Canine", "Equine", "Bovine"), selected = "Canine")
    ),
    
    mainPanel(
      plotOutput("amino_acid_plot")
    )
  )
)

# Define the server
server <- function(input, output) {
  
  # Read PDB files based on selected animal type
  pdb_file <- reactive({
    switch(input$animal,
           "Canine" = "canine_hemoglobin.pdb",
           "Equine" = "equine_hemoglobin.pdb",
           "Bovine" = "bovine_hemoglobin.pdb")
  })
  
  # Extract amino acid sequence
  protein_seq <- reactive({
    pdb <- read.pdb(pdb_file())
    pdb2seq(pdb, oneletter = TRUE)
  })
  
  # Create amino acid frequency plot
  output$amino_acid_plot <- renderPlot({
    aa_counts <- data.frame(AminoAcid = names(table(protein_seq())),
                            Frequency = as.numeric(table(protein_seq())))
    
    ggplot(aa_counts, aes(x = AminoAcid, y = Frequency, fill = AminoAcid)) +
      geom_bar(stat = "identity") +
      geom_text(aes(label = AminoAcid), position = position_stack(vjust = 0.5), color = "white", size = 3) +
      scale_fill_manual(values = rainbow(20)) +
      labs(title = paste(input$animal, "Hemoglobin Amino Acid Frequencies"),
           x = "Amino Acid", y = "Frequency") +
      theme_minimal() +
      guides(fill = FALSE) +
      theme(axis.text.x = element_blank())
  })
}

# Run the app
shinyApp(ui, server)
```
