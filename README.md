## Simple Gantt chart in R

#### Code

``` R
library("ggplot2")
library("tidyr")

# Timeline data
timeline = read.csv("timeline.csv", stringsAsFactors = FALSE)
timeline$name = factor(timeline$name, levels = rev(timeline$name)) # Preserve the order of the steps in the csv

timeline = pivot_longer(timeline, cols = start:end, names_to = "time") # Needed modification for ggplot

# Where the x-axis labels should be placed and what they should say
labels <- read.csv("labels.csv", stringsAsFactors = FALSE)

# Plot
ggplot(timeline, aes(value, name)) +
  geom_vline(xintercept = 1, linetype = "dashed", colour = "red") + # How to add vertical line for important dates/milestones
  geom_line(size = 5) +
  annotate("text", x = c(1), y = c(1),
           label = c("Important Milestone"),
           fontface = 3, size = 3, color = "red") + # Annotations for one or more items. In this case, it's for the vertical line
  labs(x = "Timeline", y = NULL, title = "Project timeline") +
  scale_x_continuous(breaks = labels$x, labels = labels$lab) +
  theme_classic() +
  theme(axis.text.y = element_text(hjust = 0)) + # Left aligns y-axis labels
  coord_fixed(ratio = 0.25) # Essentially compresses the graph vertically


ggsave("gantt.png", width = 7, height = 3) # Set dimensions to how big the figure should be if printed (default: inches)
  
```

#### Output

![](./gantt.png)
