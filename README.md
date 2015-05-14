# Source & Raw Data
Official web site : http://www.epa.gov/ttn/chief/eiinformation.html
Raw data : https://d396qusza40orc.cloudfront.net/exdata%2Fdata%2FNEI_data.zip

#Introduction 
There is 6 scripts that will try to show answers for the following questions :
1. Have total emissions from PM2.5 decreased in the United States from 1999 to 2008? Using the base plotting system, make a plot showing the total PM2.5 emission from all sources for each of the years 1999, 2002, 2005, and 2008.
2. Have total emissions from PM2.5 decreased in the Baltimore City, Maryland (fips == "24510") from 1999 to 2008? Use the base plotting system to make a plot answering this question.
3. Of the four types of sources indicated by the type (point, nonpoint, onroad, nonroad) variable, which of these four sources have seen decreases in emissions from 1999–2008 for Baltimore City? Which have seen increases in emissions from 1999–2008? Use the ggplot2 plotting system to make a plot answer this question.
4. Across the United States, how have emissions from coal combustion-related sources changed from 1999–2008?
5. How have emissions from motor vehicle sources changed from 1999–2008 in Baltimore City?
6.Compare emissions from motor vehicle sources in Baltimore City with emissions from motor vehicle sources in Los Angeles County, California (fips == "06037"). Which city has seen greater changes over time in motor vehicle emissions?


# Source File analysis
## "summarySCC_PM25.rds" 
str(NEI)
'data.frame':	6497651 obs. of  6 variables:
 $ fips     : chr  "09001" "09001" "09001" "09001" ...
 $ SCC      : chr  "10100401" "10100404" "10100501" "10200401" ...
 $ Pollutant: chr  "PM25-PRI" "PM25-PRI" "PM25-PRI" "PM25-PRI" ...
 $ Emissions: num  15.714 234.178 0.128 2.036 0.388 ...
 $ type     : chr  "POINT" "POINT" "POINT" "POINT" ...
 $ year     : int  1999 1999 1999 1999 1999 1999 1999 1999 1999 1999 ...

*fips: A five-digit number (represented as a string) indicating the U.S. county
*SCC: The name of the source as indicated by a digit string (see source code classification table)
*Pollutant: A string indicating the pollutant
*Emissions: Amount of PM2.5 emitted, in tons
*type: The type of source (point, non-point, on-road, or non-road)
*year: The year of emissions recorded

> head(NEI)
    fips      SCC Pollutant Emissions  type year
4  09001 10100401  PM25-PRI    15.714 POINT 1999
8  09001 10100404  PM25-PRI   234.178 POINT 1999
12 09001 10100501  PM25-PRI     0.128 POINT 1999
16 09001 10200401  PM25-PRI     2.036 POINT 1999
20 09001 10200504  PM25-PRI     0.388 POINT 1999
24 09001 10200602  PM25-PRI     1.490 POINT 1999

##"Source_Classification_Code.rds"
> str(SCC)
'data.frame':	11717 obs. of  15 variables:
 $ SCC                : Factor w/ 11717 levels "10100101","10100102",..: 1 2 3 4 5 6 7 8 9 10 ...
 $ Data.Category      : Factor w/ 6 levels "Biogenic","Event",..: 6 6 6 6 6 6 6 6 6 6 ...
 $ Short.Name         : Factor w/ 11238 levels "","2,4-D Salts and Esters Prod /Process Vents, 2,4-D Recovery: Filtration",..: 3283 3284 3293 3291 3290 3294 3295 3296 3292 3289 ...
 $ EI.Sector          : Factor w/ 59 levels "Agriculture - Crops & Livestock Dust",..: 18 18 18 18 18 18 18 18 18 18 ...
 $ Option.Group       : Factor w/ 25 levels "","C/I Kerosene",..: 1 1 1 1 1 1 1 1 1 1 ...
 $ Option.Set         : Factor w/ 18 levels "","A","B","B1A",..: 1 1 1 1 1 1 1 1 1 1 ...
 $ SCC.Level.One      : Factor w/ 17 levels "Brick Kilns",..: 3 3 3 3 3 3 3 3 3 3 ...
 $ SCC.Level.Two      : Factor w/ 146 levels "","Agricultural Chemicals Production",..: 32 32 32 32 32 32 32 32 32 32 ...
 $ SCC.Level.Three    : Factor w/ 1061 levels "","100% Biosolids (e.g., sewage sludge, manure, mixtures of these matls)",..: 88 88 156 156 156 156 156 156 156 156 ...
 $ SCC.Level.Four     : Factor w/ 6084 levels "","(NH4)2 SO4 Acid Bath System and Evaporator",..: 4455 5583 4466 4458 1341 5246 5584 5983 4461 776 ...
 $ Map.To             : num  NA NA NA NA NA NA NA NA NA NA ...
 $ Last.Inventory.Year: int  NA NA NA NA NA NA NA NA NA NA ...
 $ Created_Date       : Factor w/ 57 levels "","1/27/2000 0:00:00",..: 1 1 1 1 1 1 1 1 1 1 ...
 $ Revised_Date       : Factor w/ 44 levels "","1/27/2000 0:00:00",..: 1 1 1 1 1 1 1 1 1 1 ...
 $ Usage.Notes        : Factor w/ 21 levels ""," ","includes bleaching towers, washer hoods, filtrate tanks, vacuum pump exhausts",..: 1 1 1 1 1 1 1 1 1 1 ...
 
> head(SCC)
       SCC Data.Category                                                                 Short.Name
1 10100101         Point                   Ext Comb /Electric Gen /Anthracite Coal /Pulverized Coal
2 10100102         Point Ext Comb /Electric Gen /Anthracite Coal /Traveling Grate (Overfeed) Stoker
3 10100201         Point       Ext Comb /Electric Gen /Bituminous Coal /Pulverized Coal: Wet Bottom
4 10100202         Point       Ext Comb /Electric Gen /Bituminous Coal /Pulverized Coal: Dry Bottom
5 10100203         Point                   Ext Comb /Electric Gen /Bituminous Coal /Cyclone Furnace
6 10100204         Point                   Ext Comb /Electric Gen /Bituminous Coal /Spreader Stoker
                               EI.Sector Option.Group Option.Set               SCC.Level.One
1 Fuel Comb - Electric Generation - Coal                         External Combustion Boilers
2 Fuel Comb - Electric Generation - Coal                         External Combustion Boilers
3 Fuel Comb - Electric Generation - Coal                         External Combustion Boilers
4 Fuel Comb - Electric Generation - Coal                         External Combustion Boilers
5 Fuel Comb - Electric Generation - Coal                         External Combustion Boilers
6 Fuel Comb - Electric Generation - Coal                         External Combustion Boilers
        SCC.Level.Two               SCC.Level.Three                                SCC.Level.Four Map.To
1 Electric Generation               Anthracite Coal                               Pulverized Coal     NA
2 Electric Generation               Anthracite Coal             Traveling Grate (Overfeed) Stoker     NA
3 Electric Generation Bituminous/Subbituminous Coal Pulverized Coal: Wet Bottom (Bituminous Coal)     NA
4 Electric Generation Bituminous/Subbituminous Coal Pulverized Coal: Dry Bottom (Bituminous Coal)     NA
5 Electric Generation Bituminous/Subbituminous Coal             Cyclone Furnace (Bituminous Coal)     NA
6 Electric Generation Bituminous/Subbituminous Coal             Spreader Stoker (Bituminous Coal)     NA
  Last.Inventory.Year Created_Date Revised_Date Usage.Notes
1                  NA                                      
2                  NA                                      
3                  NA                                      
4                  NA                                      
5                  NA                                      
6                  NA 
 
## common key
SCC is the common key between "summarySCC_PM25.rds" and "Source_Classification_Code.rds"


## The tidy data set 


