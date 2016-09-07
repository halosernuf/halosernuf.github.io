---
layout: post
title: Funimation theater locator
date: 2016-09-07 15:03:28
---
Looking forward to the screening for [Kiminonawa](https://myanimelist.net/anime/32281/Kimi_no_Na_wa). Funimation [licenced](http://www.funimation.com/blog/2016/07/03/funimation-licences-makoto-shinkais-newest-film-your-name-kimi-no-na-wa/) the anime in 07/03 and will be at north america soon.

Funimation's theater locator is kind of s***. However, its api is somehow open without app-key needed. 

```
http://www.funimationfilms.com/api/locator.php/theater/[film name]
```

Json response

```javascript
{
        u 'City': u 'BUFFALO', 
        u 'CircuitID':u 'ASHURST', 
        u 'MovieID': u 'Empire of Corpses',
        u 'TheaterIDSpecial': u '', 
        u 'Title': u 'NORTH PARK THEATRE',
        u 'MovieIDSpecial': u '',
        u 'Longitude': u '-78.8553828',
        u 'Latitude': u '42.9479209', 
        u 'State': u 'NY', 
        u 'Exhibitor': u 'Annette Ashurst',
        u 'Address': u '1428 HERTEL AVENUE',
        u 'PostalCode': u '14216', 
        u 'TicketRegex': u 'https://www.northparktheatre.org/showtimes/2016-04-19',
        u 'MovieName': u 'Empire of Corpses',
        u 'ScreenDate': u '2016-04-19'
}
```