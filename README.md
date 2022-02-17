# Timerefs

The goal of this project is to compare different time and frequency references.

### Turns out someone beat me to the punch

So I've procrastinated on actually starting this project for 7 years or so, and someone actually went and built it: https://github.com/jp3141/60Hz

## But first, a brief essay on time and frequency.

### Time reference

A time reference is anything that can tell you the current time.

Examples of time references:
 - The [system clock](https://en.wikipedia.org/wiki/System_time)
 - A [real-time clock](https://en.wikipedia.org/wiki/Real-time_clock) (RTC) chip.
 - A GPS device, connected via serial.
 - A web API that returns the current time
 - NIST's WWV, WWVH, and WWVB radio stations
 - A [grandfather clock](https://en.wikipedia.org/wiki/Longcase_clock).

### Frequency reference

A frequency reference, or oscillator, is anything that produces a signal of a known frequency.
Unlike a time reference, a frequency reference does not provide the current time; only that a certain amount of time has passed since the last cycle.

Examples of frequency references:
 - The rotation of the Earth.
 - A [crystal oscillator](https://en.wikipedia.org/wiki/Crystal_oscillator)
 - Atomic clocks
 - 60Hz or 50Hz [AC power](https://en.wikipedia.org/wiki/Utility_frequency)
 - The [High Precision Event Timer](https://en.wikipedia.org/wiki/High_Precision_Event_Timer)
 - The [pulse per second](https://en.wikipedia.org/wiki/Pulse_per_second) output of a GPS unit
 - A pendulum

### Long-term stability and clock disciplining.

The two concepts are strongly intertwined: time references are generally created by making a clock from a frequency reference, as in RTC devices, atomic clocks, and mechanical clocks.
Over a long time, two clocks will tend to drift away from each other.
Inaccurate clocks will drift quickly, accurate clocks will drift slowly.
To compensate for this, many clocks will use some sort of [time transfer](https://en.wikipedia.org/wiki/Time_transfer), such as the [Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol), or radio broadcasts.

Similarly, the short-term stability of a frequency reference can be improved by disciplining it against an accurate time reference, as in [GPS-disciplined oscillators](https://en.wikipedia.org/wiki/GPS_disciplined_oscillator).
This is a similar concept to time transfer, but the goal is to keep the local oscillator within tight frequency tolerances, rather than caring about the integral over a long time period.

#### TAI, UTC, and leap seconds

There are many valid systems of time: (from [Systems of Time Time Service Department, U.S. Naval Observatory](http://tycho.usno.navy.mil/systime.html))

> - Atomic Time , with the unit of duration the Systeme International (SI) second defined as the duration of 9,192,631,770 cycles of radiation corresponding to the transition between two hyperfine levels of the ground state of cesium 133. TAI is the International Atomic Time scale, a statistical timescale based on a large number of atomic clocks.
> - Universal Time (UT) is counted from 0 hours at midnight, with unit of duration the mean solar day, defined to be as uniform as possible despite variations in the rotation of the Earth.
>  - UT0 is the rotational time of a particular place of observation. It is observed as the diurnal motion of stars or extraterrestrial radio sources.
>  - UT1 is computed by correcting UT0 for the effect of polar motion on the longitude of the observing site. It varies from uniformity because of the irregularities in the Earth's rotation.
> - Coordinated Universal Time (UTC) differs from TAI by an integral number of seconds. UTC is kept within 0.9 seconds of UT1 by the introduction of one-second steps to UTC, the "leap second." To date these steps have always been positive.

TAI and UTC are probably the most commonly used time systems. TAI is defined by atomic clocks, which are based on very accurate frequency references. 
UTC is a modified version of TAI which has been disciplined to UT1, so as to be useful for humans who care about the solar day.

## Goals of the project

I intend to observe several time or frequency references and plot their relative drift over time. In particular, I'd like to measure how various references handle leap seconds.

 - How exactly does Google handle leap seconds? (They have publicly blogged about their [smearing technique](http://googleblog.blogspot.com/2011/09/time-technology-and-leaping-seconds.html). I want to make graphs of it.)
 - The power grid in North America is [clock-disciplined](https://en.wikipedia.org/wiki/Utility_frequency#Long-term_stability_and_clock_synchronization). Does this follow TAI or UTC (that is, will the power company add cycles when there is a leap second?)
  - check out this sweet [real-time map](http://fnetpublic.utk.edu/gradientmap.html) of the US
  - and this awesome [indicator](http://www.dynamicdemand.co.uk/grid.htm) for the UK
  - and [this one](http://www.mainsfrequency.com/) for mainland Europe.

