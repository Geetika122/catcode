# This lab requires 'httr' and 'rvest'packages, which are already pre-loaded into this lab environment.
# However, if you are working on your local RStudio, please uncomment the below codes and install the packages.

#install.packages("httr")
#install.packages("rvest")
library(httr) 
library(rvest)
response <- GET("https://en.wikipedia.org/w/index.php?title=Template:COVID-19_testing_by_country")  
return(response)
get_wiki_covid19_page <- function() {
    wiki_base_url <- "https://en.wikipedia.org/w/index.php?"
    query_param <- "title=Template:COVID-19_testing_by_country"
    response <- GET (wiki_base_url,query=query_param)
    return(response)
   } 
   Covid19<- get_wiki_covid19_page()
Covid19
# Get the root html node from the http response in task 1 
root_node <- read_html(get_wiki_covid19_page())

root_node
# Get the table node from the root html node
table_node <- html_nodes(root_node,"table")
# Read the table node and convert it into a data frame, and print the data frame for review
the_url <- "https://en.wikipedia.org/w/index.php?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkRP0101ENCoursera23911160-2021-01-01&title=Template%3ACOVID-19_testing_by_country"

covid <- the_url %>%
  read_html() %>% 
  html_table(fill=TRUE)

covid[[2]]
# Print the summary of the data frame
summary(data_frame)
table_node
