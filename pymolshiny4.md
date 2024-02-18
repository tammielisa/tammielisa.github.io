# ChatGPT Shiny App Part 4: Alternate Slider Code (This One Worked!)

After much frustration and scouring Google searches for answers, I got the idea that maybe there was a problem
with the package functions it was giving me. I took a look at the R repository documention for the 'Shiny JS" package,
And didn't see an 'updateImage' function. I don't know if all package functions are included in the official document 
or not, or if it matters, but I asked anyway. As it turns out, I was right!

Me: hey chat, I'm looking at the documentation for shinyjs and I don't see updateImage. 
maybe this function no longer exists. Do you know of an alternative?

Chat: I apologize for the confusion. It seems I made an error in my responses. Indeed, there is no updateImage function in the shinyjs package.
To dynamically update the image source in Shiny, you can use the htmlOutput and renderUI functions. Here's an updated example:

```r
library(shiny)

ui <- fluidPage(
  sliderInput("view_slider", "Select View:", min = 1, max = 4, value = 1),
  uiOutput("pymolImage"),
)

server <- function(input, output) {
  output$pymolImage <- renderUI({
    img_src <- paste0("scene", input$view_slider, ".png")
    tags$img(src = img_src, id = "pymolImage")
  })
}

shinyApp(ui, server)
```

The renderUI function is used to dynamically generate the image tag based on the selected slider value.
The uiOutput("pymolImage") in the UI is a placeholder where the dynamically generated UI will be inserted.
This should work for dynamically updating the displayed image based on the slider value. I appreciate your patience, 
and I apologize for any confusion caused by my previous responses.

I pasted this code and... success! A simple simple with four values, that switches between images. Yay!
