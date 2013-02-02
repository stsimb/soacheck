soacheck
========
soacheck - report changes in domain serial numbers
http://stsimb.irc.gr/2013/02/02/soacheck/

Intro
=====
I wanted to check how often a domain gets updated, so I quickly put together
soacheckd.

I assume that everybody increments the SOA serial number when they make a change
or generate the zone file. But strictly speaking, they don't have to do it (they
can use some other way to sync changes to all their NSs and make them available).

Usage
=====
List the zones you're interested in file "zones-to-check".
Execute soacheckd in your crontab (no need to run as root), as often as you like.
e.g.
 * * * * * /path/to/soacheckd > /dev/null

Check the results in soacheckd.log.

[stsimb@pipitsa soacheck]$ grep " gr. " soacheckd.log | tail
Fri Feb 1 04:51:01 EET 2013 soacheckd[22093] gr. serial changed from 1301312194 to 1302010099
Fri Feb 1 07:51:02 EET 2013 soacheckd[19481] gr. serial changed from 1302010099 to 1302010401
Fri Feb 1 10:52:01 EET 2013 soacheckd[18500] gr. serial changed from 1302010401 to 1302010695
Fri Feb 1 13:52:01 EET 2013 soacheckd[19079] gr. serial changed from 1302010695 to 1302011000

Ideas
=====
* Record answers from authoritative servers (answers now are from system resolver's cache)
* Record answers from multiple servers
 ** use a set of public dns servers
 ** use some dns-lg instances around the world [https://github.com/bortzmeyer/dns-lg]
* Make multiple checks in parallel
* Record changes of other RR types, e.g. A, AAAA, CNAME, PTR etc
* Trigger some event on change

