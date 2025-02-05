## Overview

Shift's calendar event data is stored in a mysql database running on api.bikeslist.org.  This has some "How do I?" tips and tricks for people who need to update or use that data directly.

## Common tasks

- How can I find the URL for an event to be edited?
1. Start in `api.bikeslist.org:/opt/shift-docs`
2. `./shift mysql`
3. Find the event.  Best way is probably to search by case-sensitive exact title, but make sure you're looking at the correct event in case there have been several with the same title over the years.  Looking for the most recently modified one will USUALLY be correct.  For instance: `select * from calevent where title="Thursday Night Ride" order by modified desc limit 1;`
4. Get the password and ID for that event, for instance:  `select id,password from calevent where title="Thursday Night Ride" order by modified desc limit 1;`
5. Construct the URL:  https://bikeslist.org/addevent/edit-ID-PASSWORD
6. Before sharing, test the URL in your browser - does it load successfully and does that look like the right event?

- How can I set a password for an event without one? (so that we can create an edit link)
1. Start in `api.bikeslist.org:/opt/shift-docs`
2. `./shift mysql`
3. Find the event.  Best way is probably to search by case-sensitive exact title, but make sure you're looking at the correct event in case there have been several with the same title over the years.  Looking for the most recently modified one will USUALLY be correct.  For instance: `select * from calevent where title="Thursday Night Ride" order by modified desc limit 1;`.  
4. If that is the right event, you need the ID field: `select ID from calevent where title="Thursday Night Ride" order by modified desc limit 1;`
5. Update the event.  You can use any password, make it a little hard to guess: `update calevent set password="hard-to-guess" where id=7283;`
6. Now you can do steps 5 and 6 from the previous question to create the URL.

- How can I mark an event as "featured"?
1. Locate the event in the database (see steps 1–3 in the above questions). 
2. If that is the right event, you need the ID field: `select ID from calevent where title="Pedalpalooza 2019 Kickoff Ride" order by modified desc limit 1;`
5. Update the `highlight` field with a value of `1` to mark it as featured (or zero to remove featured status): `update calevent set highlight = 1 where id = 7483;`


## Who knows more?

@fool (gently@gmail.com) and @carrythebanner .  Best to reach them and the rest of the crew as bikecal@bikeslist.org
