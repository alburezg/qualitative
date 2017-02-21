library(shiny)

text1 <- "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce nec quam ut tortor interdum pulvinar id vitae magna. Curabitur commodo consequat arcu et lacinia. Proin at diam vitae lectus dignissim auctor nec dictum lectus. Fusce venenatis eros congue velit feugiat, ac aliquam ipsum gravida. Cras bibendum malesuada est in tempus. Suspendisse tincidunt, nisi non finibus consequat, ex nisl condimentum orci, et dignissim neque est vitae nulla." 
text2 <- "Aliquam ut purus neque. Maecenas justo orci, semper eget purus eu, aliquet molestie mi. Duis convallis ut erat at faucibus. Quisque malesuada ante elementum, tempor felis et, faucibus orci. Praesent iaculis nisi lorem, non faucibus neque suscipit eu. Ut porttitor risus eu convallis tristique. Integer ac mauris a ex maximus consequat eget non felis. Pellentesque quis sem aliquet, feugiat ligula vel, convallis sapien. Ut suscipit nulla leo"
highlight <- '
function getSelectionText() {
var text = "";
if (window.getSelection) {
text = window.getSelection().toString();
} else if (document.selection) {
text = document.selection.createRange().text;
}
return text;
}

document.onmouseup = document.onkeyup = document.onselectionchange = function() {
var selection = getSelectionText();
Shiny.onInputChange("mydata", selection);
};
'

coded_text <- character(0)

ui <- bootstrapPage(
  tags$script(highlight),
  fluidRow(
    column(4,
           tags$h1("Text to code"),
           tags$h2("From table"),
           tableOutput("table"),
           tags$h2("From raw text"),
           verbatimTextOutput("text")
    ),
    column(4,
           tags$h1("Coding options"),
           actionButton("code1", "Assign selected text to Code1"),
           tags$h1("Code1 output"),
           verbatimTextOutput("selected_text")
    )
  )
)


server <- function(input, output) {
  output$table <- renderTable({
    data.frame(paragraph = 1:2, text = c(text1, text2))
  })
  
  output$text <- renderText(paste(text1, text2))
  
  coded <- eventReactive(input$code1, {
    coded_text <<- c(coded_text, input$mydata)
    coded_text
  })
  
  output$selected_text <- renderPrint({
    coded()
  })
  
}

shinyApp(ui = ui, server = server)
