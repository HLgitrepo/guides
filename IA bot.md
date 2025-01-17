# Introduction:
In this file you will find more informations about IA bot. It is split in:
1. Slash commands that the bot have.
2. Other functions from the bot.
3. Definitions and explanation of some (technical) expressions.

# Commands:
## /ship_data
This will show some data about the state of a ship on certain day(s). The arguments are:
- `data`: Which kind of data you want to search:
  - `names`: Which names a ship had.
  - `resources`: The resources that ship had on the day.
  - `has_tag`: Which ships had a text inside their names. (usefull to check all ships with certain tag or name)
- `split_by`: Defines the split character used to *IdsInput*. (default is `,`)
- `ships`: An *IdsInput* with the ship IDs to be searched (or texts that a ship name contain if 'data' is `has_tag` is selected on `data`).
- `days`: An integer of how many days before today the search should be. By default it takes all data available.
## /get_logs
This will show all items transfered from one place to another. (Which includes Farmed -> Ship, Ship -> Destroied, Ship -> Ship).
The aesthetical arguments, the way data will be show, are:
- `order_by`: If the tree should show Sources or Destinations first.
- `show`: 'How many data to show'
  - `Srcs/Dsts`: Will show only the sources and destinations.
  - `Days,S/D`: Will show days, then inside each one the sources and destinations.
  - `Zone,D,S/D`: Will show the zones, then inside each one the same as `Days,S/D`.
  - `Z-Server,All`: Same as above, but will split zones by servers (eg. "US falcon, US raven, EU falcon")
  - `Day-Hours`, `Day-30mins` and `Day-15mins`: Will only show items transfered on the respectives periods of time.
The filter arguments, the ones that decide which data will be get or no, are (note, ejected_by may change how data is show):
- `start`: A *DateInput* where the search will begin.
- `end`: A *DateInput* where the search will stop.
- `split_by`: Defines the split character used to *IdsInput*. (default is `,`)
- `src_type`: If the src must be ship IDs (where 0 will be "mined/farmed") or if ship name contains a text (check `/ship_data`), by default it take ship IDs.
- `src`: An *IdsInput* (or text if 'src_type' is set to such) containing the sources that the search will be limited to, if empty it will get any source.
- `dst_type`: If the dst must be ship IDs (where 0 will be "destroied") or if ship name contains a text (check `/ship_data`), by default it take ship IDs.
- `dst`: An *IdsInput* (or text if 'dst_type' is set to such) containing the destinations that the search will be limited to, if empty it will get any destination.
- `ejected_by` can be:
  - `Normal`: Will only get items ejected by ejectors and farmed/mined.
  - `Hurt`: Will only get items get by damaging __ships__.
  - `All`: Will get all items. (this argument is the default)
  - `Differ`: Will show `Normal` and `Hurt` sources separately.
- `items`: An *IdsInput* containing the items that the search will be limited to, if empty it will get any item.
- `zones`: An *IdsInput* containing the zones that the search will be limited to, if empty it will get any zone.
## /related_ships
Will show ships that are considered related to a single ship, and ships related to related (if `recursive` is greater than 1).
- To get the main ship insert a ship id on `main_target`.
- `recursive` will decide how many times the search should happen (maximun is 10).
To consider if a ship is "related" the following arguments will be used:
- `start`: A *DateInput* where the search will begin.
- `end`: A *DateInput* where the search will stop.
- `types`: How many types of items was transfered.
- `amount`: How many items was transfered in total.
- `days`: In how many days the transactions happen.
## /multiple_ids
This will simply return the Integer ids that IA bot uses to express game items (same as drednot uses), game zones and game servers (deprecated due 1 single server).
## /read_ship_list
Will get an text file with a JSON inside, provided by `https://drednot.io/shiplist?server=0`, and give ships IDs togheter split by ',' in a way that it can be copied and paste to other commanders. There will be 4 categories where ships will be show: Where *owned* is set as "True", where *saved* is set as "True", where either *owned* and *saved* are set as "True", and where both *owned* and *saved* are set as "False" (the ships that didnt fit on other categories).
## /send_et_data
Send a text defined on `message` argument to the event tracker ship chat. It can even be commands such "/save". (Restricted command)

# Extra functions:
## Event tracker:
The event tracker is an in-game bot that will make one ship still load. And will get all messages sent on this ship, from which we can know when an event will happen.
## Message relay:
Send a DM to bot will make it relay your message to certain places, with a pseudonym, if you are registered.

# Definitions:
## Integer:
Name given to simple numbers, eg. `1` or `845878971974876`.
## IdsInput:
A list of Integers or text splited by `,` or `|`, for example: `1,2,3`.
## DateInput:
To insert a point in time using IA's DateInput you must use either an integer or normal date. Remembering it will limit to the minimun and maximun period on database.
### Integers:
By using an integer it will be read as unix second; Unix seconds are how many secs elapsed since 1/1/1970 00:00 0-UTC, you can eazily find a converter from date to it online.
### Human date:
Insert human date requires it to be formated in DD/MM/YYYY such as `4/1/2025`; The exact point on time that it represents depends if it was given on *start* or *end* argument, where:
- If given on *start*, it will take the first second from a day (eg. `4/1/2025` will mean 00:00 of 4/1, on 0-UTC).
- If given on *end*, it will take the last second from a day (eg. `4/1/2025` will mean 23:59 of 4/1, on 0-UTC).
So to get the entire 24h of a day you just need to repeat it in both *start* and *end* arguments.
## JSON:
A type of data storage using text.