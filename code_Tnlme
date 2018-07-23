# Function used to turn multiple lme models results in to table for word
# I call it Tlme because it turns lme() results into a table

# Library -----------------------------------------------------------------
library(tidyverse)
library(dplyr)
library(tidyr)
library(broom)

datum <- read.csv("data/Cleaned/Shadecover.csv")

# Create model and store as "Z1"
Z1 <- lme(n ~ k, data = datum, random = ~1|j.)

# Tlme Function -----------------------------------------------------------
## This Tlme ver. 1.0 function will combine the results from lme
Tlme <- function(x, y) {
  
  # Calculates the F-statistic for the model
  F_stat <- as.data.frame(anova(x, type = "marginal"))
  colnames(F_stat) <- c("var", "df", "F", "p-value")
  F_stat <- F_stat %>%  select(df, F)
  as.tibble(F_stat)
  
  # cbind (column bind) df and F to estimate and std error
  tab<- cbind(tidy(x, effects = "fixed"), #specify fixed effect to get the summary              
                  F_stat) %>% #bind it with tidy anova data values
    mutate(model = y) %>% 
    mutate_at(vars(c("estimate", "std.error", "df", "F", "p.value")), funs(round(., 3))) %>% 
    filter(!term %in% c("(Intercept)", ("sd_(Intercept).Plot"))) %>% 
    select(model, term, df, estimate, std.error, F, p.value)
  

}

# Use 
Tlme(x)

## Bind using rbind()
table <- rbind(Z1, Z1) #where Z1 and Z2 are models
table <- table %>% 
  arrange(term)
  
write.table(table, file = "nesttable.txt", sep = ",", quote = FALSE, row.names = F)
