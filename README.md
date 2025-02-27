"# Assignment" 
# Project title
Assignment on data handling

## Overview
Used data from Tidytuesday to practice on the aspects taught.

## Contents
Load up dataset

1. Load up the dataset you wish to work on. The dataset is gotten from GitHub tidytuesday

call in the package to read the data. Since it is a csv data, library(readr) was used.

load up the data by copy pasting the link generated from GitHub

library(readr) volcano <- read_csv("//storage.slu.se/home_2$/ador0002/Desktop/Finalized/tidytuesday/data/2020/2020-05-12/volcano.csv") View(volcano)

2. Load up the packages needed to work on the dataset

library(tidyverse)

library(sf)

library(tmap)

3. Take a quick overview on all the dataset at a glimpse

glimpse(volcano)

Group the selected headings and get the mean

Rename the selected headings

volcano3 <- volcano2 %>% group_by (primary_volcano_type,name)%>% summarise(population= mean(value)) colnames (volcano3)[1] = "type" colnames (volcano3)[2] = "distance"

4. Arrange and rename columns needed

#volcano3 <- as.data.frame(volcano2) %>% arrange (primary_volcano_type,name)#colnames (volcano3)[1] = "type" #colnames (volcano3)[2] = "population"

5. Selection of some column

volcano4 <- volcano3[c(1:4, 9:12, 17:20),]

6. Plotting a boxplot using the data from volcano4

ggplot(volcano4, aes(x = type, y = population)) + geom_boxplot()

7. Add colours to the plotted boxplot

ggplot(volcano4, aes(x = type, y = population, fill = type)) + geom_boxplot() + scale_fill_manual(values = c("black", "brown", "gold"))

8. Plotting a geom_col and differentiate with colours using the data from volcano4

ggplot(volcano4, aes(x = type, y = population, fill = distance)) + geom_col(position = "dodge") + scale_fill_manual(values = c("blue", "brown","black", "gold"))

9. Plotting a geom_density and differentiate with colours using the data from volcano4

ggplot(volcano4, aes(x = population, color = type, fill = type)) + geom_density(alpha = 0.5)

10. Plotting a geom_point and differentiate with colours using the data from volcano4

ggplot(volcano4, aes(x = type, y = population, colour = type, shape = type)) + geom_point()

11. Call in a package you intend to work

library(cowplot)

12. Rename columns needed

a <- ggplot(volcano4, aes(x = type, y = population)) + geom_boxplot() b <- ggplot(volcano4, aes(x = type, y = population, fill = distance)) + geom_col(position = "dodge") + scale_fill_manual(values = c("blue", "brown","black", "gold")) c <- ggplot(volcano4, aes(x = population, color = type, fill = type)) + geom_density(alpha = 0.5) d <- ggplot(volcano4, aes(x = type, y = population, colour = type, shape = type)) + geom_point()

13. Arrange all plots into one frame

plot_grid(a, b, c, d, nrow = 2, ncol = 2)

14. Differentiate with label

library(cowplot) plot_grid(a, b, c, d, nrow = 2, ncol = 2, labels=c("A", "B", "C", "D"))

15. Group preferred columns to work on

volcano5 <- subset(volcano, select = c(2,5:6,8:9,23:26))

16. Make selected columns longer

volcano6 <- pivot_longer(volcano5, cols = c("population_within_5_km", "population_within_10_km", "population_within_30_km", "population_within_100_km"))

17. Group preferred columns to work on

volcano7 <- subset(volcano6, select = c(1:2,4:5))

18. Load up the packages needed to create the map

library(geometry)

19. Load up the packages needed to create the map

library(rnaturalearth) world_map <- ne_countries(scale = "medium", returnclass = "sf")

20. Create the map using geom_point

volcanomap<-ggplot(volcano6, aes(x = longitude, y = latitude, group = name)) + geom_point(aes(fill = value, colour = region)) print(volcanomap)

21. Load up the packages needed to create a map

library(rnaturalearth)

22. Select specific rows

volcanomap_data <- volcano6[c(1:24),]

23. Create sf object

volcanomap_data <- volcano6 %>% st_as_sf(coords = c("longitude", "latitude"),

crs=st_crs(world_map))

24. Create a map

ggplot() + geom_sf(data = world_map, fill = NA, colour = "red")+ geom_sf(data = volcanomap_data)

25. Adjust the colour for better visibility

ggplot() + geom_sf(aes(geometry = world_map$geometry))+ geom_sf(data = world_map, fill = NA, colour = "blue") + geom_sf(data = volcanomap_data)


Challenges include

had no knowledge of R studio before the class

difficulty loading up the dataset from Github

large dataset hence understanding it was a serious challenge

Rendering was a big challenge as mine was not rendering in full


knowledge gain

the use of R studio being an entirely new experience for me, everything I was able to come up with and any further improvements are all new knowledge I have gain.


Thank you!!!
