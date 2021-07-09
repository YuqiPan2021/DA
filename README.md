# DA
```{r}
library(tidyverse)
library(skimr)
library(janitor)
library(moderndive)
library(infer)
library(broom)
library(knitr)
library(gridExtra)
library(GGally)
library(kableExtra)
library(corrplot)
library(RColorBrewer)
library(car)
library(forcats)
library(ggfortify)
```
This is some test.

```{r data, echo = FALSE, eval = TRUE, warning = FALSE}
world <- read.csv("Group_13.csv")
glimpse(world)
```
```{r summaries, echo = FALSE, eval = TRUE, warning = FALSE}
happiness <- world %>% select(-c(1,2))
#head(happiness)
happiness %>%
  skim() %>%
  select(c(2,5,6,7,9,11)) %>%
  kable(col.names=c("Variables","Mean","SD","Min","Median","Max"),
          booktabs=TRUE, linesep="", digits=2, caption = 
          '\\label{tab:summaries} Summary statistics on all numerical variables') %>%
  kable_styling(font_size=10, latex_options="HOLD_position")
```

```{r map, echo = FALSE, eval = TRUE, fig.width=12, fig.height=6, fig.align = "center", fig.pos = "H", warning = FALSE, fig.cap = "\\label{fig:map} Map of Happiness Socore by Countries"}
world[19,1] <- "USA"; world[24,1] <- "Taiwan"; world[83,1] <- "Republic of Congo";
world[17,1] <- "UK"
worldn <- world %>%
  right_join(map_data("world"), by=c("Country.name"="region"))
worldn[is.na(worldn)] <- 5
country_map <- map_data("world") 
ggplot(worldn, aes(map_id = Country.name)) +
  geom_map(aes(fill=Happiness.score), map=country_map, colour="gray50", size=0.5) + 
  scale_fill_distiller(palette = "RdBu",direction= -1) + 
  expand_limits(x = country_map$long, y = country_map$lat) +  
  labs(x = "Longitude", y = "Latitude")
```

