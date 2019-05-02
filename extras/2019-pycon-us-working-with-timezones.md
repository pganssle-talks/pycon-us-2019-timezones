# PyCon US 2019 Proposal
## Working with Time Zones: Everything You Wish You Didn't Need to Know (Paul Ganssle)

#### Submitted by
Paul Ganssle

#### Duration
No preference

### Description
Time zones are complicated, but they are a fact of engineering life. Time zones have [skipped entire days](http://www.bbc.com/news/world-asia-16351377) and repeated others. There are time zones that switch to [DST twice per year](https://www.timeanddate.com/time/zone/morocco/casablanca). But not necessarily every year.  In Python it's even possible to create datetimes with non-transitive equality (`a == b`, `b == c`, `a != c`).

In this talk you'll learn about Python's time zone model and other concepts critical to avoiding datetime troubles. Using `dateutil` and `pytz` as examples, this talk covers how to deal with ambiguous and imaginary times, datetime arithmetic around a Daylight Savings Time transition, and datetime's new `fold` attribute, introduced in Python 3.6 ([PEP 495](https://www.python.org/dev/peps/pep-0495/)).

### Who and Why (Audience)
All users will learn a number of common time zone pitfalls in Python and in general. Beginners (and those unfamiliar with this particular corner of Python) will learn about the abstractions Python uses to represent time zones and why they are only *partially* compatible with pytz. Intermediate and advanced users will probably rush off in the middle of the talk to fix a bunch of their code that's going to break next time it gets called during a DST transition or deployed to a machine with a different time zone environment.

### Outline
(Note: Times at the highest level of the outline include times for the items on lower levels; times preceeded by "T" are a running total)

- Introduction [ 9m 30s ]
  - Speaker and talk intro (1m)
  - UTC (1m)
  - Time zones vs. offsets (1m 45s)
  - Fun examples (4m 15s)
    > Examples of counter-inuitive time zones, including:
    > - Change in DST without an offset change, change in offset without DST change
    > - Multiple yearly DST shifts
    > - Missing days, doubled days
  - Why do we need to work with time zones at all? (1m 30s)

- Python time zone model [ 1m 30s, T:11m ]
  - tzinfo objects, with example implementation (1m 30s)

- Ambiguous times [ 4m, T:15m ]
  - Introduction (30s)
  - PEP 495: Local Time Disambiguation  (1m 30s)
    > Introduction of the fold attribute, dateutil's backport
  - Comparing aware timezones (2m 30s)
    > Intra- vs. inter-zone semantics, a case of non-transitive datetime comparisons

- Imaginary times [ 2m 30s, T:17m 30s ]
  > Times that don't exist, why this led to non-transitivity in the previous case.

- Working with time zones [ 2m 30s, T:20m ]
  - dateutil (1m)
    > How to attach, replace and convert between time zones.
  - pytz (30s)
    - pytz's time zone model (1m 30s)

- Handling ambiguous times [ 3m, T:23m ]
  > How to write code that responds when a wall time appears twice in a given zone
  - Overview (30s)
  - dateutil (2m)
  - pytz (30s)

- Handling imaginary times [2m, T:25m ]
  > How to write code that won't generate non-existent datetimes
  - dateutil (45s)
  - pytz (1m 15s)

- Conclusion [1m 30s, T:26m 30s]

This is the outline for the 30-minute version. There is also a 45 minute version that expands on the types of time zone objects available, and goes into more detail about best practices such as storing and serializing timezone-aware datetimes and dealing with the IANA time zone database. In the 45 minute version, I will also discuss some of the pitfalls around local time, and in particular the problems that arise when your system time zone changes during the course of a program (*many* bets are off in that case).


### Additional Notes
- I am the maintainer for python-dateutil and a frequent contributor to CPython's `datetime` library.
- I have spoken at many conferences, you can find my previous talks here: https://ganssle.io/talks/
- I have given a 45-minute version of this talk at PyBay 2017 (though the content would be updated before the next time I give the talk): https://www.youtube.com/watch?v=l4UCKCo9FWY
- Other versions of this talk:
   - 30 minute version at PyLondinium 2018: https://youtu.be/TPrmyAZZPi0
    - Lightning talk at PyCon 2017: https://youtu.be/SXl-pZnoaQ0?t=1228
- I have three blog posts on this subject as well, tagged "timezones" on my blog: https://blog.ganssle.io/tag/timezones.html
