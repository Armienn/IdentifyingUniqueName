# Identifying Unique Name (IDUN)

(Draft)

This is a form of identification, meant to be universally unique, usable by everyone and somewhat easy to remember. It consists of 24-36 digits, and may be presented in three different manners:

- All numbers: `701119-900312-003053-761660`
- All words: `sacedu-xaoci-adatu-tedepa`
- Birthdate + words: `sacedu-900312-adatu-tedepa`

## Segments

These are the most common segments of an IDUN:

`cc`: Two control digits (the sum of the remaining pairwise digits, modulo 100). These are generated from the remaining digits by handling them in pairs as numbers between 0 and 99: sum these and take the modulus of 100.

`vv`: One or two version digits.

`nn`: Two digits for the issuing nation. There will be at least two lists of which number corresponds to which nation.

`ddddddddd`: 9 digits representing the birthdate. The first five are the Human Era year, then two for the month and two for the date.

`rrrrrrr`: Varying amounts of random digits.

## Versions

The current versions are as follows:

`cc0ddd-dddddd-rrrrrr-rrrrrr`: General purpose IDUNs. 6 or 12 additional random digits should be added by individuals creating their own IDUN. The short form is reserved for historical figures and for use by a few initial issuers.

`cc1ddd-dddddd-nnrrrr-rrrrrr`: Nationally issued IDUNs from the first list of nations. Nations may decide not to randomly generate the "random" digits, if they use other means to ensure uniqueness. Otherwise 6 or 12 additional random digits is generally recommendable.

`cc2ddd-dddddd-nnrrrr-rrrrrr`: Nationally issued IDUNs from the second list of nations. See above.

`cc3+`: Reserved

## Presentation

An IDUN may be presented as digits or as characters. The numbers can be converted to characters using the following scheme:

A number `n` between 0 and 99 is converted by finding `c = floor(n / 5)` and `v = n % 5`. A syllable is then constructed by taking first the character at index `c` in: `_bcdfghjklmnprstvwxz`, and then the character at index `v` in: `aeiou`. Thus from 19 we get `c = 3` and `v = 4`, which results in the syllable "du". The number 3 would result in "\_o", but "\_" can be safely be dropped, leaving "o".

The three suggested presentations of an IDUN: 

- All numbers (701119-900312-003053-761660)
- All words (sacedu-xaoci-adatu-tedepa)
- Birthdate + words (sacedu-900312-adatu-tedepa)
