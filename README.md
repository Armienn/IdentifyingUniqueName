# Identifying Unique Name (IDUN)

(Draft)

This is a form of identification meant to be universally unique, usable by everyone and somewhat easy to remember. It consists of 36 digits, and may be textually represented in a few different manners:

- Number form: `000000-000000-000000-305300-181119-900312`
- Name form: `datua-docedu-xaoci`
- Mixed form: `datua-docedu-900312`

## Structure 

The most basic structure of an IDUN is `xxxxxx-xxxxxx-xxxxxx-xxxxxx-CCVxxx-xxxxxx`. `V` is the IDUN version, `CC` are the check digits, and the rest depend on the version.

The structure of the current versions are:

`V = 0`: `rrrrrr-rrrrrr-rrrrrr-rrrrrr-cc0ddd-dddddd` - General purpose IDUN.  
`V = 1`: `rrrrrr-rrrrrr-rrrrrr-rrrrnn-cc1ddd-dddddd` - First group of nationally issued IDUN.  
`V = 2`: `rrrrrr-rrrrrr-rrrrrr-rrrrnn-cc2ddd-dddddd` - Second group of nationally issued IDUN.  
`V = 3+`: Reserved for future uses.

## Segments

`rrrrrrr`: Varying amounts of usually random digits.  
`nn`: Two digits for the issuing nation. There will be at least two lists of which number corresponds to which nation.  
`cc`: Two check digits. These are calculated as the sum of the other digits (taken pairwise as numbers between 0 and 99) modulo 100.  
`ddddddddd`: 9 digits representing the birthdate. The first five are the Human Era year, then two for the month and two for the date.

## Versions

### General purpose IDUN

`rrrrrr-rrrrrr-rrrrrr-rrrrrr-cc0ddd-dddddd`

These are IDUNs for general use. Anyone may generate an IDUN of this version, by generating a random number for the `r`s.

The risk of duplicate IDUNs for a specific birthdate is one in a million, if a million of these are generated for that date. If half of the 24 random digits are set to zero, the risk is one in a million if a thousand are generated. Setting initial digits to zero makes the IDUN easier to remember, but with the trade-off of increased risk of duplicates.

A rule of thumb as to how many initial digits you may set to zero: are you the only one to use IDUNs (you're not)? Then three sections (18 digits) of zeroes. Do you know of only one organisation which uses IDUNs? Then two sections of zeroes (12 digits). Do you know of less than ten such organisations? Then one section of zeroes (6 digits). Otherwise no intentional initial zeroes.

### First and second group of nationally issued IDUN

`rrrrrr-rrrrrr-rrrrrr-rrrrnn-cc1ddd-dddddd` / `rrrrrr-rrrrrr-rrrrrr-rrrrnn-cc2ddd-dddddd`

These are IDUNs to be issued by nations. Version 1 and 2 each has a list of which `nn` numbers correspond to which nation.

It is up to each nation whether to generate the `r`s randomly, or to use some other scheme. In accordance with the study ["The Introduction and Use of Personal Identification Numbers: The Data Protection Issues"](https://rm.coe.int/16806845b3) commissioned by the Council of Europe, it is preferable to not encode any personal information in the number.

## Presentation

An IDUN may be presented in three standard representations:

### Number Form

This is simply the pure numbers, split into six parts by dashes:

`000000-000000-000000-305300-181119-900312`

### Name Form

For this representation, the digits are converted to [syllabic numerals](https://github.com/Armienn/SyllabicNumerals) via the scheme described in the conversion section below. Leading sections of zeroes are trimmed:

`datua-docedu-xaoci`

### Mixed Form

This is like the Name Form, except the final section is written as digits, as it is usually a date of birth:

`datua-docedu-900312`

## Decimal to Syllabic Numeral Conversion

The following is a short description of the how to generate syllabic numerals. More details can be found [here](https://github.com/Armienn/SyllabicNumerals).

A number `n` between 0 and 99 is converted by finding `c = floor(n / 5)` and `v = n % 5`. A syllable is then constructed by taking first the character at index `c` in: `_bcdfghjklmnprstvwxz`, and then the character at index `v` in: `aeiou`. Thus from 19 we get `c = 3` and `v = 4`, which results in the syllable "du". The number 3 would result in "\_o", but "\_" can be safely be dropped, leaving "o".

Some longer examples:
- 488352 > lovomi
- 00732 > abihi (alternatively bihi, in the same way that 00732 = 732)
- 49024178 > luiketo

## Redundant IDUNs

At times a person might be assigned different IDUNs by separate entities. When becoming aware of this, as a rule of thumb the IDUN which corresponds to the lowest number should be used going forward, and the other one discarded.

## Possible UUID Format

UUIDs consist of 128 bits, of which 6-8 bits are used for version information, and IDUNs happen to fit nicely in 120 bits. A UUID version containing an IDUN could technically be defined.

## Privacy and Other Considerations

This is a name. It is for identification, not authentification. (TODO)
