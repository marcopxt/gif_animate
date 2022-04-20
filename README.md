# gif_animate
Script for animate gifs - PCA example

#### 1. Library

##### The packages that we will use
```
library(ggplot2)
library(gganimate)
library(gifski)
library(dplyr)
library(tidyr)
```

#### 2. The data
##### Reading the dataset
```
dat_f1=read.table("dat.txt", h=TRUE)

head(dat_f1)

              PC1        PC2 Yr
11861 -16.3199766   5.378733  1
10547  -8.4177069  10.995337  1
9271   16.3844172   2.373787  1
12582   0.4429941  -8.940353  1
10910   2.5347552   7.263499  1
11059  -5.7668394 -10.466436  1
```

#### 3. Creat the PCA plot

```
animat = ggplot(dat_f1, aes(PC1, PC2, col=Yr)) +
              geom_point() +
              scale_colour_viridis_c() +
              theme(panel.grid.minor = element_blank(),
                   panel.grid.major.y = element_blank(),
                   panel.grid.major.x = element_blank(),
                   plot.title = element_text(size = 18, 
                                            hjust = 0.5, 
                                             face = "bold", 
                                           colour = 'blue'),
                   legend.title = element_blank(),
                   legend.text = element_blank(),
                   legend.position = "none",
                   legend.key = element_blank(),
                   axis.text = element_text(size = 15, colour = "black"),
                   axis.title = element_text(size = 18),
                   strip.text = element_text(face = "bold", 
                                             size = 20, 
                                           colour = 'blue'))+
             labs(title = 'Year: {frame_time}', x = 'PC1(6.61%)', y = 'PC2(2.70%)') +
             transition_time(Yr) +
             ease_aes('linear')
```

#### 4. Render the animation
```
anim = animate(animat, 
               height = 4.5, 
               width = 8, 
               units = "in", 
               res = 200,
               end_pause = 30, 
               renderer = gifski_renderer())
```

#### 5. Saving the animation
```
anim_save("Gif10.gif", anim)
```

#### 6. Gif generated
```
>> Gif10.gif
```

![Gif10](https://user-images.githubusercontent.com/59318360/164309215-be3d7f5a-5024-4784-b30c-220c5b0b3e66.gif)


