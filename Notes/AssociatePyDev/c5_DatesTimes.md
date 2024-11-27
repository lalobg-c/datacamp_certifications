# Working with Dates and Times in Python

////////////////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////////////

## Dates and Calendars
### Dates in Python
```python
from datetime import date
two_hurricanes_date = [date(2016, 10, 7), date(2017, 6, 21)]
print(two_hurricanes_date[0].year) #--> 2016
print(two_hurricanes_date[0].month) #--> 10
print(two_hurricanes_date[0].day) #--> 7
print(two_hurricanes_date[0].weekday()) #--> 4 which is Friday
```

### Math with dates
```python
from datetime import date
d1 = date(2017, 11, 5)
d2 = date(2017, 12, 4)
l = [d1, d2]
print(min(l)) #--> 2017-11-05
delta = d2 - d1
print(delta.days) #--> 29

from datetime import timedelta
td = timedelta(days=29)
print(d1 + td) #--> 2017-12-04
```

### Turning dates into strings
```python
d = date(2017, 11, 5)
# ISO format or ISO 8601 format: YYYY-MM-DD
print(d) #--> 2017-11-05
print([d.isoformat()]) #--> ['2017-11-05']

# d.strftime() method for a custom date format
d = date(2017, 1, 5)
print(d.strftime("%Y")) #--> 2017
print(d.strftime("Year is %Y")) #--> Year is 2017
print(d.strftime("%Y/%m/%d")) #--> 2017/01/05
# %j for day number of the year
# %B for full name month
```

////////////////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////////////

## Combining Dates and Times
### Dates and times
```python
from datetime import datetime
dt = datetime(2017, 10, 1, 15, 23, 25, 500000)
dt_hr = dt.replace(minute=0, second=0, microsecond=0)
print(dt_hr)#--> 2017-10-01 15:00:00
```

### Printing and parsing datetimes
```python
dt = datetime(2017, 12, 30, 15, 19, 13)
print(dt.strftime("%Y-%m-%d %H:%M:%S"))
print(dt.strftime("%H:%M:%S on %Y/%m/%d"))
print(dt.isoformat())

dt = datetime.strptime("12/30/2017 15:19:13", "%m/%d/%Y %H:%M:%S")
print(type(dt)) #--> <class 'datetime.datetime'>

ts = somenumber
print(datetime.fromtimestamp(ts))
```

### Working with durations
```python
start = datetime(...)
end = datetime(...)
duration = end - start
print(duration.total_seconds())

from datetime import timedelta
delta1 = timedelta(seconds=1)
delta2 = timedelta(days=1, seconds=1)
# One can do things like:
start + delta1
start + delta2
```

////////////////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////////////

## Time Zones and Daylight Saving
### UTC offsets
```python
from datetime import datetime, timedelta, timezone
ET = timezone(timedelta(hours=-5))
dt = datetime(2017, 12, 30, 15, 9, 3, tzinfo = ET)
print(dt) #--> 2017-12-30 15:09:03-05:00

IST = timezone(timedelta(hours=5, minutes=30))
print(dt.astimezone(IST))

print(dt.replace(tzinfo=timezone.utc)) # UTC offset shifted
print(dt.astimezone(timezone.utc))
```

### Time zone database
```python
from dateutil import tz
et = tz.gettz('America/New_York')
last = datetime(2017, 12, 30, 15, 9, 3, tzinfo = et)
```

### Starting daylight saving time
```python
spring_ahead_159am = datetime(2017, 3, 12, 1, 59, 59)
spring_ahead_3am = datetime(2017, 3, 12, 3, 0, 0)
spring_ahead_3am.isoformat()
(spring_ahead_3am - spring_ahead_159am).total_seconds() #--> 3601.0

EST = timezone(timedelta(hours=-5))
EDT = timezone(timedelta(hours=-4))

spring_ahead_159am = spring_ahead_159am.replace(tzinfo = EST)
spring_ahead_159am.isoformat() #--> '2017-03-12T01:59:59-05:00'
spring_ahead_3am = spring_ahead_3am.replace(tzinfo = EDT)
spring_ahead_3am.isoformat() #--> '2017-03-12T03:00:00-04:00'
(spring_ahead_3am - spring_ahead_159am).seconds #--> 1

# Using tz from dateutil, this is done automatically:
eastern = tz.gettz('America/New_York')
spring_ahead_159am = datetime(2017, 3, 12, 1, 59, 59, tzinfo = eastern)
spring_ahead_3am = datetime(2017, 3, 12, 3, 0, 0, tzinfo = eastern)
```

### Ending dayligh saving time
```python
eastern = tz.gettz('US/Eastern')
first_1am = datetime(2017, 11, 5, 1, 0, 0, tzinfo=eastern)
tz.datetime_ambiguous(first_1am) #--> returns true or false

second_1am = datetime(2017, 11, 5, 1, 0, 0, tzinfo = eastern)
second_1am = tz.enfold(second_1am)
(first_1am - second_1am).total_seconds() #--> 0,0

first_1am = first_1am.astimezone(tz.UTC)
second_1am = second_1am.astimezone(tz.UTC)
(second_1am - second_1am).total_seconds() #--> 3600.0
```


////////////////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////////////


## Easy and Powerful: Dates and Times in Pandas
### Reading date and time data in Pandas
```python
rides = pd.read_csv('file.csv', parse_dates=['Start date', 'End date'])
rides['Start date'] = pd.to_datetime(rides['Start date'], format = "%Y-%m-%d %H:%M:%S")
rides['Start date'].iloc[2] #--> pandas timestamp
rides['Duration'] = rides['End date'] - rides['Start date']
rides['Duration'].dt.total_seconds().head()
```



### Summarizing datetime data in Pandas
```python
rides['Duration'].mean()
rides['Duration'].sum()
rides['Duration'].sum() / timedelta(days=91)
rides['Member type'].value_counts() / len(rides)

rides['Duration seconds'] = rides['Duration'].dt.total_seconds()
rides.groupby('Member type')['Duration seconds'].mean()

# Average duration by month
rides.resample('M', on = 'Start date')['Duration seconds'].mean()

# Size per group
rides.groupby('Member type').size()

# First ride per group
rides.groupby('Member type').first()
```



### Additional datime methods in Pandas
```python
rides['Duration'].dt.total_seconds().min()

rides['Start date'].head().dt.tz_localize('America/New_York')

# Handle ambiguous datetimes
rides['Start date'] = rides['Start date'].dt.tz_localize('America/New_York', ambiguous = 'NaT')

# years, months, days of data
rides['Start date'].head().dt.year
rides['Start date'].head().dt.month
rides['Start date'].head().dt.day_name()
```

////////////////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////////////
