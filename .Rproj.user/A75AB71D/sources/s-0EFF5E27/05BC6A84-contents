#### Introduction to Tidyverse

####
## Section 1 - Data Wrangling
####

#load gapminder package
#install.packages("gapminder")
library(gapminder)
library(dplyr)
gapminder #show the dataset which is a tibble

#dataset has - country, continent, year, lifeExp, pop, gdpPercap

#filter verb
#to filter to show only records from year 2007, does not remove data
gapminder %>% filter(year == 2007)

#filter observations from United States
gapminder %>% filter(country == "United States")

#multiple conditions - resulting in a single observation
gapminder %>% filter(year == 2007, country == "United States")

#arrange verb
#arrange sorts a table based on a variable in ascending or descending
gapminder %>% arrange(gdpPercap)
#to display in descending order
gapminder %>% arrange(desc(gdpPercap))

#filter then arranging
gapminder %>%
  filter(year == 2007) %>%
  arrange(desc(gdpPercap))

#mutate verb
#mutate changes or adds variables 
gapminder %>%
  mutate(pop = pop / 1000000)

#mutate to add new variable
gapminder %>%
  mutate(gdp = gdpPercap * pop)

#putting it all together - to know which country has the highest GDP in 2007
gapminder %>%
  mutate(gdp = gdpPercap * pop) %>%  # create new column
  filter(year == 2007) %>%  # filter records to 2007 only
  arrange(desc(gdp))  # show by descending GDP


####
# Section 2 - Visualising with ggplot2
####

#load ggplot2 library
library(ggplot2)

#variable assignment
gapminder_2007 <- gapminder %>%
  filter(year == 2007)
gapminder_2007

#creating the scatter plot, specifying the aesthetic components
g <- ggplot(gapminder_2007, aes(x=gdpPercap, y=lifeExp))
#specifying the aesthetic
g + geom_point()

#log scales
g + geom_point() + scale_x_log10()

#additional aesthetics
f <- ggplot(gapminder_2007, aes(x=gdpPercap, y=lifeExp, color=continent))
f + geom_point() + scale_x_log10()

#changing aesthetics
h <- ggplot(gapminder_2007, aes(x=gdpPercap, y=lifeExp, color=continent, size=pop))
h + geom_point() + scale_x_log10()

#faceting
i <- ggplot(gapminder_2007, aes(x=gdpPercap, y=lifeExp))
i + geom_point() + scale_x_log10() + facet_wrap(~ continent) #split by continent


####
# Section 3 - Grouping and Summarizing
####

#summarize verb
#summaizes by turning many rows into one'
gapminder %>% 
  summarize(meanLifeExp = mean(lifeExp))  # does not work

#summarizing for one year
gapminder %>%
  filter(year == 2007) %>%
  summarize(meanLifeExp = mean(lifeExp))

#summarizing into mulitple columns
gapminder %>%
  filter(year == 2007) %>%
  summarize(meanLifeExp = mean(lifeExp), 
            totalPop = sum(pop))

#functions usable for summarizing
#mean(), sum(), median(), min(), max()

#group_by verb
#summarizing by year
gapminder %>%
  group_by(year) %>%
  summarize(meanLifeExp = mean(lifeExp),
            totalPop = sum(pop))

#summarizing by continent
gapminder %>%
  filter(year == 2007) %>%
  group_by(continent) %>%
  summarize(meanLifeExp = mean(lifeExp),
            totalPop = sum(pop))

#summarizing by continent and year
gapminder %>%
  group_by(year, continent) %>%
  summarize(meanLifeExp = mean(lifeExp),
            totalPop = sum(pop))

#visualizing summarized data
#summarizing by year
by_year <- gapminder %>%
  group_by(year) %>%
  summarize(totalPop = sum(pop),
            meanLifeExp = mean(lifeExp))
by_year

#visualising over time
j <- ggplot(by_year, aes(x=year, y=totalPop))
j + geom_point()

#starting y-axis at zero
j + geom_point() + expand_limits(y = 0)

#summarizing by year and continent
by_year_continent <- gapminder %>%
  group_by(year, continent) %>%
  summarize(totalPop = sum(pop),
            meanLifeExp = mean(lifeExp))
by_year_continent

#visualising  by year and continent
k <- ggplot(by_year_continent, aes(x=year, y=totalPop, color=continent))
k + geom_point() + expand_limits(y = 0)


####
# Section 4 - Types of Visualization
####

#line plots - useful for showing change over time
#bar plot - good for comparing statistics for each of several categories
#histograms - describe distribution of a 1-dimensional variable
#boxplot - compare the distribution of a numeric variable among several categories
#scatter plot good for comparing 2 variables
#scatter vs line plot
l <- ggplot(by_year_continent, aes(x=year, y=meanLifeExp, color=continent))
l + geom_line() + expand_limits(y=0)

#barplots
#useful for comparing values across discrete categories, such as continents
#summarizing by continent
by_continent <- gapminder %>%
  filter(year == 2007) %>%
  group_by(continent) %>%
  summarize(meanLifeExp = mean(lifeExp))
by_continent

m <- ggplot(by_continent, aes(x=continent, y=meanLifeExp))
m + geom_col()

#histograms
#allows the investigation of one dimension of data at a time
#and has only one aesthetic, the x-axis
n <- ggplot(gapminder_2007, aes(x=lifeExp))
n + geom_histogram()

#customizing the width of the bin
n + geom_histogram(binwidth = 5)  # each bin is 5 years

#boxplots
#allows us to compare distribution against another variable
o <- ggplot(gapminder_2007, aes(x=continent, y=lifeExp, color=continent))
o + geom_boxplot()

p <- ggplot(gapminder_2007, aes(x = continent, y = gdpPercap, color=continent))
p + geom_boxplot() + scale_y_log10() + 
  labs(title="Comparing GDP per capita across continents")


####
# the end
####

# - data visualisation with ggplot2
# - data manipuation with dplyr
# - importing and cleaning data
# - exploratoy data analysis in R; case study