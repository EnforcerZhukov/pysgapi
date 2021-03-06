# PySgApi

PySgApi is a Python tool that works as some sort of unofficial "API" for the [SteamGifts](http://www.steamgifts.com) website.

It can fetch active giveaways on the page with many useful information about them, like:

* Game's name
* Giveaway URL and ID
* Cost in points
* Required level
* Datetime when it was created and ends
* How much time is left for the giveaway to end; how much time it has been active
* How many users entered the giveaway and their usernames
* Probability to win the giveaway (1/entries)

## Requirements

* Python >=3.6
* requests-html

## Examples

```python
from pysgapi import SG
sg = SG()

#Find giveaways on the first 5 pages
giveaways = sg.find_giveaways(page=5)

#Find giveaways that cost no more than 10 points
#By default only giveaways on first page will be returned
giveaways = sg.find_giveaways(max_points=10)

#Find giveaways with no more than 1000 entries, and with a required level not higher than 3
giveaways = sg.find_giveaways(max_entries=1000, max_level=3)

#Find giveaways where there I have 50% of probabilities of wining it
giveaways = sg.find_giveaways(min_probability=0.5, page=10)

#You can get many things from a giveaway object
ga = giveaways[0]
#Game's name
print(ga.name)
#Giveaway URL
print(ga.url)
#Game's Steam URL
print(ga.steam_url)
#Game's Steam ID
print(ga.steam_id)
#Entries (how many users entered the GA)
print(ga.entries)
#Giveaway required level and cost in points
print(ga.level, ga.points)
#Datetime when giveaway was created and ends (in UTC time)
print(ga.created_utc, ga.end_utc)
#Get the probability to win (1/number of entries)
print(ga.calculate_probability())

#Useful methods related with time (all of them return time in seconds)
#How much time is left until giveaway ends?
print(ga.get_remaining_time())
#How much time has the giveaway been active?
print(ga.get_elapsed_time())
#How much time will the giveaway be active?
print(ga.get_total_time())

#Get users that entered the giveaway
users = ga.get_users()
print("Users that entered the giveaway for", ga.name, "URL:", ga.url)
for u in users:
    print(u)
```
