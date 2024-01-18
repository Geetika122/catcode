install.packages("RSQLite")
library("RSQLite")
#CROP_DATA:
df1 <- dbExecute(conn, 
                    "CREATE TABLE CROP_DATA (
                                      CD_ID INTEGER NOT NULL,
                                      YEAR DATE NOT NULL,
                                      CROP_TYPE VARCHAR(20) NOT NULL,
                                      GEO VARCHAR(20) NOT NULL, 
                                      SEEDED_AREA INTEGER NOT NULL,
                                      HARVESTED_AREA INTEGER NOT NULL,
                                      PRODUCTION INTEGER NOT NULL,
                                      AVG_YIELD INTEGER NOT NULL,
                                      PRIMARY KEY (CD_ID)
                                      )", 
                    errors=FALSE
                    )

    if (df1 == -1){
        cat ("An error has occurred.\n")
        msg <- odbcGetErrMsg(conn)
        print (msg)
    } else {
        cat ("Table was created successfully.\n")
    }
#Farm_Product_prices:
df2 <- dbExecute(conn, 
                    "CREATE TABLE FARM_PRICES (
                                     CD_ID INTEGER NOT NULL,
                                      YEAR DATE NOT NULL,
                                      CROP_TYPE VARCHAR(20) NOT NULL,
                                      GEO VARCHAR(20) NOT NULL,
                                      PRICE_PERMIT NOT NULL,
                                      PRIMARY KEY (CD_ID)   


)", 
                    errors=FALSE
                    )

    if (df2 == -1){
        cat ("An error has occurred.\n")
        msg <- odbcGetErrMsg(conn)
        print (msg)
    } else {
        cat ("Table was created successfully.\n")
    }
    
    #Daily_FX:
df3 <- dbExecute(conn, 
                    "CREATE TABLE DAILY_FX (
                                      DFX_ID INTEGER NOT NULL,
                                      YEAR DATE NOT NULL,
                                      FXUSDCAD VARCHAR(20) NOT NULL,
                                      PRIMARY KEY (DFX_ID)
                                      )", 
                    errors=FALSE
                    )

    if (df3 == -1){
        cat ("An error has occurred.\n")
        msg <- odbcGetErrMsg(conn)
        print (msg)
    } else {
        cat ("Table was created successfully.\n")
    }
    #MONTHLY_FX:
df4 <- dbExecute(conn, 
                    "CREATE TABLE MONTHLY_FX (
                                      DFX_ID INTEGER NOT NULL,
                                      YEAR DATE NOT NULL,
                                      FXUSDCAD VARCHAR(20) NOT NULL,
                                      PRIMARY KEY (DFX_ID)
                                      )", 
                    errors=FALSE
                    )

    if (df4 == -1){
        cat ("An error has occurred.\n")
        msg <- odbcGetErrMsg(conn)
        print (msg)
    } else {
        cat ("Table was created successfully.\n")
    }

    # Write your query here
crop_df <- read.csv('Annual_Crop_Data.csv')
farm_df <- read.csv('Monthly_Farm_Prices.csv')
daily_df <- read.csv('Daily_FX.csv')
monthly_df <- read.csv('Monthly_FX.csv')

head(crop_df)
head(farm_df)
head(daily_df)
head(monthly_df)


# Write your query here
dbGetQuery(conn, 'SELECT COUNT(CD_ID) FROM Farm_Prices')
     


# Write your query here
 dbGetQuery(conn, 'SELECT DISTINCT(GEO) FROM FARM_PRICES')
     
query <- "select SUM(HARVESTED_AREA)
            FROM CROP_DATA
            WHERE GEO = 'CANADA' AND
            YEAR(YEAR) = 1968 AND 
            CROP_TYPE = 'RYE';"
view <- sqlQuery(conn, query)
view
     
