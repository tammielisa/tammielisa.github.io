# ChatGPT Shiny App Part 2: Make Sure You Have a 'WWW' Folder!

To start things off, I attempted to simply get the image to show up in the app. This is done in the UI part only; 
no server logic is needed. When working correctly, this should simply display a static image when the app runs. 
However, I kept getting a broken image icon. I made sure that the image was inside the app folder, but it didn’t work.

The code looked like this:
		
		
```r
library(shiny)
library(shinyjs)

ui <- fluidPage(
 # UI components go here
 ui <- fluidPage(
 # UI components go here
	 tags$img(src = "path/to/your/image.png", id = "pymolImage"),
		  useShinyjs()
	)
		
	)
		
server <- function(input, output) {
	 # Server logic goes here
	}
		
shinyApp(ui, server)
```
	
Asking chat for help:

**Me:** 
"I did step 3 but it shows a broken image file when I run it. What could be causing this?"

***Chat:***
*If you are seeing a broken image file when running your Shiny app, there are a few common issues you can check:
Correct Path to Images:
Ensure that the path to your PyMOL images is specified correctly. The path should be relative to the directory 
where your Shiny app script is located. You can use normalizePath to get the correct path.*

*Check Image Format:*
*Make sure that your PyMOL images are in a format supported by web browsers (e.g., PNG, JPEG).* 
*File Permissions:
Ensure that the Shiny app has the necessary permissions to access the image files. Check the file permissions for the image files 
and the directory containing them. 
Case Sensitivity:
Be aware that file paths are case-sensitive. Check that the letter casing (uppercase/lowercase) in your file paths 
matches the actual file names. 
Here's a modified example with normalizePath:*

```r
library(shiny)
library(shinyjs)

ui <- fluidPage(
  tags$img(src = normalizePath("path/to/your/image.png"), id = "pymolImage"),
  useShinyjs()
)

server <- function(input, output) {
  # Your server logic goes here
}

shinyApp(ui, server)
```

*This basic example just displays the image without any interactivity. Replace "path/to/your/image.png" with the correct path
to your PyMOL image. If you don't need any server logic, you can even remove the server function and run the shinyApp(ui) directly.*
	
I tried all this and still nothing. Chat seemed unable to help me at this point, so I started searching Google. 
I found several relevant conversations mentioning something about a “www” folder. 

**Me:**
"hey I found this somewhere:"
'To include the image in your App, you’ll need to make use of the image tag, img. 
When you run your App, Shiny automatically knows to check the www folder any time the img tag gets called…' 
What is this www folder?"
	
***Chat:*** 
*in a Shiny app, the www folder is a special directory where you can place static files such as images, stylesheets, 
JavaScript files, etc. The contents of the www folder are automatically made available to the web browser when your Shiny app is running. 
It acts as a web-accessible directory, and Shiny automatically serves its contents.
When you use the tags$img function to include an image in your Shiny app, the path to the image should be relative to the www folder. 
By default, Shiny looks for static assets in the www folder, so you don't need to explicitly specify the path to the www folder in your code.*

**Me:** 
"I don't see this folder anywhere, is it because I'm using a mac?"

***Chat:*** 
*No, the absence of the www folder might be due to it not being automatically created when you create a Shiny app. 
If it doesn't exist, you can simply create it yourself in the same directory as your Shiny app script.*
*Here are the steps to create the www folder manually:*
*Open your Shiny app directory in Finder.* 
*Create a new folder named www in the same directory* *where your Shiny app script e.g. app.R* *or server.R and ui.R is located.*  *Place your static files, such as images, inside the www folder.* 

```
	- shiny_app_directory/
		  - app.R
		  - www/
		    - scene1.png
		    - other_static_files.css
```
*After creating the www folder and placing your static files in it, you should be able to reference those files in your Shiny app 
using paths relative to the www folder.*
	
** Me:** 
"OMG it worked! I just created a folder called "www" and dumped the images in there."


Main takeaway: ensure there is a folder titled “www” within your Shiny app folder, and place any images you want the app to display in there. 
Pretty random right?

**[On to part 3.](pymolshiny3.md)**
