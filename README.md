
#SST Wadden Sea ![Wadden Sea](https://github.com/gabrielamg24/SST/blob/extras/waddensea.jpg)

##Sea Surface Temperature throughout time
###Python program that generates a video from color temperature based maps by running an R-script on data of sea surface temperature (SST) in the Wadden Sea 
==================
##Index
  - [Usage](#usage)
    - [Python](#python)
    - [R script](#r-script)
    - [How to](#how-to)
  - [Temperature map](#temperature-map)
  - [Features and advantages of this project](#features-and-advantages-of-this-project)
    - [Challenges](#challenges)
  - [Are we missing something?](#are-we-missing-something)
  - [License](#license)

---
##Usage 
(paste python script) 


gif

![](https://github.com/gabrielamg24/SST/blob/master/ggplot2-brownian-motion.gif)

###Python

          #! /usr/bin/env python

          #This programs  reads a file containing values of sea surface temperature (SST) from the Wadden Sea across a set of   coordinates and years it normalizes the data by using regular expression, joins files, and creates a .gif out of temperature-based color maps generates by R program 


          #Load regular expression module as well as glob that finds pathnames with a pattern

          import re
          import glob

          #Open a new file in format .txt where we will save the output lines from all other files
          #The header is also stated in format csv 
          Header = 'Latitude,Longitude,Year.Month,Temperature\n'
          data = open("All_data.txt",'w')
          data.write(Header)
          data.close()

          #For loop that goes through every line of all the .csv files 
          #With regular expression latitude and longitude are taken from the first line of each file and put into two new columns to               each line of each file, so that for each data point we define lat and lon 
          for filename in glob.glob('*.csv'):
            with open(filename,'r') as f:
              for line in f:
                #re.sub equals the search and replace method of gedit, and consists of three components, the first one is what we want                   to match, the second one is the replacement and lastly where we want the program to look for it 
                if "Latitude" in line:
                  Latitude = re.sub(r".\s\bLatitude\b\:\s(.*\d+\..*\d+)\n",r"\1",line)
                elif "Longitude" in line:
                  Longitude = re.sub(r".\s\bLongitude\b\:\s(.*\d+\..*\d+)\n",r"\1",line)			
                    else:
                  newline = "%s,%s,%s" % (Latitude,Longitude,line)
                                          #line = line.replace(r"(^.+)",r"Latitude,Longitude,\1")
                                          #print newline
                                          #for the new line, we use regular expression to rearrange the data, get rid of day, time and                                             sea surface temperrature anomalies; as well as leaving only 3 decimal point for temperature 
                                          match = re.sub(r'^(\w+.\w+),(-*\w+.\w+),(\w+)-(\w+)-\w+:\w+:\w+.\w+                (\w+.\w{1,3}).*',r"\1,\2,\3-\4,\5",newline)
                                          #delete the original header of each file 
                                          match = re.sub(r'^(\w+.\w+),(-*\w+.\w+),T.*',r"",match)
                                          #delete blank lines 
                        match = re.sub(r'^\n',r"",match)
          #				print match
          #       we now write everything into our file and then we close it 
                  f2 = open ('All_data.txt','a')
                  f2.write(match)
                  f2.close()



###R script


###How to 
      **If you want to learn how to write a code like ours click [here](link) !**
       
---
##Temperature map 

--- 
##Features and advantages of this project


###Challenges

- [ ] set year range 
- [ ] extract data directly from python 
- [ ] set maximal temperature -Rscript

--- 
##Are we missing something? 

**Don't be shy, let us know!**
open an issue and we'll build this up together 

##License
>This project is licensed under the terms of the **GNU GENERAL PUBLIC LICENSE** license.
You can check out the full license [here](link)


