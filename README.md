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

