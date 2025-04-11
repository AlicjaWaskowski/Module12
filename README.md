# Module12
---
title: "CyberSecAnalyze"
author: "Alicja Waskowski"
date: "2025-04-11"
output: html_document
---


```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
library(dplyr)
library(ggplot2)
```

## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

```
## Function: Summarize Incidents

**Purpose:**  
Summarize the number of incidents grouped by a variable (e.g., year).

**Inputs:**  
- `data`: A data frame containing cybersecurity incident data.
- `group_var`: A column to group by (e.g., `year`, `AttackType`).

**Output:**  
- A data frame with the counts of incidents for each group.

```{r}
summarize_incidents <- function(cyber_data, group_var) {
  data %>%
    group_by({{ group_var }}) %>%
    summarise(incident_count = n(), .groups = 'drop')
}
```

```{r}
#Example usage of summary_incidents
incident_summary <- summarize_incidents(cyber_data, year)
```

## Function: Filter by Attack Type

**Purpose:**  
Filter the dataset to include only incidents of a specific attack type.

**Inputs:**  
- `data`: A data frame containing cybersecurity incident data.
- `attack_type`: The attack type to filter by (e.g., `"Phishing"`, `"Malware"`).

**Output:**  
- A data frame filtered to include only rows where the `AttackType` matches the specified `attack_type`.

```{r}
filter_by_type <- function(cyber_data, attack_type) {
  data %>%
    filter(AttackType == attack_type)
}
```

```{r}
#Example usage of filter_by_type
phishing_attacks <- filter_by_type(cyber_data, "Phishing")
```

## Function: Plot Attack Trends

**Purpose:**  
Creates a line chart to show the trend of cybersecurity incidents over time or across categories.

**Inputs:**  
- `summary_data`: A data frame summarizing the incidents (e.g., grouped by year or attack type).
- `x_var`: The variable to be plotted on the x-axis (e.g., `year`).
- `y_var`: The variable to be plotted on the y-axis (e.g., `incident_count`).

**Output:**  
- A `ggplot` object displaying a line chart visualizing the trend of cybersecurity incidents.

```{r}
plot_attack_trends <- function(summary_data, x_var, y_var) {
  ggplot(summary_data, aes(x = {{ x_var }}, y = {{ y_var }})) +
    geom_line(color = "steelblue", size = 1.2) +
    geom_point(color = "black") +
    theme_minimal() +
    labs(title = "Cybersecurity Attack Trends", x = "Year", y = "Number of Incidents")
}
```

```{r}
#Example usage of plot_attack_trends
plot_attack_trends(incident_summary, year, incident_count)

```

