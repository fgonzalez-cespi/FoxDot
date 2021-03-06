# `PGroups`

## Classes

### `PGroupPrime(self, seq=[], *args)`

Class to represent any groupings of notes as denoted by brackets.
PGroups should only be found within a Pattern object.

#### Methods

##### `__key(self)`

Returns a tuple of information to identify this Pattern 

##### `__bool__(self)`

Returns True if *any* value in the Pattern are greater than zero 

##### `__eq__(self, other)`

Return self==value.

##### `__ge__(self, other)`

Return self>=value.

##### `__getitem__(self, key)`

Overrides the Pattern.__getitem__ to allow indexing
by TimeVar and PlayerKey instances. 

##### `__gt__(self, other)`

Return self>value.

##### `__hash__(self)`

Return hash(self).

##### `__init__(self, seq=[], *args)`

Initialize self.  See help(type(self)) for accurate signature.

##### `__invert__(self)`

Using the ~ symbol as a prefix to a Pattern will reverse it.
>>> a = P[:4]
>>> print(a, ~a)
P[0, 1, 2, 3], P[3, 2, 1, 0]

##### `__iter__(self)`

Returns a generator object for this Pattern 

##### `__le__(self, other)`

Return self<=value.

##### `__len__(self)`

Returns the *expanded* length of the pattern such that if the pattern is laced, the
value is the length of the list multiplied by the lowest-common-multiple of the lengths
of nested patterns. e.g. the following are identical:
```
>>> print( len(P[0,1,2,[3,4]]) )
8
>>> print( len(P[0,1,2,3,0,1,2,4]) )
8
```

##### `__lt__(self, other)`

Return self<value.

##### `__ne__(self, other)`

Return self!=value.

##### `__or__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__repr__(self)`

Return repr(self).

##### `__ror__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__setslice__(self, i, j, item)`

Only works in Python 2 

##### `__str__(self)`

Return str(self).

##### `_update_delay(event, delay)`

Updates the delay value in the event dictionary 

##### `_update_sample(event, sample)`

Updates the sample value in the event dictionary 

##### `accum(self, *args)`

Returns a Pattern that is equivalent to list of sums of that
Pattern up to that index.

##### `all(self, func=<lambda>)`

Returns true if all of the patterns contents satisfies func(x) - default is nonzero 

##### `amen(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `arp(self, arp_pattern)`

Return a new Pattern with each item repeated len(arp_pattern) times
and incremented by arp_pattern. Useful for arpeggiating. e.g.
```
>>> P[0, 1, 2, 3].arp([0, 2])
P[0, 2, 1, 3, 2, 4, 3, 5]
```

##### `asGroup(self)`

Returns the Pattern as a PGroup 

##### `bubble(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `calculate_time(self, dur)`

Returns a PGroup of durations to use as the delay argument
when this is a sub-class of `PGroupPrime` 

##### `change_state(self)`

To be overridden by any PGroupPrime that changes state after access by a Player 

##### `choose(self)`

Returns one randomly selected item 

##### `convert_data(self, *args, **kwargs)`

Makes a true copy and converts the data to a given data type 

##### `copy(self)`

Returns a copy of the Pattern such that alterations to the
Pattern.data do not affect the original.

##### `count(self, item)`

Returns the number of occurrences of item in the Pattern

##### `deep_shuffle(self, n=1)`

Returns a new Pattern with shuffled contents and shuffles
any nested patterns. To shuffle the contents of nested patterns
with the rest of the Pattern's contents, use `true_shuffle`.

##### `duplicate(self, *args)`

Repeats this pattern n times but keep nested pattern values 

##### `eq(self, other)`

equals operator 

##### `every(self, n, method, *args, **kwargs)`

Returns the pattern looped n-1 times then appended with
the version returned when method is called on it. 

##### `flatten(self)`

Returns a nested PGroup as un-nested e.g.
::

    >>> P(0,(3,5)).flatten()
    P(0, 3, 5)

##### `get_behaviour(self)`

Returns a function that changes a player event dictionary 

##### `get_methods(cls)`

Returns the methods associated with the `Pattern` class as a list 

##### `getitem(self, key, get_generator=False)`

Called by __getitem__() 

##### `group(self)`

Returns the Pattern as a PGroup 

##### `has_behaviour(self)`

Returns True if this is a PGroupPrime or any elements are
instances of PGroupPrime or its sub-classes

##### `help(cls)`

Prints the Pattern class docstring to the console 

##### `invert(self)`

Inverts the values with the Pattern.
        

##### `items(self)`

Returns a generator object equivalent to using enumerate() 

##### `iter(self, *args)`

Repeats this pattern n times but doesn't take nested pattern into account for length

##### `layer(self, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `limit(self, *args)`

Returns a new Pattern generated by adding elements from
this Pattern to a new list and repeatedly calling
`func()` on this list until `func(l)` is greater than `value`
e.g.
```
>>> print( P[0, 1, 2, 3].limit(sum, 10) )
P[0, 1, 2, 3, 0, 1, 2]
```

##### `loop(self, *args)`

Repeats this pattern n times 

##### `make(self)`

This method automatically laces and groups the data 

##### `map(self, func)`

Returns a Pattern that calls `func` on each item 

##### `merge(self, value)`

Merge values into one PGroup 

##### `mirror(self)`

Reverses the pattern. Differs to `Pattern.reverse()` in that
all nested patters are also reversed. 

##### `ne(self, other)`

Not equals operator 

##### `norm(self)`

Returns the pattern with all values between 0 and 1 

##### `offlayer(self, dur, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `palindrome(self, *args)`

Returns the original pattern with mirrored version of itself appended.
a removes values from the middle of the pattern, if positive.
b removes values from the end of the pattern, should be negative.

e.g.

>>> P[:4].palindrome()
P[0, 1, 2, 3, 3, 2, 1, 0]
>>> P[:4].palindrome(1)
P[0, 1, 2, 3, 2, 1, 0]
>>> P[:4].palindrome(-1)
P[0, 1, 2, 3, 3, 2, 1]
>>> P[:4].palindrome(1,-1)
P[0, 1, 2, 3, 2, 1]

##### `pipe(self, pattern)`

Concatonates this patterns stream with another 

##### `pivot(self, *args)`

Mirrors and rotates the Pattern such that the item at index 'i'
is in the same place 

##### `replace(self, sub, repl)`

Replaces any occurrences of "sub" with "repl" 

##### `reverse(self)`

Reverses the contents of the Pattern. Nested patterns are
not reversed. To reverse the contents of nester patterns
use `Pattern.mirror()`

##### `sample(self, *args)`

Returns an n-length pattern from a sample

##### `shuffle(self, n=1)`

Returns a new Pattern with shuffled contents. Note: nested patterns
stay together. To shuffle the contents of nested patterns, use
`deep_shuffle` or `true_shuffle`.

##### `shufflets(self, n)`

Returns a Pattern of 'n' number of PGroups made from shuffled
versions of the original Pattern 

##### `sort(self)`

Used in place of sorted(pattern) to force type 

##### `splice(self, seq, *seqs)`

Takes at least list / Pattern and creates a new Pattern by
adding a value from each pattern in turn to the new pattern.
e.g.
```
>>> P[0,1,2,3].splice([4,5,6,7],[8,9])
P[0,4,8,1,5,9,2,6,8,3,7,9]
```

##### `startswith(self, prefix)`

Returns True if the first item in the Pattern is equal to prefix 

##### `stretch(self, *args)`

Stretches (repeats) the contents until len(Pattern) == size 

##### `string(self)`

Returns a PlayString in string format from the Patterns values 

##### `stutter(self, n=2)`

Returns a new Pattern with each item repeated by `n`. Use
a list of numbers for stutter different items by different
amount. e.g.
```
>>> P[0, 1, 2, 3].stutter([1,3])
P[0, 1, 1, 1, 2, 3, 3, 3]
```

##### `true_copy(self, new_data=None)`

Returns a copy of the Pattern such that items within the
Pattern hold the same state as the original.

##### `true_shuffle(self, n=1)`

Returns a new Pattern with completely shuffle contents such
that nested Patterns are shuffled within the larger Pattern

##### `undup(self)`

Removes any consecutive duplicate numbers from a Pattern 

##### `zip(self, other, dtype=None)`

Zips two patterns together. If one item is a tuple, it extends the tuple / PGroup
i.e. arrow_zip([(0,1),3], [2]) -> [(0,1,2),(3,2)]

##### `zipx(self, other)`

Returns a `Pattern` of `PGroups`, where each `PGroup` contains the i-th
element from each of the argument sequences. The length of the pattern
is the lowest common multiple of the lengths of the two joining patterns. 

---

### `metaPGroupPrime(self, *args, **kwargs)`

Base class for PGroups that take any extra arguments to be stored 

#### Methods

##### `__key(self)`

Returns a tuple of information to identify this Pattern 

##### `__bool__(self)`

Returns True if *any* value in the Pattern are greater than zero 

##### `__eq__(self, other)`

Return self==value.

##### `__ge__(self, other)`

Return self>=value.

##### `__getitem__(self, key)`

Overrides the Pattern.__getitem__ to allow indexing
by TimeVar and PlayerKey instances. 

##### `__gt__(self, other)`

Return self>value.

##### `__hash__(self)`

Return hash(self).

##### `__init__(self, *args, **kwargs)`

Initialize self.  See help(type(self)) for accurate signature.

##### `__invert__(self)`

Using the ~ symbol as a prefix to a Pattern will reverse it.
>>> a = P[:4]
>>> print(a, ~a)
P[0, 1, 2, 3], P[3, 2, 1, 0]

##### `__iter__(self)`

Returns a generator object for this Pattern 

##### `__le__(self, other)`

Return self<=value.

##### `__len__(self)`

Returns the *expanded* length of the pattern such that if the pattern is laced, the
value is the length of the list multiplied by the lowest-common-multiple of the lengths
of nested patterns. e.g. the following are identical:
```
>>> print( len(P[0,1,2,[3,4]]) )
8
>>> print( len(P[0,1,2,3,0,1,2,4]) )
8
```

##### `__lt__(self, other)`

Return self<value.

##### `__ne__(self, other)`

Return self!=value.

##### `__or__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__repr__(self)`

Return repr(self).

##### `__ror__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__setslice__(self, i, j, item)`

Only works in Python 2 

##### `__str__(self)`

Return str(self).

##### `_update_delay(event, delay)`

Updates the delay value in the event dictionary 

##### `_update_sample(event, sample)`

Updates the sample value in the event dictionary 

##### `accum(self, *args)`

Returns a Pattern that is equivalent to list of sums of that
Pattern up to that index.

##### `all(self, func=<lambda>)`

Returns true if all of the patterns contents satisfies func(x) - default is nonzero 

##### `amen(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `arp(self, arp_pattern)`

Return a new Pattern with each item repeated len(arp_pattern) times
and incremented by arp_pattern. Useful for arpeggiating. e.g.
```
>>> P[0, 1, 2, 3].arp([0, 2])
P[0, 2, 1, 3, 2, 4, 3, 5]
```

##### `asGroup(self)`

Returns the Pattern as a PGroup 

##### `bubble(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `calculate_time(self, dur)`

Returns a PGroup of durations to use as the delay argument
when this is a sub-class of `PGroupPrime` 

##### `change_state(self)`

To be overridden by any PGroupPrime that changes state after access by a Player 

##### `choose(self)`

Returns one randomly selected item 

##### `convert_data(self, *args, **kwargs)`

Makes a true copy and converts the data to a given data type 

##### `copy(self)`

Returns a copy of the Pattern such that alterations to the
Pattern.data do not affect the original.

##### `count(self, item)`

Returns the number of occurrences of item in the Pattern

##### `deep_shuffle(self, n=1)`

Returns a new Pattern with shuffled contents and shuffles
any nested patterns. To shuffle the contents of nested patterns
with the rest of the Pattern's contents, use `true_shuffle`.

##### `duplicate(self, *args)`

Repeats this pattern n times but keep nested pattern values 

##### `eq(self, other)`

equals operator 

##### `every(self, n, method, *args, **kwargs)`

Returns the pattern looped n-1 times then appended with
the version returned when method is called on it. 

##### `flatten(self)`

Returns a nested PGroup as un-nested e.g.
::

    >>> P(0,(3,5)).flatten()
    P(0, 3, 5)

##### `get_behaviour(self)`

Returns a function that changes a player event dictionary 

##### `get_methods(cls)`

Returns the methods associated with the `Pattern` class as a list 

##### `getitem(self, key, get_generator=False)`

Called by __getitem__() 

##### `group(self)`

Returns the Pattern as a PGroup 

##### `has_behaviour(self)`

Returns True if this is a PGroupPrime or any elements are
instances of PGroupPrime or its sub-classes

##### `help(cls)`

Prints the Pattern class docstring to the console 

##### `invert(self)`

Inverts the values with the Pattern.
        

##### `items(self)`

Returns a generator object equivalent to using enumerate() 

##### `iter(self, *args)`

Repeats this pattern n times but doesn't take nested pattern into account for length

##### `layer(self, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `limit(self, *args)`

Returns a new Pattern generated by adding elements from
this Pattern to a new list and repeatedly calling
`func()` on this list until `func(l)` is greater than `value`
e.g.
```
>>> print( P[0, 1, 2, 3].limit(sum, 10) )
P[0, 1, 2, 3, 0, 1, 2]
```

##### `loop(self, *args)`

Repeats this pattern n times 

##### `make(self)`

This method automatically laces and groups the data 

##### `map(self, func)`

Returns a Pattern that calls `func` on each item 

##### `merge(self, value)`

Merge values into one PGroup 

##### `mirror(self)`

Reverses the pattern. Differs to `Pattern.reverse()` in that
all nested patters are also reversed. 

##### `ne(self, other)`

Not equals operator 

##### `norm(self)`

Returns the pattern with all values between 0 and 1 

##### `offlayer(self, dur, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `palindrome(self, *args)`

Returns the original pattern with mirrored version of itself appended.
a removes values from the middle of the pattern, if positive.
b removes values from the end of the pattern, should be negative.

e.g.

>>> P[:4].palindrome()
P[0, 1, 2, 3, 3, 2, 1, 0]
>>> P[:4].palindrome(1)
P[0, 1, 2, 3, 2, 1, 0]
>>> P[:4].palindrome(-1)
P[0, 1, 2, 3, 3, 2, 1]
>>> P[:4].palindrome(1,-1)
P[0, 1, 2, 3, 2, 1]

##### `pipe(self, pattern)`

Concatonates this patterns stream with another 

##### `pivot(self, *args)`

Mirrors and rotates the Pattern such that the item at index 'i'
is in the same place 

##### `replace(self, sub, repl)`

Replaces any occurrences of "sub" with "repl" 

##### `reverse(self)`

Reverses the contents of the Pattern. Nested patterns are
not reversed. To reverse the contents of nester patterns
use `Pattern.mirror()`

##### `sample(self, *args)`

Returns an n-length pattern from a sample

##### `shuffle(self, n=1)`

Returns a new Pattern with shuffled contents. Note: nested patterns
stay together. To shuffle the contents of nested patterns, use
`deep_shuffle` or `true_shuffle`.

##### `shufflets(self, n)`

Returns a Pattern of 'n' number of PGroups made from shuffled
versions of the original Pattern 

##### `sort(self)`

Used in place of sorted(pattern) to force type 

##### `splice(self, seq, *seqs)`

Takes at least list / Pattern and creates a new Pattern by
adding a value from each pattern in turn to the new pattern.
e.g.
```
>>> P[0,1,2,3].splice([4,5,6,7],[8,9])
P[0,4,8,1,5,9,2,6,8,3,7,9]
```

##### `startswith(self, prefix)`

Returns True if the first item in the Pattern is equal to prefix 

##### `stretch(self, *args)`

Stretches (repeats) the contents until len(Pattern) == size 

##### `string(self)`

Returns a PlayString in string format from the Patterns values 

##### `stutter(self, n=2)`

Returns a new Pattern with each item repeated by `n`. Use
a list of numbers for stutter different items by different
amount. e.g.
```
>>> P[0, 1, 2, 3].stutter([1,3])
P[0, 1, 1, 1, 2, 3, 3, 3]
```

##### `true_copy(self, new_data=None)`

Returns a copy of the Pattern such that items within the
Pattern hold the same state as the original.

##### `true_shuffle(self, n=1)`

Returns a new Pattern with completely shuffle contents such
that nested Patterns are shuffled within the larger Pattern

##### `undup(self)`

Removes any consecutive duplicate numbers from a Pattern 

##### `zip(self, other, dtype=None)`

Zips two patterns together. If one item is a tuple, it extends the tuple / PGroup
i.e. arrow_zip([(0,1),3], [2]) -> [(0,1,2),(3,2)]

##### `zipx(self, other)`

Returns a `Pattern` of `PGroups`, where each `PGroup` contains the i-th
element from each of the argument sequences. The length of the pattern
is the lowest common multiple of the lengths of the two joining patterns. 

---

### `PGroupStar(self, seq=[], *args)`

Stutters the values over the length of and event's 'dur' 

#### Methods

##### `__key(self)`

Returns a tuple of information to identify this Pattern 

##### `__bool__(self)`

Returns True if *any* value in the Pattern are greater than zero 

##### `__eq__(self, other)`

Return self==value.

##### `__ge__(self, other)`

Return self>=value.

##### `__getitem__(self, key)`

Overrides the Pattern.__getitem__ to allow indexing
by TimeVar and PlayerKey instances. 

##### `__gt__(self, other)`

Return self>value.

##### `__hash__(self)`

Return hash(self).

##### `__init__(self, seq=[], *args)`

Initialize self.  See help(type(self)) for accurate signature.

##### `__invert__(self)`

Using the ~ symbol as a prefix to a Pattern will reverse it.
>>> a = P[:4]
>>> print(a, ~a)
P[0, 1, 2, 3], P[3, 2, 1, 0]

##### `__iter__(self)`

Returns a generator object for this Pattern 

##### `__le__(self, other)`

Return self<=value.

##### `__len__(self)`

Returns the *expanded* length of the pattern such that if the pattern is laced, the
value is the length of the list multiplied by the lowest-common-multiple of the lengths
of nested patterns. e.g. the following are identical:
```
>>> print( len(P[0,1,2,[3,4]]) )
8
>>> print( len(P[0,1,2,3,0,1,2,4]) )
8
```

##### `__lt__(self, other)`

Return self<value.

##### `__ne__(self, other)`

Return self!=value.

##### `__or__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__repr__(self)`

Return repr(self).

##### `__ror__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__setslice__(self, i, j, item)`

Only works in Python 2 

##### `__str__(self)`

Return str(self).

##### `_update_delay(event, delay)`

Updates the delay value in the event dictionary 

##### `_update_sample(event, sample)`

Updates the sample value in the event dictionary 

##### `accum(self, *args)`

Returns a Pattern that is equivalent to list of sums of that
Pattern up to that index.

##### `all(self, func=<lambda>)`

Returns true if all of the patterns contents satisfies func(x) - default is nonzero 

##### `amen(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `arp(self, arp_pattern)`

Return a new Pattern with each item repeated len(arp_pattern) times
and incremented by arp_pattern. Useful for arpeggiating. e.g.
```
>>> P[0, 1, 2, 3].arp([0, 2])
P[0, 2, 1, 3, 2, 4, 3, 5]
```

##### `asGroup(self)`

Returns the Pattern as a PGroup 

##### `bubble(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `calculate_time(self, dur)`

Returns a PGroup of durations to use as the delay argument
when this is a sub-class of `PGroupPrime` 

##### `change_state(self)`

To be overridden by any PGroupPrime that changes state after access by a Player 

##### `choose(self)`

Returns one randomly selected item 

##### `convert_data(self, *args, **kwargs)`

Makes a true copy and converts the data to a given data type 

##### `copy(self)`

Returns a copy of the Pattern such that alterations to the
Pattern.data do not affect the original.

##### `count(self, item)`

Returns the number of occurrences of item in the Pattern

##### `deep_shuffle(self, n=1)`

Returns a new Pattern with shuffled contents and shuffles
any nested patterns. To shuffle the contents of nested patterns
with the rest of the Pattern's contents, use `true_shuffle`.

##### `duplicate(self, *args)`

Repeats this pattern n times but keep nested pattern values 

##### `eq(self, other)`

equals operator 

##### `every(self, n, method, *args, **kwargs)`

Returns the pattern looped n-1 times then appended with
the version returned when method is called on it. 

##### `flatten(self)`

Returns a nested PGroup as un-nested e.g.
::

    >>> P(0,(3,5)).flatten()
    P(0, 3, 5)

##### `get_behaviour(self)`

Returns a function that changes a player event dictionary 

##### `get_methods(cls)`

Returns the methods associated with the `Pattern` class as a list 

##### `getitem(self, key, get_generator=False)`

Called by __getitem__() 

##### `group(self)`

Returns the Pattern as a PGroup 

##### `has_behaviour(self)`

Returns True if this is a PGroupPrime or any elements are
instances of PGroupPrime or its sub-classes

##### `help(cls)`

Prints the Pattern class docstring to the console 

##### `invert(self)`

Inverts the values with the Pattern.
        

##### `items(self)`

Returns a generator object equivalent to using enumerate() 

##### `iter(self, *args)`

Repeats this pattern n times but doesn't take nested pattern into account for length

##### `layer(self, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `limit(self, *args)`

Returns a new Pattern generated by adding elements from
this Pattern to a new list and repeatedly calling
`func()` on this list until `func(l)` is greater than `value`
e.g.
```
>>> print( P[0, 1, 2, 3].limit(sum, 10) )
P[0, 1, 2, 3, 0, 1, 2]
```

##### `loop(self, *args)`

Repeats this pattern n times 

##### `make(self)`

This method automatically laces and groups the data 

##### `map(self, func)`

Returns a Pattern that calls `func` on each item 

##### `merge(self, value)`

Merge values into one PGroup 

##### `mirror(self)`

Reverses the pattern. Differs to `Pattern.reverse()` in that
all nested patters are also reversed. 

##### `ne(self, other)`

Not equals operator 

##### `norm(self)`

Returns the pattern with all values between 0 and 1 

##### `offlayer(self, dur, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `palindrome(self, *args)`

Returns the original pattern with mirrored version of itself appended.
a removes values from the middle of the pattern, if positive.
b removes values from the end of the pattern, should be negative.

e.g.

>>> P[:4].palindrome()
P[0, 1, 2, 3, 3, 2, 1, 0]
>>> P[:4].palindrome(1)
P[0, 1, 2, 3, 2, 1, 0]
>>> P[:4].palindrome(-1)
P[0, 1, 2, 3, 3, 2, 1]
>>> P[:4].palindrome(1,-1)
P[0, 1, 2, 3, 2, 1]

##### `pipe(self, pattern)`

Concatonates this patterns stream with another 

##### `pivot(self, *args)`

Mirrors and rotates the Pattern such that the item at index 'i'
is in the same place 

##### `replace(self, sub, repl)`

Replaces any occurrences of "sub" with "repl" 

##### `reverse(self)`

Reverses the contents of the Pattern. Nested patterns are
not reversed. To reverse the contents of nester patterns
use `Pattern.mirror()`

##### `sample(self, *args)`

Returns an n-length pattern from a sample

##### `shuffle(self, n=1)`

Returns a new Pattern with shuffled contents. Note: nested patterns
stay together. To shuffle the contents of nested patterns, use
`deep_shuffle` or `true_shuffle`.

##### `shufflets(self, n)`

Returns a Pattern of 'n' number of PGroups made from shuffled
versions of the original Pattern 

##### `sort(self)`

Used in place of sorted(pattern) to force type 

##### `splice(self, seq, *seqs)`

Takes at least list / Pattern and creates a new Pattern by
adding a value from each pattern in turn to the new pattern.
e.g.
```
>>> P[0,1,2,3].splice([4,5,6,7],[8,9])
P[0,4,8,1,5,9,2,6,8,3,7,9]
```

##### `startswith(self, prefix)`

Returns True if the first item in the Pattern is equal to prefix 

##### `stretch(self, *args)`

Stretches (repeats) the contents until len(Pattern) == size 

##### `string(self)`

Returns a PlayString in string format from the Patterns values 

##### `stutter(self, n=2)`

Returns a new Pattern with each item repeated by `n`. Use
a list of numbers for stutter different items by different
amount. e.g.
```
>>> P[0, 1, 2, 3].stutter([1,3])
P[0, 1, 1, 1, 2, 3, 3, 3]
```

##### `true_copy(self, new_data=None)`

Returns a copy of the Pattern such that items within the
Pattern hold the same state as the original.

##### `true_shuffle(self, n=1)`

Returns a new Pattern with completely shuffle contents such
that nested Patterns are shuffled within the larger Pattern

##### `undup(self)`

Removes any consecutive duplicate numbers from a Pattern 

##### `zip(self, other, dtype=None)`

Zips two patterns together. If one item is a tuple, it extends the tuple / PGroup
i.e. arrow_zip([(0,1),3], [2]) -> [(0,1,2),(3,2)]

##### `zipx(self, other)`

Returns a `Pattern` of `PGroups`, where each `PGroup` contains the i-th
element from each of the argument sequences. The length of the pattern
is the lowest common multiple of the lengths of the two joining patterns. 

---

### `PGroupPlus(self, seq=[], *args)`

Stutters the values over the length of and event's 'sus' 

#### Methods

##### `__key(self)`

Returns a tuple of information to identify this Pattern 

##### `__bool__(self)`

Returns True if *any* value in the Pattern are greater than zero 

##### `__eq__(self, other)`

Return self==value.

##### `__ge__(self, other)`

Return self>=value.

##### `__getitem__(self, key)`

Overrides the Pattern.__getitem__ to allow indexing
by TimeVar and PlayerKey instances. 

##### `__gt__(self, other)`

Return self>value.

##### `__hash__(self)`

Return hash(self).

##### `__init__(self, seq=[], *args)`

Initialize self.  See help(type(self)) for accurate signature.

##### `__invert__(self)`

Using the ~ symbol as a prefix to a Pattern will reverse it.
>>> a = P[:4]
>>> print(a, ~a)
P[0, 1, 2, 3], P[3, 2, 1, 0]

##### `__iter__(self)`

Returns a generator object for this Pattern 

##### `__le__(self, other)`

Return self<=value.

##### `__len__(self)`

Returns the *expanded* length of the pattern such that if the pattern is laced, the
value is the length of the list multiplied by the lowest-common-multiple of the lengths
of nested patterns. e.g. the following are identical:
```
>>> print( len(P[0,1,2,[3,4]]) )
8
>>> print( len(P[0,1,2,3,0,1,2,4]) )
8
```

##### `__lt__(self, other)`

Return self<value.

##### `__ne__(self, other)`

Return self!=value.

##### `__or__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__repr__(self)`

Return repr(self).

##### `__ror__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__setslice__(self, i, j, item)`

Only works in Python 2 

##### `__str__(self)`

Return str(self).

##### `_update_delay(event, delay)`

Updates the delay value in the event dictionary 

##### `_update_sample(event, sample)`

Updates the sample value in the event dictionary 

##### `accum(self, *args)`

Returns a Pattern that is equivalent to list of sums of that
Pattern up to that index.

##### `all(self, func=<lambda>)`

Returns true if all of the patterns contents satisfies func(x) - default is nonzero 

##### `amen(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `arp(self, arp_pattern)`

Return a new Pattern with each item repeated len(arp_pattern) times
and incremented by arp_pattern. Useful for arpeggiating. e.g.
```
>>> P[0, 1, 2, 3].arp([0, 2])
P[0, 2, 1, 3, 2, 4, 3, 5]
```

##### `asGroup(self)`

Returns the Pattern as a PGroup 

##### `bubble(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `calculate_time(self, dur)`

Returns a PGroup of durations to use as the delay argument
when this is a sub-class of `PGroupPrime` 

##### `change_state(self)`

To be overridden by any PGroupPrime that changes state after access by a Player 

##### `choose(self)`

Returns one randomly selected item 

##### `convert_data(self, *args, **kwargs)`

Makes a true copy and converts the data to a given data type 

##### `copy(self)`

Returns a copy of the Pattern such that alterations to the
Pattern.data do not affect the original.

##### `count(self, item)`

Returns the number of occurrences of item in the Pattern

##### `deep_shuffle(self, n=1)`

Returns a new Pattern with shuffled contents and shuffles
any nested patterns. To shuffle the contents of nested patterns
with the rest of the Pattern's contents, use `true_shuffle`.

##### `duplicate(self, *args)`

Repeats this pattern n times but keep nested pattern values 

##### `eq(self, other)`

equals operator 

##### `every(self, n, method, *args, **kwargs)`

Returns the pattern looped n-1 times then appended with
the version returned when method is called on it. 

##### `flatten(self)`

Returns a nested PGroup as un-nested e.g.
::

    >>> P(0,(3,5)).flatten()
    P(0, 3, 5)

##### `get_behaviour(self)`

Returns a function that modulates a player event dictionary 

##### `get_methods(cls)`

Returns the methods associated with the `Pattern` class as a list 

##### `getitem(self, key, get_generator=False)`

Called by __getitem__() 

##### `group(self)`

Returns the Pattern as a PGroup 

##### `has_behaviour(self)`

Returns True if this is a PGroupPrime or any elements are
instances of PGroupPrime or its sub-classes

##### `help(cls)`

Prints the Pattern class docstring to the console 

##### `invert(self)`

Inverts the values with the Pattern.
        

##### `items(self)`

Returns a generator object equivalent to using enumerate() 

##### `iter(self, *args)`

Repeats this pattern n times but doesn't take nested pattern into account for length

##### `layer(self, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `limit(self, *args)`

Returns a new Pattern generated by adding elements from
this Pattern to a new list and repeatedly calling
`func()` on this list until `func(l)` is greater than `value`
e.g.
```
>>> print( P[0, 1, 2, 3].limit(sum, 10) )
P[0, 1, 2, 3, 0, 1, 2]
```

##### `loop(self, *args)`

Repeats this pattern n times 

##### `make(self)`

This method automatically laces and groups the data 

##### `map(self, func)`

Returns a Pattern that calls `func` on each item 

##### `merge(self, value)`

Merge values into one PGroup 

##### `mirror(self)`

Reverses the pattern. Differs to `Pattern.reverse()` in that
all nested patters are also reversed. 

##### `ne(self, other)`

Not equals operator 

##### `norm(self)`

Returns the pattern with all values between 0 and 1 

##### `offlayer(self, dur, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `palindrome(self, *args)`

Returns the original pattern with mirrored version of itself appended.
a removes values from the middle of the pattern, if positive.
b removes values from the end of the pattern, should be negative.

e.g.

>>> P[:4].palindrome()
P[0, 1, 2, 3, 3, 2, 1, 0]
>>> P[:4].palindrome(1)
P[0, 1, 2, 3, 2, 1, 0]
>>> P[:4].palindrome(-1)
P[0, 1, 2, 3, 3, 2, 1]
>>> P[:4].palindrome(1,-1)
P[0, 1, 2, 3, 2, 1]

##### `pipe(self, pattern)`

Concatonates this patterns stream with another 

##### `pivot(self, *args)`

Mirrors and rotates the Pattern such that the item at index 'i'
is in the same place 

##### `replace(self, sub, repl)`

Replaces any occurrences of "sub" with "repl" 

##### `reverse(self)`

Reverses the contents of the Pattern. Nested patterns are
not reversed. To reverse the contents of nester patterns
use `Pattern.mirror()`

##### `sample(self, *args)`

Returns an n-length pattern from a sample

##### `shuffle(self, n=1)`

Returns a new Pattern with shuffled contents. Note: nested patterns
stay together. To shuffle the contents of nested patterns, use
`deep_shuffle` or `true_shuffle`.

##### `shufflets(self, n)`

Returns a Pattern of 'n' number of PGroups made from shuffled
versions of the original Pattern 

##### `sort(self)`

Used in place of sorted(pattern) to force type 

##### `splice(self, seq, *seqs)`

Takes at least list / Pattern and creates a new Pattern by
adding a value from each pattern in turn to the new pattern.
e.g.
```
>>> P[0,1,2,3].splice([4,5,6,7],[8,9])
P[0,4,8,1,5,9,2,6,8,3,7,9]
```

##### `startswith(self, prefix)`

Returns True if the first item in the Pattern is equal to prefix 

##### `stretch(self, *args)`

Stretches (repeats) the contents until len(Pattern) == size 

##### `string(self)`

Returns a PlayString in string format from the Patterns values 

##### `stutter(self, n=2)`

Returns a new Pattern with each item repeated by `n`. Use
a list of numbers for stutter different items by different
amount. e.g.
```
>>> P[0, 1, 2, 3].stutter([1,3])
P[0, 1, 1, 1, 2, 3, 3, 3]
```

##### `true_copy(self, new_data=None)`

Returns a copy of the Pattern such that items within the
Pattern hold the same state as the original.

##### `true_shuffle(self, n=1)`

Returns a new Pattern with completely shuffle contents such
that nested Patterns are shuffled within the larger Pattern

##### `undup(self)`

Removes any consecutive duplicate numbers from a Pattern 

##### `zip(self, other, dtype=None)`

Zips two patterns together. If one item is a tuple, it extends the tuple / PGroup
i.e. arrow_zip([(0,1),3], [2]) -> [(0,1,2),(3,2)]

##### `zipx(self, other)`

Returns a `Pattern` of `PGroups`, where each `PGroup` contains the i-th
element from each of the argument sequences. The length of the pattern
is the lowest common multiple of the lengths of the two joining patterns. 

---

### `PGroupPow(self, seq=[], *args)`

Stutters a shuffled version the values over the length of and event's 'dur' 

#### Methods

##### `__key(self)`

Returns a tuple of information to identify this Pattern 

##### `__bool__(self)`

Returns True if *any* value in the Pattern are greater than zero 

##### `__eq__(self, other)`

Return self==value.

##### `__ge__(self, other)`

Return self>=value.

##### `__getitem__(self, key)`

Overrides the Pattern.__getitem__ to allow indexing
by TimeVar and PlayerKey instances. 

##### `__gt__(self, other)`

Return self>value.

##### `__hash__(self)`

Return hash(self).

##### `__init__(self, seq=[], *args)`

Initialize self.  See help(type(self)) for accurate signature.

##### `__invert__(self)`

Using the ~ symbol as a prefix to a Pattern will reverse it.
>>> a = P[:4]
>>> print(a, ~a)
P[0, 1, 2, 3], P[3, 2, 1, 0]

##### `__iter__(self)`

Returns a generator object for this Pattern 

##### `__le__(self, other)`

Return self<=value.

##### `__len__(self)`

Returns the *expanded* length of the pattern such that if the pattern is laced, the
value is the length of the list multiplied by the lowest-common-multiple of the lengths
of nested patterns. e.g. the following are identical:
```
>>> print( len(P[0,1,2,[3,4]]) )
8
>>> print( len(P[0,1,2,3,0,1,2,4]) )
8
```

##### `__lt__(self, other)`

Return self<value.

##### `__ne__(self, other)`

Return self!=value.

##### `__or__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__repr__(self)`

Return repr(self).

##### `__ror__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__setslice__(self, i, j, item)`

Only works in Python 2 

##### `__str__(self)`

Return str(self).

##### `_update_delay(event, delay)`

Updates the delay value in the event dictionary 

##### `_update_sample(event, sample)`

Updates the sample value in the event dictionary 

##### `accum(self, *args)`

Returns a Pattern that is equivalent to list of sums of that
Pattern up to that index.

##### `all(self, func=<lambda>)`

Returns true if all of the patterns contents satisfies func(x) - default is nonzero 

##### `amen(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `arp(self, arp_pattern)`

Return a new Pattern with each item repeated len(arp_pattern) times
and incremented by arp_pattern. Useful for arpeggiating. e.g.
```
>>> P[0, 1, 2, 3].arp([0, 2])
P[0, 2, 1, 3, 2, 4, 3, 5]
```

##### `asGroup(self)`

Returns the Pattern as a PGroup 

##### `bubble(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `calculate_time(self, dur)`

Returns a PGroup of durations to use as the delay argument
when this is a sub-class of `PGroupPrime` 

##### `change_state(self)`

To be overridden by any PGroupPrime that changes state after access by a Player 

##### `choose(self)`

Returns one randomly selected item 

##### `convert_data(self, *args, **kwargs)`

Makes a true copy and converts the data to a given data type 

##### `copy(self)`

Returns a copy of the Pattern such that alterations to the
Pattern.data do not affect the original.

##### `count(self, item)`

Returns the number of occurrences of item in the Pattern

##### `deep_shuffle(self, n=1)`

Returns a new Pattern with shuffled contents and shuffles
any nested patterns. To shuffle the contents of nested patterns
with the rest of the Pattern's contents, use `true_shuffle`.

##### `duplicate(self, *args)`

Repeats this pattern n times but keep nested pattern values 

##### `eq(self, other)`

equals operator 

##### `every(self, n, method, *args, **kwargs)`

Returns the pattern looped n-1 times then appended with
the version returned when method is called on it. 

##### `flatten(self)`

Returns a nested PGroup as un-nested e.g.
::

    >>> P(0,(3,5)).flatten()
    P(0, 3, 5)

##### `get_behaviour(self)`

Returns a function that changes a player event dictionary 

##### `get_methods(cls)`

Returns the methods associated with the `Pattern` class as a list 

##### `getitem(self, key, get_generator=False)`

Called by __getitem__() 

##### `group(self)`

Returns the Pattern as a PGroup 

##### `has_behaviour(self)`

Returns True if this is a PGroupPrime or any elements are
instances of PGroupPrime or its sub-classes

##### `help(cls)`

Prints the Pattern class docstring to the console 

##### `invert(self)`

Inverts the values with the Pattern.
        

##### `items(self)`

Returns a generator object equivalent to using enumerate() 

##### `iter(self, *args)`

Repeats this pattern n times but doesn't take nested pattern into account for length

##### `layer(self, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `limit(self, *args)`

Returns a new Pattern generated by adding elements from
this Pattern to a new list and repeatedly calling
`func()` on this list until `func(l)` is greater than `value`
e.g.
```
>>> print( P[0, 1, 2, 3].limit(sum, 10) )
P[0, 1, 2, 3, 0, 1, 2]
```

##### `loop(self, *args)`

Repeats this pattern n times 

##### `make(self)`

This method automatically laces and groups the data 

##### `map(self, func)`

Returns a Pattern that calls `func` on each item 

##### `merge(self, value)`

Merge values into one PGroup 

##### `mirror(self)`

Reverses the pattern. Differs to `Pattern.reverse()` in that
all nested patters are also reversed. 

##### `ne(self, other)`

Not equals operator 

##### `norm(self)`

Returns the pattern with all values between 0 and 1 

##### `offlayer(self, dur, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `palindrome(self, *args)`

Returns the original pattern with mirrored version of itself appended.
a removes values from the middle of the pattern, if positive.
b removes values from the end of the pattern, should be negative.

e.g.

>>> P[:4].palindrome()
P[0, 1, 2, 3, 3, 2, 1, 0]
>>> P[:4].palindrome(1)
P[0, 1, 2, 3, 2, 1, 0]
>>> P[:4].palindrome(-1)
P[0, 1, 2, 3, 3, 2, 1]
>>> P[:4].palindrome(1,-1)
P[0, 1, 2, 3, 2, 1]

##### `pipe(self, pattern)`

Concatonates this patterns stream with another 

##### `pivot(self, *args)`

Mirrors and rotates the Pattern such that the item at index 'i'
is in the same place 

##### `replace(self, sub, repl)`

Replaces any occurrences of "sub" with "repl" 

##### `reverse(self)`

Reverses the contents of the Pattern. Nested patterns are
not reversed. To reverse the contents of nester patterns
use `Pattern.mirror()`

##### `sample(self, *args)`

Returns an n-length pattern from a sample

##### `shuffle(self, n=1)`

Returns a new Pattern with shuffled contents. Note: nested patterns
stay together. To shuffle the contents of nested patterns, use
`deep_shuffle` or `true_shuffle`.

##### `shufflets(self, n)`

Returns a Pattern of 'n' number of PGroups made from shuffled
versions of the original Pattern 

##### `sort(self)`

Used in place of sorted(pattern) to force type 

##### `splice(self, seq, *seqs)`

Takes at least list / Pattern and creates a new Pattern by
adding a value from each pattern in turn to the new pattern.
e.g.
```
>>> P[0,1,2,3].splice([4,5,6,7],[8,9])
P[0,4,8,1,5,9,2,6,8,3,7,9]
```

##### `startswith(self, prefix)`

Returns True if the first item in the Pattern is equal to prefix 

##### `stretch(self, *args)`

Stretches (repeats) the contents until len(Pattern) == size 

##### `string(self)`

Returns a PlayString in string format from the Patterns values 

##### `stutter(self, n=2)`

Returns a new Pattern with each item repeated by `n`. Use
a list of numbers for stutter different items by different
amount. e.g.
```
>>> P[0, 1, 2, 3].stutter([1,3])
P[0, 1, 1, 1, 2, 3, 3, 3]
```

##### `true_copy(self, new_data=None)`

Returns a copy of the Pattern such that items within the
Pattern hold the same state as the original.

##### `true_shuffle(self, n=1)`

Returns a new Pattern with completely shuffle contents such
that nested Patterns are shuffled within the larger Pattern

##### `undup(self)`

Removes any consecutive duplicate numbers from a Pattern 

##### `zip(self, other, dtype=None)`

Zips two patterns together. If one item is a tuple, it extends the tuple / PGroup
i.e. arrow_zip([(0,1),3], [2]) -> [(0,1,2),(3,2)]

##### `zipx(self, other)`

Returns a `Pattern` of `PGroups`, where each `PGroup` contains the i-th
element from each of the argument sequences. The length of the pattern
is the lowest common multiple of the lengths of the two joining patterns. 

---

### `PGroupDiv(self, *args, **kwargs)`

Stutter every other request 

#### Methods

##### `__key(self)`

Returns a tuple of information to identify this Pattern 

##### `__bool__(self)`

Returns True if *any* value in the Pattern are greater than zero 

##### `__eq__(self, other)`

Return self==value.

##### `__ge__(self, other)`

Return self>=value.

##### `__getitem__(self, key)`

Overrides the Pattern.__getitem__ to allow indexing
by TimeVar and PlayerKey instances. 

##### `__gt__(self, other)`

Return self>value.

##### `__hash__(self)`

Return hash(self).

##### `__init__(self, *args, **kwargs)`

Initialize self.  See help(type(self)) for accurate signature.

##### `__invert__(self)`

Using the ~ symbol as a prefix to a Pattern will reverse it.
>>> a = P[:4]
>>> print(a, ~a)
P[0, 1, 2, 3], P[3, 2, 1, 0]

##### `__iter__(self)`

Returns a generator object for this Pattern 

##### `__le__(self, other)`

Return self<=value.

##### `__len__(self)`

Returns the *expanded* length of the pattern such that if the pattern is laced, the
value is the length of the list multiplied by the lowest-common-multiple of the lengths
of nested patterns. e.g. the following are identical:
```
>>> print( len(P[0,1,2,[3,4]]) )
8
>>> print( len(P[0,1,2,3,0,1,2,4]) )
8
```

##### `__lt__(self, other)`

Return self<value.

##### `__ne__(self, other)`

Return self!=value.

##### `__or__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__repr__(self)`

Return repr(self).

##### `__ror__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__setslice__(self, i, j, item)`

Only works in Python 2 

##### `__str__(self)`

Return str(self).

##### `_update_delay(event, delay)`

Updates the delay value in the event dictionary 

##### `_update_sample(event, sample)`

Updates the sample value in the event dictionary 

##### `accum(self, *args)`

Returns a Pattern that is equivalent to list of sums of that
Pattern up to that index.

##### `all(self, func=<lambda>)`

Returns true if all of the patterns contents satisfies func(x) - default is nonzero 

##### `amen(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `arp(self, arp_pattern)`

Return a new Pattern with each item repeated len(arp_pattern) times
and incremented by arp_pattern. Useful for arpeggiating. e.g.
```
>>> P[0, 1, 2, 3].arp([0, 2])
P[0, 2, 1, 3, 2, 4, 3, 5]
```

##### `asGroup(self)`

Returns the Pattern as a PGroup 

##### `bubble(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `calculate_time(self, dur)`

Returns a PGroup of durations to use as the delay argument
when this is a sub-class of `PGroupPrime` 

##### `change_state(self)`

To be overridden by any PGroupPrime that changes state after access by a Player 

##### `choose(self)`

Returns one randomly selected item 

##### `convert_data(self, *args, **kwargs)`

Makes a true copy and converts the data to a given data type 

##### `copy(self)`

Returns a copy of the Pattern such that alterations to the
Pattern.data do not affect the original.

##### `count(self, item)`

Returns the number of occurrences of item in the Pattern

##### `deep_shuffle(self, n=1)`

Returns a new Pattern with shuffled contents and shuffles
any nested patterns. To shuffle the contents of nested patterns
with the rest of the Pattern's contents, use `true_shuffle`.

##### `duplicate(self, *args)`

Repeats this pattern n times but keep nested pattern values 

##### `eq(self, other)`

equals operator 

##### `every(self, n, method, *args, **kwargs)`

Returns the pattern looped n-1 times then appended with
the version returned when method is called on it. 

##### `flatten(self)`

Returns a nested PGroup as un-nested e.g.
::

    >>> P(0,(3,5)).flatten()
    P(0, 3, 5)

##### `get_behaviour(self)`

Returns a function that changes a player event dictionary 

##### `get_methods(cls)`

Returns the methods associated with the `Pattern` class as a list 

##### `getitem(self, key, get_generator=False)`

Called by __getitem__() 

##### `group(self)`

Returns the Pattern as a PGroup 

##### `has_behaviour(self)`

Returns True if this is a PGroupPrime or any elements are
instances of PGroupPrime or its sub-classes

##### `help(cls)`

Prints the Pattern class docstring to the console 

##### `invert(self)`

Inverts the values with the Pattern.
        

##### `items(self)`

Returns a generator object equivalent to using enumerate() 

##### `iter(self, *args)`

Repeats this pattern n times but doesn't take nested pattern into account for length

##### `layer(self, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `limit(self, *args)`

Returns a new Pattern generated by adding elements from
this Pattern to a new list and repeatedly calling
`func()` on this list until `func(l)` is greater than `value`
e.g.
```
>>> print( P[0, 1, 2, 3].limit(sum, 10) )
P[0, 1, 2, 3, 0, 1, 2]
```

##### `loop(self, *args)`

Repeats this pattern n times 

##### `make(self)`

This method automatically laces and groups the data 

##### `map(self, func)`

Returns a Pattern that calls `func` on each item 

##### `merge(self, value)`

Merge values into one PGroup 

##### `mirror(self)`

Reverses the pattern. Differs to `Pattern.reverse()` in that
all nested patters are also reversed. 

##### `ne(self, other)`

Not equals operator 

##### `norm(self)`

Returns the pattern with all values between 0 and 1 

##### `offlayer(self, dur, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `palindrome(self, *args)`

Returns the original pattern with mirrored version of itself appended.
a removes values from the middle of the pattern, if positive.
b removes values from the end of the pattern, should be negative.

e.g.

>>> P[:4].palindrome()
P[0, 1, 2, 3, 3, 2, 1, 0]
>>> P[:4].palindrome(1)
P[0, 1, 2, 3, 2, 1, 0]
>>> P[:4].palindrome(-1)
P[0, 1, 2, 3, 3, 2, 1]
>>> P[:4].palindrome(1,-1)
P[0, 1, 2, 3, 2, 1]

##### `pipe(self, pattern)`

Concatonates this patterns stream with another 

##### `pivot(self, *args)`

Mirrors and rotates the Pattern such that the item at index 'i'
is in the same place 

##### `replace(self, sub, repl)`

Replaces any occurrences of "sub" with "repl" 

##### `reverse(self)`

Reverses the contents of the Pattern. Nested patterns are
not reversed. To reverse the contents of nester patterns
use `Pattern.mirror()`

##### `sample(self, *args)`

Returns an n-length pattern from a sample

##### `shuffle(self, n=1)`

Returns a new Pattern with shuffled contents. Note: nested patterns
stay together. To shuffle the contents of nested patterns, use
`deep_shuffle` or `true_shuffle`.

##### `shufflets(self, n)`

Returns a Pattern of 'n' number of PGroups made from shuffled
versions of the original Pattern 

##### `sort(self)`

Used in place of sorted(pattern) to force type 

##### `splice(self, seq, *seqs)`

Takes at least list / Pattern and creates a new Pattern by
adding a value from each pattern in turn to the new pattern.
e.g.
```
>>> P[0,1,2,3].splice([4,5,6,7],[8,9])
P[0,4,8,1,5,9,2,6,8,3,7,9]
```

##### `startswith(self, prefix)`

Returns True if the first item in the Pattern is equal to prefix 

##### `stretch(self, *args)`

Stretches (repeats) the contents until len(Pattern) == size 

##### `string(self)`

Returns a PlayString in string format from the Patterns values 

##### `stutter(self, n=2)`

Returns a new Pattern with each item repeated by `n`. Use
a list of numbers for stutter different items by different
amount. e.g.
```
>>> P[0, 1, 2, 3].stutter([1,3])
P[0, 1, 1, 1, 2, 3, 3, 3]
```

##### `true_copy(self, new_data=None)`

Returns a copy of the Pattern such that items within the
Pattern hold the same state as the original.

##### `true_shuffle(self, n=1)`

Returns a new Pattern with completely shuffle contents such
that nested Patterns are shuffled within the larger Pattern

##### `undup(self)`

Removes any consecutive duplicate numbers from a Pattern 

##### `zip(self, other, dtype=None)`

Zips two patterns together. If one item is a tuple, it extends the tuple / PGroup
i.e. arrow_zip([(0,1),3], [2]) -> [(0,1,2),(3,2)]

##### `zipx(self, other)`

Returns a `Pattern` of `PGroups`, where each `PGroup` contains the i-th
element from each of the argument sequences. The length of the pattern
is the lowest common multiple of the lengths of the two joining patterns. 

---

### `PGroupMod(self, seq=[], *args)`

OBSOLETE
--------
Useful for when you want many nested groups. This PGroup flattens the original
but the delay times are calculated in the same way as if the values were neseted

#### Methods

##### `__key(self)`

Returns a tuple of information to identify this Pattern 

##### `__bool__(self)`

Returns True if *any* value in the Pattern are greater than zero 

##### `__eq__(self, other)`

Return self==value.

##### `__ge__(self, other)`

Return self>=value.

##### `__getitem__(self, key)`

Overrides the Pattern.__getitem__ to allow indexing
by TimeVar and PlayerKey instances. 

##### `__gt__(self, other)`

Return self>value.

##### `__hash__(self)`

Return hash(self).

##### `__init__(self, seq=[], *args)`

Initialize self.  See help(type(self)) for accurate signature.

##### `__invert__(self)`

Using the ~ symbol as a prefix to a Pattern will reverse it.
>>> a = P[:4]
>>> print(a, ~a)
P[0, 1, 2, 3], P[3, 2, 1, 0]

##### `__iter__(self)`

Returns a generator object for this Pattern 

##### `__le__(self, other)`

Return self<=value.

##### `__len__(self)`

Returns the *expanded* length of the pattern such that if the pattern is laced, the
value is the length of the list multiplied by the lowest-common-multiple of the lengths
of nested patterns. e.g. the following are identical:
```
>>> print( len(P[0,1,2,[3,4]]) )
8
>>> print( len(P[0,1,2,3,0,1,2,4]) )
8
```

##### `__lt__(self, other)`

Return self<value.

##### `__ne__(self, other)`

Return self!=value.

##### `__or__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__repr__(self)`

Return repr(self).

##### `__ror__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__setslice__(self, i, j, item)`

Only works in Python 2 

##### `__str__(self)`

Return str(self).

##### `_update_delay(event, delay)`

Updates the delay value in the event dictionary 

##### `_update_sample(event, sample)`

Updates the sample value in the event dictionary 

##### `accum(self, *args)`

Returns a Pattern that is equivalent to list of sums of that
Pattern up to that index.

##### `all(self, func=<lambda>)`

Returns true if all of the patterns contents satisfies func(x) - default is nonzero 

##### `amen(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `arp(self, arp_pattern)`

Return a new Pattern with each item repeated len(arp_pattern) times
and incremented by arp_pattern. Useful for arpeggiating. e.g.
```
>>> P[0, 1, 2, 3].arp([0, 2])
P[0, 2, 1, 3, 2, 4, 3, 5]
```

##### `asGroup(self)`

Returns the Pattern as a PGroup 

##### `bubble(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `calculate_time(self, dur)`

Returns a PGroup of durations to use as the delay argument
when this is a sub-class of `PGroupPrime` 

##### `change_state(self)`

To be overridden by any PGroupPrime that changes state after access by a Player 

##### `choose(self)`

Returns one randomly selected item 

##### `convert_data(self, *args, **kwargs)`

Makes a true copy and converts the data to a given data type 

##### `copy(self)`

Returns a copy of the Pattern such that alterations to the
Pattern.data do not affect the original.

##### `count(self, item)`

Returns the number of occurrences of item in the Pattern

##### `deep_shuffle(self, n=1)`

Returns a new Pattern with shuffled contents and shuffles
any nested patterns. To shuffle the contents of nested patterns
with the rest of the Pattern's contents, use `true_shuffle`.

##### `duplicate(self, *args)`

Repeats this pattern n times but keep nested pattern values 

##### `eq(self, other)`

equals operator 

##### `every(self, n, method, *args, **kwargs)`

Returns the pattern looped n-1 times then appended with
the version returned when method is called on it. 

##### `flatten(self)`

Returns a nested PGroup as un-nested e.g.
::

    >>> P(0,(3,5)).flatten()
    P(0, 3, 5)

##### `get_behaviour(self)`

Returns a function that modulates a player event dictionary 

##### `get_iter(group)`

Recursively unpacks nested PGroup into an un-nested group

##### `get_methods(cls)`

Returns the methods associated with the `Pattern` class as a list 

##### `getitem(self, index)`

Called by __getitem__() 

##### `group(self)`

Returns the Pattern as a PGroup 

##### `has_behaviour(self)`

Returns True if this is a PGroupPrime or any elements are
instances of PGroupPrime or its sub-classes

##### `help(cls)`

Prints the Pattern class docstring to the console 

##### `invert(self)`

Inverts the values with the Pattern.
        

##### `items(self)`

Returns a generator object equivalent to using enumerate() 

##### `iter(self, *args)`

Repeats this pattern n times but doesn't take nested pattern into account for length

##### `layer(self, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `limit(self, *args)`

Returns a new Pattern generated by adding elements from
this Pattern to a new list and repeatedly calling
`func()` on this list until `func(l)` is greater than `value`
e.g.
```
>>> print( P[0, 1, 2, 3].limit(sum, 10) )
P[0, 1, 2, 3, 0, 1, 2]
```

##### `loop(self, *args)`

Repeats this pattern n times 

##### `make(self)`

This method automatically laces and groups the data 

##### `map(self, func)`

Returns a Pattern that calls `func` on each item 

##### `merge(self, value)`

Merge values into one PGroup 

##### `mirror(self)`

Reverses the pattern. Differs to `Pattern.reverse()` in that
all nested patters are also reversed. 

##### `ne(self, other)`

Not equals operator 

##### `norm(self)`

Returns the pattern with all values between 0 and 1 

##### `offlayer(self, dur, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `palindrome(self, *args)`

Returns the original pattern with mirrored version of itself appended.
a removes values from the middle of the pattern, if positive.
b removes values from the end of the pattern, should be negative.

e.g.

>>> P[:4].palindrome()
P[0, 1, 2, 3, 3, 2, 1, 0]
>>> P[:4].palindrome(1)
P[0, 1, 2, 3, 2, 1, 0]
>>> P[:4].palindrome(-1)
P[0, 1, 2, 3, 3, 2, 1]
>>> P[:4].palindrome(1,-1)
P[0, 1, 2, 3, 2, 1]

##### `pipe(self, pattern)`

Concatonates this patterns stream with another 

##### `pivot(self, *args)`

Mirrors and rotates the Pattern such that the item at index 'i'
is in the same place 

##### `replace(self, sub, repl)`

Replaces any occurrences of "sub" with "repl" 

##### `reverse(self)`

Reverses the contents of the Pattern. Nested patterns are
not reversed. To reverse the contents of nester patterns
use `Pattern.mirror()`

##### `sample(self, *args)`

Returns an n-length pattern from a sample

##### `shuffle(self, n=1)`

Returns a new Pattern with shuffled contents. Note: nested patterns
stay together. To shuffle the contents of nested patterns, use
`deep_shuffle` or `true_shuffle`.

##### `shufflets(self, n)`

Returns a Pattern of 'n' number of PGroups made from shuffled
versions of the original Pattern 

##### `sort(self)`

Used in place of sorted(pattern) to force type 

##### `splice(self, seq, *seqs)`

Takes at least list / Pattern and creates a new Pattern by
adding a value from each pattern in turn to the new pattern.
e.g.
```
>>> P[0,1,2,3].splice([4,5,6,7],[8,9])
P[0,4,8,1,5,9,2,6,8,3,7,9]
```

##### `startswith(self, prefix)`

Returns True if the first item in the Pattern is equal to prefix 

##### `stretch(self, *args)`

Stretches (repeats) the contents until len(Pattern) == size 

##### `string(self)`

Returns a PlayString in string format from the Patterns values 

##### `stutter(self, n=2)`

Returns a new Pattern with each item repeated by `n`. Use
a list of numbers for stutter different items by different
amount. e.g.
```
>>> P[0, 1, 2, 3].stutter([1,3])
P[0, 1, 1, 1, 2, 3, 3, 3]
```

##### `true_copy(self, new_data=None)`

Returns a copy of the Pattern such that items within the
Pattern hold the same state as the original.

##### `true_shuffle(self, n=1)`

Returns a new Pattern with completely shuffle contents such
that nested Patterns are shuffled within the larger Pattern

##### `undup(self)`

Removes any consecutive duplicate numbers from a Pattern 

##### `zip(self, other, dtype=None)`

Zips two patterns together. If one item is a tuple, it extends the tuple / PGroup
i.e. arrow_zip([(0,1),3], [2]) -> [(0,1,2),(3,2)]

##### `zipx(self, other)`

Returns a `Pattern` of `PGroups`, where each `PGroup` contains the i-th
element from each of the argument sequences. The length of the pattern
is the lowest common multiple of the lengths of the two joining patterns. 

---

### `PGroupOr(self, seq=[])`

Used to specify `sample` values, usually from within a play string using values 
between "bar" signs e.g. "|x2|" 

#### Methods

##### `__key(self)`

Returns a tuple of information to identify this Pattern 

##### `__bool__(self)`

Returns True if *any* value in the Pattern are greater than zero 

##### `__eq__(self, other)`

Return self==value.

##### `__ge__(self, other)`

Return self>=value.

##### `__getitem__(self, key)`

Overrides the Pattern.__getitem__ to allow indexing
by TimeVar and PlayerKey instances. 

##### `__gt__(self, other)`

Return self>value.

##### `__hash__(self)`

Return hash(self).

##### `__init__(self, seq=[])`

Initialize self.  See help(type(self)) for accurate signature.

##### `__invert__(self)`

Using the ~ symbol as a prefix to a Pattern will reverse it.
>>> a = P[:4]
>>> print(a, ~a)
P[0, 1, 2, 3], P[3, 2, 1, 0]

##### `__iter__(self)`

Returns a generator object for this Pattern 

##### `__le__(self, other)`

Return self<=value.

##### `__len__(self)`

Returns the *expanded* length of the pattern such that if the pattern is laced, the
value is the length of the list multiplied by the lowest-common-multiple of the lengths
of nested patterns. e.g. the following are identical:
```
>>> print( len(P[0,1,2,[3,4]]) )
8
>>> print( len(P[0,1,2,3,0,1,2,4]) )
8
```

##### `__lt__(self, other)`

Return self<value.

##### `__ne__(self, other)`

Return self!=value.

##### `__or__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__repr__(self)`

Return repr(self).

##### `__ror__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__setslice__(self, i, j, item)`

Only works in Python 2 

##### `__str__(self)`

Return str(self).

##### `_update_delay(event, delay)`

Updates the delay value in the event dictionary 

##### `_update_sample(event, sample)`

Updates the sample value in the event dictionary 

##### `accum(self, *args)`

Returns a Pattern that is equivalent to list of sums of that
Pattern up to that index.

##### `all(self, func=<lambda>)`

Returns true if all of the patterns contents satisfies func(x) - default is nonzero 

##### `amen(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `arp(self, arp_pattern)`

Return a new Pattern with each item repeated len(arp_pattern) times
and incremented by arp_pattern. Useful for arpeggiating. e.g.
```
>>> P[0, 1, 2, 3].arp([0, 2])
P[0, 2, 1, 3, 2, 4, 3, 5]
```

##### `asGroup(self)`

Returns the Pattern as a PGroup 

##### `bubble(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `calculate_time(self, *args, **kwargs)`

Return a single value, as its always "length" 1 

##### `change_state(self)`

To be overridden by any PGroupPrime that changes state after access by a Player 

##### `choose(self)`

Returns one randomly selected item 

##### `convert_data(self, *args, **kwargs)`

Makes a true copy and converts the data to a given data type 

##### `copy(self)`

Returns a copy of the Pattern such that alterations to the
Pattern.data do not affect the original.

##### `count(self, item)`

Returns the number of occurrences of item in the Pattern

##### `deep_shuffle(self, n=1)`

Returns a new Pattern with shuffled contents and shuffles
any nested patterns. To shuffle the contents of nested patterns
with the rest of the Pattern's contents, use `true_shuffle`.

##### `duplicate(self, *args)`

Repeats this pattern n times but keep nested pattern values 

##### `eq(self, other)`

equals operator 

##### `every(self, n, method, *args, **kwargs)`

Returns the pattern looped n-1 times then appended with
the version returned when method is called on it. 

##### `flatten(self)`

Returns a nested PGroup as un-nested e.g.
::

    >>> P(0,(3,5)).flatten()
    P(0, 3, 5)

##### `get_behaviour(self)`

Returns a function that changes a player event dictionary 

##### `get_methods(cls)`

Returns the methods associated with the `Pattern` class as a list 

##### `getitem(self, key, get_generator=False)`

Called by __getitem__() 

##### `group(self)`

Returns the Pattern as a PGroup 

##### `has_behaviour(self)`

Returns True if this is a PGroupPrime or any elements are
instances of PGroupPrime or its sub-classes

##### `help(cls)`

Prints the Pattern class docstring to the console 

##### `invert(self)`

Inverts the values with the Pattern.
        

##### `items(self)`

Returns a generator object equivalent to using enumerate() 

##### `iter(self, *args)`

Repeats this pattern n times but doesn't take nested pattern into account for length

##### `layer(self, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `limit(self, *args)`

Returns a new Pattern generated by adding elements from
this Pattern to a new list and repeatedly calling
`func()` on this list until `func(l)` is greater than `value`
e.g.
```
>>> print( P[0, 1, 2, 3].limit(sum, 10) )
P[0, 1, 2, 3, 0, 1, 2]
```

##### `loop(self, *args)`

Repeats this pattern n times 

##### `make(self)`

This method automatically laces and groups the data 

##### `map(self, func)`

Returns a Pattern that calls `func` on each item 

##### `merge(self, value)`

Merge values into one PGroup 

##### `mirror(self)`

Reverses the pattern. Differs to `Pattern.reverse()` in that
all nested patters are also reversed. 

##### `ne(self, other)`

Not equals operator 

##### `norm(self)`

Returns the pattern with all values between 0 and 1 

##### `offlayer(self, dur, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `palindrome(self, *args)`

Returns the original pattern with mirrored version of itself appended.
a removes values from the middle of the pattern, if positive.
b removes values from the end of the pattern, should be negative.

e.g.

>>> P[:4].palindrome()
P[0, 1, 2, 3, 3, 2, 1, 0]
>>> P[:4].palindrome(1)
P[0, 1, 2, 3, 2, 1, 0]
>>> P[:4].palindrome(-1)
P[0, 1, 2, 3, 3, 2, 1]
>>> P[:4].palindrome(1,-1)
P[0, 1, 2, 3, 2, 1]

##### `pipe(self, pattern)`

Concatonates this patterns stream with another 

##### `pivot(self, *args)`

Mirrors and rotates the Pattern such that the item at index 'i'
is in the same place 

##### `replace(self, sub, repl)`

Replaces any occurrences of "sub" with "repl" 

##### `reverse(self)`

Reverses the contents of the Pattern. Nested patterns are
not reversed. To reverse the contents of nester patterns
use `Pattern.mirror()`

##### `sample(self, *args)`

Returns an n-length pattern from a sample

##### `shuffle(self, n=1)`

Returns a new Pattern with shuffled contents. Note: nested patterns
stay together. To shuffle the contents of nested patterns, use
`deep_shuffle` or `true_shuffle`.

##### `shufflets(self, n)`

Returns a Pattern of 'n' number of PGroups made from shuffled
versions of the original Pattern 

##### `sort(self)`

Used in place of sorted(pattern) to force type 

##### `splice(self, seq, *seqs)`

Takes at least list / Pattern and creates a new Pattern by
adding a value from each pattern in turn to the new pattern.
e.g.
```
>>> P[0,1,2,3].splice([4,5,6,7],[8,9])
P[0,4,8,1,5,9,2,6,8,3,7,9]
```

##### `startswith(self, prefix)`

Returns True if the first item in the Pattern is equal to prefix 

##### `stretch(self, *args)`

Stretches (repeats) the contents until len(Pattern) == size 

##### `string(self)`

Returns a PlayString in string format from the Patterns values 

##### `stutter(self, n=2)`

Returns a new Pattern with each item repeated by `n`. Use
a list of numbers for stutter different items by different
amount. e.g.
```
>>> P[0, 1, 2, 3].stutter([1,3])
P[0, 1, 1, 1, 2, 3, 3, 3]
```

##### `true_copy(self, new_data=None)`

Returns a copy of the Pattern such that items within the
Pattern hold the same state as the original.

##### `true_shuffle(self, n=1)`

Returns a new Pattern with completely shuffle contents such
that nested Patterns are shuffled within the larger Pattern

##### `undup(self)`

Removes any consecutive duplicate numbers from a Pattern 

##### `zip(self, other, dtype=None)`

Zips two patterns together. If one item is a tuple, it extends the tuple / PGroup
i.e. arrow_zip([(0,1),3], [2]) -> [(0,1,2),(3,2)]

##### `zipx(self, other)`

Returns a `Pattern` of `PGroups`, where each `PGroup` contains the i-th
element from each of the argument sequences. The length of the pattern
is the lowest common multiple of the lengths of the two joining patterns. 

---

### `PGroupXor(self, seq=[])`

The delay of this PGroup is specified by the last value (not included in the data) 

#### Methods

##### `__key(self)`

Returns a tuple of information to identify this Pattern 

##### `__bool__(self)`

Returns True if *any* value in the Pattern are greater than zero 

##### `__eq__(self, other)`

Return self==value.

##### `__ge__(self, other)`

Return self>=value.

##### `__getitem__(self, key)`

Overrides the Pattern.__getitem__ to allow indexing
by TimeVar and PlayerKey instances. 

##### `__gt__(self, other)`

Return self>value.

##### `__hash__(self)`

Return hash(self).

##### `__init__(self, seq=[])`

Initialize self.  See help(type(self)) for accurate signature.

##### `__invert__(self)`

Using the ~ symbol as a prefix to a Pattern will reverse it.
>>> a = P[:4]
>>> print(a, ~a)
P[0, 1, 2, 3], P[3, 2, 1, 0]

##### `__iter__(self)`

Returns a generator object for this Pattern 

##### `__le__(self, other)`

Return self<=value.

##### `__len__(self)`

Returns the *expanded* length of the pattern such that if the pattern is laced, the
value is the length of the list multiplied by the lowest-common-multiple of the lengths
of nested patterns. e.g. the following are identical:
```
>>> print( len(P[0,1,2,[3,4]]) )
8
>>> print( len(P[0,1,2,3,0,1,2,4]) )
8
```

##### `__lt__(self, other)`

Return self<value.

##### `__ne__(self, other)`

Return self!=value.

##### `__or__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__repr__(self)`

Return repr(self).

##### `__ror__(self, other)`

Use the '|' symbol to 'pipe' Patterns into on another 

##### `__setslice__(self, i, j, item)`

Only works in Python 2 

##### `__str__(self)`

Return str(self).

##### `_update_delay(event, delay)`

Updates the delay value in the event dictionary 

##### `_update_sample(event, sample)`

Updates the sample value in the event dictionary 

##### `accum(self, *args)`

Returns a Pattern that is equivalent to list of sums of that
Pattern up to that index.

##### `all(self, func=<lambda>)`

Returns true if all of the patterns contents satisfies func(x) - default is nonzero 

##### `amen(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `arp(self, arp_pattern)`

Return a new Pattern with each item repeated len(arp_pattern) times
and incremented by arp_pattern. Useful for arpeggiating. e.g.
```
>>> P[0, 1, 2, 3].arp([0, 2])
P[0, 2, 1, 3, 2, 4, 3, 5]
```

##### `asGroup(self)`

Returns the Pattern as a PGroup 

##### `bubble(self, size=2)`

Merges and laces the first and last two items such that a
drum pattern "x-o-" would become "(x[xo])-o([-o]-)" 

##### `calculate_time(self, dur)`

Returns a PGroup of durations to use as the delay argument
when this is a sub-class of `PGroupPrime` 

##### `change_state(self)`

To be overridden by any PGroupPrime that changes state after access by a Player 

##### `choose(self)`

Returns one randomly selected item 

##### `convert_data(self, *args, **kwargs)`

Makes a true copy and converts the data to a given data type 

##### `copy(self)`

Returns a copy of the Pattern such that alterations to the
Pattern.data do not affect the original.

##### `count(self, item)`

Returns the number of occurrences of item in the Pattern

##### `deep_shuffle(self, n=1)`

Returns a new Pattern with shuffled contents and shuffles
any nested patterns. To shuffle the contents of nested patterns
with the rest of the Pattern's contents, use `true_shuffle`.

##### `duplicate(self, *args)`

Repeats this pattern n times but keep nested pattern values 

##### `eq(self, other)`

equals operator 

##### `every(self, n, method, *args, **kwargs)`

Returns the pattern looped n-1 times then appended with
the version returned when method is called on it. 

##### `flatten(self)`

Returns a nested PGroup as un-nested e.g.
::

    >>> P(0,(3,5)).flatten()
    P(0, 3, 5)

##### `get_behaviour(self)`

Returns a function that changes a player event dictionary 

##### `get_methods(cls)`

Returns the methods associated with the `Pattern` class as a list 

##### `getitem(self, key, get_generator=False)`

Called by __getitem__() 

##### `group(self)`

Returns the Pattern as a PGroup 

##### `has_behaviour(self)`

Returns True if this is a PGroupPrime or any elements are
instances of PGroupPrime or its sub-classes

##### `help(cls)`

Prints the Pattern class docstring to the console 

##### `invert(self)`

Inverts the values with the Pattern.
        

##### `items(self)`

Returns a generator object equivalent to using enumerate() 

##### `iter(self, *args)`

Repeats this pattern n times but doesn't take nested pattern into account for length

##### `layer(self, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `limit(self, *args)`

Returns a new Pattern generated by adding elements from
this Pattern to a new list and repeatedly calling
`func()` on this list until `func(l)` is greater than `value`
e.g.
```
>>> print( P[0, 1, 2, 3].limit(sum, 10) )
P[0, 1, 2, 3, 0, 1, 2]
```

##### `loop(self, *args)`

Repeats this pattern n times 

##### `make(self)`

This method automatically laces and groups the data 

##### `map(self, func)`

Returns a Pattern that calls `func` on each item 

##### `merge(self, value)`

Merge values into one PGroup 

##### `mirror(self)`

Reverses the pattern. Differs to `Pattern.reverse()` in that
all nested patters are also reversed. 

##### `ne(self, other)`

Not equals operator 

##### `norm(self)`

Returns the pattern with all values between 0 and 1 

##### `offlayer(self, dur, method, *args, **kwargs)`

Zips a pattern with a modified version of itself. Method argument
can be a function that takes this pattern as its first argument,
or the name of a Pattern method as a string. 

##### `palindrome(self, *args)`

Returns the original pattern with mirrored version of itself appended.
a removes values from the middle of the pattern, if positive.
b removes values from the end of the pattern, should be negative.

e.g.

>>> P[:4].palindrome()
P[0, 1, 2, 3, 3, 2, 1, 0]
>>> P[:4].palindrome(1)
P[0, 1, 2, 3, 2, 1, 0]
>>> P[:4].palindrome(-1)
P[0, 1, 2, 3, 3, 2, 1]
>>> P[:4].palindrome(1,-1)
P[0, 1, 2, 3, 2, 1]

##### `pipe(self, pattern)`

Concatonates this patterns stream with another 

##### `pivot(self, *args)`

Mirrors and rotates the Pattern such that the item at index 'i'
is in the same place 

##### `replace(self, sub, repl)`

Replaces any occurrences of "sub" with "repl" 

##### `reverse(self)`

Reverses the contents of the Pattern. Nested patterns are
not reversed. To reverse the contents of nester patterns
use `Pattern.mirror()`

##### `sample(self, *args)`

Returns an n-length pattern from a sample

##### `shuffle(self, n=1)`

Returns a new Pattern with shuffled contents. Note: nested patterns
stay together. To shuffle the contents of nested patterns, use
`deep_shuffle` or `true_shuffle`.

##### `shufflets(self, n)`

Returns a Pattern of 'n' number of PGroups made from shuffled
versions of the original Pattern 

##### `sort(self)`

Used in place of sorted(pattern) to force type 

##### `splice(self, seq, *seqs)`

Takes at least list / Pattern and creates a new Pattern by
adding a value from each pattern in turn to the new pattern.
e.g.
```
>>> P[0,1,2,3].splice([4,5,6,7],[8,9])
P[0,4,8,1,5,9,2,6,8,3,7,9]
```

##### `startswith(self, prefix)`

Returns True if the first item in the Pattern is equal to prefix 

##### `stretch(self, *args)`

Stretches (repeats) the contents until len(Pattern) == size 

##### `string(self)`

Returns a PlayString in string format from the Patterns values 

##### `stutter(self, n=2)`

Returns a new Pattern with each item repeated by `n`. Use
a list of numbers for stutter different items by different
amount. e.g.
```
>>> P[0, 1, 2, 3].stutter([1,3])
P[0, 1, 1, 1, 2, 3, 3, 3]
```

##### `true_copy(self, new_data=None)`

Returns a copy of the Pattern such that items within the
Pattern hold the same state as the original.

##### `true_shuffle(self, n=1)`

Returns a new Pattern with completely shuffle contents such
that nested Patterns are shuffled within the larger Pattern

##### `undup(self)`

Removes any consecutive duplicate numbers from a Pattern 

##### `zip(self, other, dtype=None)`

Zips two patterns together. If one item is a tuple, it extends the tuple / PGroup
i.e. arrow_zip([(0,1),3], [2]) -> [(0,1,2),(3,2)]

##### `zipx(self, other)`

Returns a `Pattern` of `PGroups`, where each `PGroup` contains the i-th
element from each of the argument sequences. The length of the pattern
is the lowest common multiple of the lengths of the two joining patterns. 

---

## Functions

## Data

