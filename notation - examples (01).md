I will try to develop a notation that can describe solo patterns and passing patterns with synchronous throws and rhythmical changes.

## vanilla site-swap

{ "pattern": "<5 3 1>"}

A simpel solo site-swap, without synchronous throws.

## passing whole counts
{ "pattern":"< 4p 3 3  | 3 5p 3 >"}

The pipe symbol ("|") separates the instructions for the next juggler.

{ "pattern":"< 4p_B 3 3  | 3 4p_C 3 | 3 3 4p_A >"}

With 3 jugglers, we must specify to which jugglers the passes go

{"nJugglers":3,  "pattern":"<  4p_B 3 3 >"}

This is the same as the previous pattern.
The computer should be able to work out that the jugglers are shifted by 1 count, because the period is 3

{"nJugglers":3,  "pattern":"<  4 4p_B 3 3 3 3>"}

The computer should be able to work out that the jugglers are shifted by 2 counts, because the period is 6.
So

{ "pattern":""<4 4p_B 3 3 3 3  | 3 3  4 4p_C 3 3  | 3 3 3 3 4 4p_A >"}

is the same as the previous pattern.

{ "pattern":"<3 3 4 4p >"}

The number of jugglers is not given, but there is a pass, so there are 2 jugglers.
The period is 4, so the second juggler is shifted by 2 counts (4/2 = 2).

{ "pattern":"<3 3 4 4p | 4 4p 3 3 >"}

{ "nJugglers":2, "pattern":"<3 3 4 4p >"}

This is the same as the previous pattern.

## passing fractions
### half-beat shift
{ "pattern":"< 4 3.5 3.5 3 3.5 | 1 3.5 1 3.5 3.5 >",

  "jugglerShift": "[0, 0.5]"}

The sequence of the second juggler will start 0.5 beat later

{"nJugglers":2,

  "pattern":"< 4 3.5 3.5 3 3.5 | 3 3.5 4 3.5 3.5 >",

  "jugglerShift": "[0, 0.5]"}

Both jugglers juggle the same sequence, but the second juggler will start 0.5 beat later

{  "pattern":"< 4 3.5 3.5 3 3.5 >"}

The fraction indicates that there is a pass to a juggler that is shifted 0.5 count.
The period of the pattern is 5. The shift is 5/2 = 2.5
So this is the same as the previous pattern.

{"nJugglers":2,

  "pattern":"<   4    3.5    3.5 

             |     3      3.5     >",

  "jugglerShift": "[0, 0.5]",

  "period": 2.5,

  "jugglerPermutation":"(A,B)"
}

This is the same as the previous pattern.
The pattern is repeated after 2.5 counts, with jugglers A and B exchanged

### multi-handed site-swap
{"nJugglers":2,

  "pattern":"<   8 6 7 7 7>",

}

Again the same pattern.
There are 2 jugglers, so the shift must be 5/2 = 2.5.
There are no fractions, so this is a multi-handed notation.

### other fractions
{"nJugglers":5,  "pattern":"<  3.6 3 3>"}

The fraction indicates that there is a pass to a juggler that is shifted 0.6 count.
(after 5 jugglers, this makes 3 counts, so the last pass fits in the pattern)
{"nJugglers":5,  "pattern":"<  3.6 3 3>",

 "jugglerShift": "[0, 0.6, 1.2, 1.8, 2.4 ]"}

This is the same as the previous pattern.
{"nJugglers":5,  "pattern":"<  3.6 3 3 | 3.6 3 3 | 3 3.6 3 | 3 3.6 3 | 3 3 3.6 >",

 "jugglerShift": "[0, 0.6, 0.2, 0.8, 0.4 ]"}

This is the same as the previous pattern.
(note: the shifts are different, so the patterns had to be shifted for jugglers 3,4 and 5)

{"pattern":"<  3.33 3 1 3 3>"}

or 

{"nJugglers":3,  "pattern":"<  3.33 3 1 3 3>"}

 "jugglerShift": "[0, 1.67, 2.33]"}

Of course, .33 means 1/3 and .67 mean 2/3.
If only the sequence for juggler 1 is given, the shifts will be period/3, 2 * period/3 etc.
or

{"nJugglers":3,  "pattern":"<  3.33 3 1 3 3 | 3 3.33 3 1 3 | 1 3 3 3.33 3 >",

 "jugglerShift": "[0, 0.67, 0.33]"}

or

{"nJugglers":3,  "pattern":"<  3.33 3 1 3 3 | 1 3 3 3.33 3 | 3 3.33 3 1 3 >",

 "jugglerShift": "[0, 0.33, 0.67]"} (note: the shifts are different, so the patterns are in a different order)

or

{"nJugglers":3,  "pattern":"<  3.33 3 1 3 3 | 1 3 3 3.33 3 | 3 3.33 3 1 3 >"}

If there is a separate sequence for each juggler, and no shift is indicated, the shift will be 1/3, 2/3 etc.


Perhaps there should be a parameter that states the desired denominator of the fraction, so wil wil know that 0.7 means 2/3. (for poly-rhythmic patterns, this will also be useful)

Like:
{"nJugglers":3, 
 "denominator":3,
 "pattern":"<  3.3 3 1 3 3>"}

(in this case, the only possible fractions are .3 and 0.7 (=.66666....) so 1 digit is sufficiently accurate.


## synchronous throws

### 2 in each hand
Now come some patterns with 2 balls in each hand, 1 hand throws every 2nd beat, the other hand throws every 3rd beat.
We would expect that the hand that throws more often, will throw lower. However, it can also throw at the same height, and have a longer empty duration.

{ "pattern":"< (4,6) (,) (4,) (,6) (4,) (,) >"}

This is a pattern that has synchronous and a-synchronous throws.
Perhaps you are used to the notation:

 < (4,6) (0,0) (4,0) (0,6) (4,0) (0,0) >
But the "0" suggest that the hand is empty, and it may hold an object at those times.

### flight durations
{ "pattern":"< (4,6) (,) (4,) (,6) (4,) (,) >",

 "flight_durations": "< (2.2,3.2) (,) (3.2,) (,2.2) (3.2,) (,) >"
}

So the hold durations of these throws are:
< (1.8,2.8) (,) (1.8,) (,2.8) (1.8,) (,) >

And the empty duration is 0.2 for each throw.
< (0.2  0,2) (,) (0.2,) (,0.2) (0.2,) (,) >
(hold duration = siteswap value - flight duration
 empty duration = time between throws - hold duration)

{ "pattern":"< (4,6) (,) (4,) (,6) (4,) (,) >",

 "flight_durations": "< (3.2,3.2) (,) (3.2,) (0,3.2) (3.2,0) (,) > "
}

Now, all throws are at the same height.
Some hold durations will be shorter:
< (0.8,2.8) (,) (0.8,) (,2.8) (0.8,) (,) >

And the empty durations will be different:
< (1.2,0.2) (,) (1.2,) (,0.2) (1.2,) (,) >

### 3 balls vs 2 balls
The hand that juggles more balls, will either throw higher, or more often.
Or both, for example:

{ "pattern":"< (6,6) (,) (6,) (,6) (6,) (,) >",

 "flight_durations": "< (4.2,3.2) (,) (4.2,) (0,3.2) (4.2,0) (,) > "
}

So the hold durations of these throws are:
< (1.8,2.8) (,) (1.8,) (,2.8) (1.8,) (,) >

And the empty duration is 0.2 for each throw.
< (0.2 , 0.2) (,) (0.2,) (,0.2) (0.2,) (,) >

Throws at the same height:
{ "pattern":"< (6,6) (,) (6,) (,6) (6,) (,) >",

 "flight_durations": "< (4.2,4.2) (,) (4.2,) (,4.2) (4.2,) (,) > "
}

Now all throws are the same height, and have the same hold duration:
< (1.8,1.8) (,) (1.8,) (,1.8) (1.8,) (,) >

The empty times are now different:
< (0.2, 1.2) (,) (0.2,) (,1.2) (0.2,) (,) >
(the hand that juggles fewer objects is more often empty)

Just throwing higher:
{ "pattern":"< (6,4) (,) >"}


alternating hands:
{ "pattern":"< (6x,4) (,) (4,6x) (,) >"}

The alternation of hands may be indicated by a symbol:
{ "pattern":"< (6x,4) (,) %  >"}


Of course, passing patterns can also be written:
{ "pattern":"< (4x,3p) (,) | (,) (4x,3p)  >"}

(this is passing 7 clubs, double selfs, single passes)

or
{"nJugglers":2,
  "pattern":"< (4x,3p) (,) >"
  "jugglerShift": "[0, 1]"}

The pass implies that there are 2 jugglers, so the following notation would be sufficient:

{ "pattern":"< (4x,3p) (,) >"}


A more complicated pattern would be:
(synchronous self/pass, then some selfs)

{ "pattern":"< (3,4xp) (,4x) (,) (3,) >"}


## poly-rhythmic
If the frequencies relate as 2/3 or 2/4, patterns can easily be described using synchronous throws.
For ratios like 3/4 or 3/5 etc, we would need many (,) in the pattern.
So I want to use a notation that has fractions.

(to be expanded)

