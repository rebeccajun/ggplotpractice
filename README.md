# ggplot practice

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## Data Preparation

```{r mpg, echo=TRUE}
library(tidyverse)
summary(mpg)
str(mpg)
```

## Creating a ggplot

```{r mpg, echo=TRUE}
ggplot(data=mpg)+
  geom_point(mapping=aes(x=displ, y=hwy))
```


```{r mpg, echo=TRUE}
ggplot(data=mpg)+
  geom_point(mapping=aes(x=displ,y=hwy,color=class))
```

```{r mpg, echo=TRUE}
ggplot(data=mpg)+
  geom_point(mapping=aes(x=displ,y=hwy),color="blue")
```

## Facets
### facet_wrap(): To facet your plot by a single variable
```{r mpg, echo=TRUE}
ggplot(data=mpg)+
  geom_point(mapping=aes(x=displ,y=hwy))+
  facet_wrap(~ class, nrow=2)
```

### facet_grid(): To facet your plot on the combination of two variables
```{r mpg, echo=TRUE}
ggplot(data=mpg)+
  geom_point(mapping=aes(x=displ,y=hwy))+
  facet_grid(drv~cyl)
```

## Geometric Objects
```{r mpg, echo=TRUE}
# left
ggplot(data=mpg)+
  geom_point(mapping=aes(x=displ,y=hwy))

#right
ggplot(data=mpg)+
  geom_smooth(mapping=aes(x=displ,y=hwy))
```

```{r mpg, echo=TRUE}
ggplot(data=mpg)+
  geom_smooth(mapping=aes(x=displ,y=hwy,linetype=drv))
```

```{r mpg, echo=TRUE}
ggplot(data=mpg)+
  geom_smooth(mapping=aes(x=displ,y=hwy))
ggplot(data=mpg)+
  geom_smooth(mapping=aes(x=displ,y=hwy,group=drv))
ggplot(data=mpg)+
  geom_smooth(
    mapping=aes(x=displ,y=hwy,color=drv),
    show.legend=FALSE
  )
```

```{r mpg, echo=TRUE}
ggplot(data=mpg)+
  geom_point(mapping=aes(x=displ,y=hwy))+
  geom_smooth(mapping=aes(x=displ,y=hwy))
```

```{r mpg, echo=TRUE}
ggplot(data=mpg,mapping=aes(x=displ,y=hwy))+
  geom_point(mapping=aes(color=class))+
  geom_smooth()
```

```{r mpg, echo=TRUE}
ggplot(data=mpg,mapping=aes(x=displ,y=hwy))+
  geom_point(mapping=aes(color=class))+
  geom_smooth(
    data=filter(mpg,class=="subcompact"),
    se=FALSE
  )
```

## Statistical Transformations
```{r mpg, echo=TRUE}
ggplot(data=diamonds)+
  geom_bar(mapping=aes(x=cut))

ggplot(data=diamonds)+
  stat_count(mapping=aes(x=cut))
```

```{r mpg, echo=TRUE}
ggplot(data=diamonds)+
  stat_summary(
    mapping=aes(x=cut,y=depth),
    fun.ymin=min,
    fun.ymax=max,
    fun.y=median
  )
```

## Position Adjustments
```{r mpg, echo=TRUE}
ggplot(data=diamonds)+
  geom_bar(mapping=aes(x=cut,color=cut))
ggplot(data=diamonds)+
  geom_bar(mapping=aes(x=cut,fill=cut))
```

```{r mpg, echo=TRUE}
ggplot(data=diamonds)+
  geom_bar(mapping=aes(x=cut,fill=clarity))
```

```{r mpg, echo=TRUE}
ggplot(data=diamonds)+
  geom_bar(
    mapping=aes(x=cut, fill=clarity),
    position="fill"
  )
```

```{r mpg, echo=TRUE}
ggplot(data=diamonds)+
  geom_bar(
    mapping=aes(x=cut,fill=clarity),
    position="dodge"
  )
```

position = "jitter" adds a small amount of random noise to each point. This spreads the points out because no two points are likely to receie the same amount of random noise:
```{r mpg, echo=TRUE}
ggplot(data=mpg)+
  geom_point(
    mapping=aes(x=displ,y=hwy),
    position="jitter"
  )
```

## Coordinate Systems
```{r mpg, echo=TRUE}
ggplot(data=mpg,mapping=aes(x=class,y=hwy))+
  geom_boxplot()

ggplot(data=mpg,mapping=aes(x=class,y=hwy))+
  geom_boxplot()+
  coord_flip()
```

```{r mpg, echo=TRUE}
nz <- map_data("nz")

ggplot(nz, aes(long,lat,group=group))+
  geom_polygon(fill="white",color="black")

ggplot(nz, aes(long, lat, group = group)) +
  geom_polygon(fill = "white", color = "black") +
  coord_quickmap()
```

```{r mpg, echo=TRUE}
bar <- ggplot(data=diamonds)+
  geom_bar(
    mapping=aes(x=cut,fill=cut),
    show.legend=FALSE,
    width=1
  )+
  theme(aspect.ratio=1)+
  labs(x=NULL,y=NULL)

bar+coord_flip()
bar+coord_polar()
```

```{r mpg, echo=TRUE}
ggplot(data=mpg, mapping=aes(x=cty,y=hwy))+
  geom_point()+
  geom_abline()+
  coord_fixed()
```

