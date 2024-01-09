install.packages("RSQLite")
library("RSQLite")
df1 <- dbExecute(conn, "CREATE TABLE Annual_CROP_DATA (
                            CD_ID CHAR(8) NOT NULL, 
                            B_NAME VARCHAR(75) NOT NULL, 
                            TYPE VARCHAR(5384) NOT NULL, 
                            LANGUAGE VARCHAR(50), 
                            PRIMARY KEY (CD_ID))", 
                errors=FALSE)
