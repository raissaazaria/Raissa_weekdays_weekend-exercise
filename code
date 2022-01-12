import csv
import matplotlib.pyplot as plt
import datetime as dt
import pygal
import statistics as st

IntervalWeekday = {}
IntervalWeekend = {}

#used the new file that has no 'NA' attributes
filename = 'newActivity.csv'

with open(filename) as f:
  reader = csv.reader(f)
  header = next(reader)

  wr = open("WeeklyActivity.csv","w")
  wr.write(str (header[0]) + "," + str (header[1]) + ","+ str (header[2]))
  wr.write("\n")

#setting a for loop to go through each rows entirely and declaring each rows as the corresponding variables.
  for row in reader :

    steps = row[0] 

    date = row[1]  
    day = dt.datetime.strptime(date,'%Y-%m-%d') 

    interval = int(row[2]) 

#if statement differentiating weekdays and weekends
    if dt.datetime.date(day).weekday() <5: 
      row.append("Weekday")
      IntervalWeekday.setdefault(interval,[])
      IntervalWeekday[interval].append(int(steps))
    else : 
      row.append("Weekend")
      IntervalWeekend.setdefault(interval,[])
      IntervalWeekend[interval].append(int(steps))


#writing new factor variable in the new dataset
    wr.write(str(row[0]))
    wr.write(str (row[0]) + "," + str (row[1]) + ","+ str (row[2]) + "," + str (row[3]))
    wr.write("\n")
  wr.close()

#creating lists to store average steps per interval for weekdays and weekends and using statistics to count the average
averageWeekdays = []
for i in IntervalWeekday.keys():
    averageWeekdays.append(st.mean(IntervalWeekday.get(i)))

averageWeekend= []
for i in IntervalWeekend.keys():
    averageWeekend.append(st.mean(IntervalWeekend.get(i)))


hist = pygal.Bar()
hist.title = "Average Steps per Interval on Weekdays"
hist.x_title = "Interval (5 minutes)"
hist.y_title = "Average Steps per Interval"
hist.x_labels = IntervalWeekday.keys()
hist.add("Average Steps", averageWeekdays)
hist.render_to_file('WeekdaySteps.svg')

hist = pygal.Bar()
hist.title = "Average Steps per Interval on Weekends"
hist.x_title = "Interval (5 minutes)"
hist.y_title = "Average Steps per Interval"
hist.x_labels = IntervalWeekday.keys()
hist.add("Average Steps", averageWeekend)
hist.render_to_file('WeekendSteps.svg')
