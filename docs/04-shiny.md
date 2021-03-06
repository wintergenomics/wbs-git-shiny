---
output:
  pdf_document: default
  html_document: default
---
# Apps con Shiny

## Diapositivas

Puedes descargar las diapositivas del curso [aquí](https://drive.google.com/u/0/uc?id=1lSnZxaSVuuOb5ilQ1GsvsZG5qD7tqVGr&export=download)

## Conociendo shiny
Para comenzar, cargamos la librería de Shiny

```r
library(shiny)
```


```r
ui <- fluidPage()
server <- function(input, output){}
shinyApp(ui = ui, server = server)
```

Escribiendo nuestro primer mensaje entre comillas `"`.


```r
ui <- fluidPage("Hola Mundo")
```

## Crear mi primera aplicación
Primero definimos la UI de la aplicación. Podemos insertar un mensaje simple como `"Hola mundo"` utilizando `fluidPage()`. También podemos agregar un slider o barra sencilla utilizando `sliderInput()`. Podemos agregar checkbox con `checkboxGroupInput()`.


```r
ui <- fluidPage(
    "Hola Mundo",
    sliderInput(inputId = "num",          
                label="Elige un número",
                value=25,
                min=1, 
                max=100,
      ),
    checkboxGroupInput("icons", "Choose icons:",
                       choiceNames =
                           list(icon("calendar"), icon("bed"),
                                icon("cog"), icon("bug")),
                       choiceValues =
                           list("calendar", "bed", "cog", "bug")
    )
```

Definimos el server

```r
server <- function(input, output) {
  output$hist <- renderPlot({
      hist(rnorm(input$num),
           main=input$title)
  })
  output$stats <- renderPrint({
      summary(rnorm(input$num))
  })
}
```

Y finalmente corremos la aplicación.


```r
shinyApp(ui = ui, server = server)
```

### Agregando más parámetros

Podemos modificar el `sliderInput` agregando un intervalo numérico con `value`, decimales e animación con `animate`.
Con `selectInput()` generamos una lista desplegable. `textInput()` permite crear una caja para agregar texto y `plotOutput()` nos permite incorporar gráficos. 


```r
ui <- fluidPage(
    "Hola Mundo",
    sliderInput(inputId = "num",          
                label="Elige un número",
                value=25,
                min=1, 
                max=100,
      ),
    # Insertando slider con intervalo numérico en value
    sliderInput(inputId = "num",     
                label="Elige un número",
                value=c(5,25),
                min=1, 
                max=100,
    ),
    # Insertando slider con decimales y animación
    sliderInput("decimal", 
                "Decimal:",
                inputId = "num",
                min = 0,
                max = 1,
                value = 0.5,
                step = 0.1,
                animate = TRUE),
    checkboxGroupInput("icons", "Choose icons:",
                       choiceNames =
                           list(icon("calendar"), icon("bed"),
                                icon("cog"), icon("bug")),
                       choiceValues =
                           list("calendar", "bed", "cog", "bug")
    ),
    selectInput("type","Elige un tipo",
                choices = c("","A","B")),
    textInput(inputId = "title",
              label = "Título",
              value = "Histograma"),
    plotOutput("hist"),
    verbatimTextOutput("stats")
)
```

Definimos el server

```r
server <- function(input, output) {
  output$hist <- renderPlot({
      hist(rnorm(input$num),
           main=input$title)
  })
  output$stats <- renderPrint({
      summary(rnorm(input$num))
  })
}
```

Y finalmente corremos la aplicación.


```r
shinyApp(ui = ui, server = server)
```

### Etiquetas para modificar texto


```r
ui <- fluidPage(
  # Encabezados
  tags$h1("Encabezado de primer nivel"),
  tags$h2("Encabezado de segundo nivel"), 
  # Hipervínculos
  tags$a(href = "www.wintergenomics.com"), 
  # Parrafo nuevo
  tags$p("Mi primera app con Shiny"),
  tags$p("Mi primera pagina web con Shiny"),
  # Enfasis en texto
  tags$em("Texto en italicas"),
  tags$strong("Texto en negritas"),
  # Salto de línea
  tags$br(),
  # Texto con tipografía de código
  tags$code("Texto que indica que es código"),
  # Anidación de tags: Ejemplo: una palabra en negritas
  tags$p("Esta es", 
         tags$strong("palabra en negritas")),
  # Línea horizontal
  tags$hr(),
  # Agregar una imagen
  tags$img(height = 100, 
           width = 100, 
           src = "url_de_la_imagen/ruta_de_la_imagen")
)
```

Algunas funciones no necesitan el `tag`


```r
library(shiny)
ui <- fluidPage(
  h1("Mi Shiny App"), 
  p(style = "font-family:Impact",
    "Puedes ver algunas apps hechas con Shiny en",
    a("Apps de Shiny",
      href = "www.rstudio.com")
    
    # También puedes utilizar las etiquetas de HTML
    HTML(
      '<div class="container-fluids">
      <h1>Mi app de Shiny</h1>'
    )
)
```

### Conociendo paneles


```r
ui <- fluidPage(
    wellPanel(
        sliderInput(inputId= "num",
                    label= "Elige un número",
                    value= 25, min= 1, max = 100),
        textInput(inputId = "title",
                  label = "Escribe un título",
                  value ="Histograma de hasta 100 valores")
    ),
    plotOutput("hist"),
    verbatimTextOutput("stats")
)
```

Definimos el server

```r
server <- function(input, output) {
  output$hist <- renderPlot({
      hist(rnorm(input$num),
           main=input$title)
  })
  output$stats <- renderPrint({
      summary(rnorm(input$num))
  })
}
```

Y corremos la aplicación


```r
shinyApp(ui = ui, server = server)
```


## Crear una aplicación más compleja

Para esta app es necesario la librería `bslib`: 


```r
install.packages("bslib")
```


```r
library(shiny)
library(bslib)
```

### Personalizando con temas de bslib
Algunos de los temas disponibles son:

cerulean, cosmo, cyborg, darkly, flatly, journal, litera, lumen, lux, materia, minty, pulse, sandstone, simplex, sketchy, slate, solar, spacelab, superhero, united, yeti

En esta app usaremos el tema `"cerulean"` con la función `theme` de bslib. Con `tabsetPanel()` podemos agregar un panel en pestañas o tablas.


```r
# Definir UI
ui <- fluidPage(
		#Insertando un encabezado
                headerPanel("Random generator"),
                theme = bslib::bs_theme(bootswatch = "cerulean"),
                tabsetPanel(
                    tabPanel(
                             title = "Normal data",
                             plotOutput("norm"),
                             actionButton("renorm", "Resample")
                    ),
                    tabPanel(title = "Uniform data",
                             plotOutput("unif"),
                             actionButton("reunif", "Resample")
                    )
                )
)
```

Definimos servidor

```r
server <- function(input, output) {
    
    #Generar valores
    rv <- reactiveValues(
        norm = rnorm(500), 
        unif = runif(500)
        )
    #Generar valores normales
    observeEvent(input$renorm, { rv$norm <- rnorm(500) })
    #Generar valores uniformes
    observeEvent(input$reunif, { rv$unif <- runif(500) })
    #Generar historama de datos normales
    output$norm <- renderPlot({
        hist(rv$norm, breaks = 30, col = "grey", border = "white",
             main = "500 random draws from a standard normal distribution")
    })
    #Generar histograma de datos uniformes
    output$unif <- renderPlot({
        hist(rv$unif, breaks = 30, col = "grey", border = "white",
             main = "500 random draws from a standard uniform distribution")
    })

}
```

Corremos la aplicación

```r
shinyApp(server = server, ui = ui)
```


### Creando temas personalizados

Definimos la ui. Para crear nuestros temas personalizados utilizando diferentes colores, podemos revisar la siguiente guía de [colores](https://htmlcolorcodes.com/color-picker/).


```r
ui <- fluidPage(
                headerPanel("Random generator"),
                theme = bs_theme(
                   bg = "#405779", 
                   fg = "#FDF7F7", 
                   primary = "#ED79F9"),
                tabsetPanel(
                    tabPanel(
                             title = "Normal data",
                             plotOutput("norm"),
                             actionButton("renorm", "Resample")
                    ),
                    tabPanel(title = "Uniform data",
                             plotOutput("unif"),
                             actionButton("reunif", "Resample")
                    )
                )
)
```



Definimos servidor

```r
server <- function(input, output) {
    
    #Generar valores
    rv <- reactiveValues(
        norm = rnorm(500), 
        unif = runif(500)
        )
    #Generar valores normales
    observeEvent(input$renorm, { rv$norm <- rnorm(500) })
    #Generar valores uniformes
    observeEvent(input$reunif, { rv$unif <- runif(500) })
    #Generar historama de datos normales
    output$norm <- renderPlot({
        hist(rv$norm, breaks = 30, col = "grey", border = "white",
             main = "500 random draws from a standard normal distribution")
    })
    #Generar histograma de datos uniformes
    output$unif <- renderPlot({
        hist(rv$unif, breaks = 30, col = "grey", border = "white",
             main = "500 random draws from a standard uniform distribution")
    })

}
```

Corremos la aplicación

```r
shinyApp(server = server, ui = ui)
```
