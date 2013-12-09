Version: 0.0.1 completely speculative

INTRODUCTION

Throughout this document, we will use the following conventions to indicate our special characters:
- [RS] for ASCII character 30 (0x1E), Record Separator
- [US] for ASCII character 31 (0x1F), Unit Separator

The "Unit and Record Separated Values" (.ursv) format is a simple delimited text file format which
intends to serve many of the same needs as the related Comma Separated Values (csv) format. This
specification is intended to clarify some issues related to practical uses of the ASCII Unit ([US])
and Record ([RS]) separator characters as delimiters, in the hopes that their use - as actual
delimiters - becomes more widely recognized. The specification attaches a related name and file
extension to the format, which can be used to disambiguate it format from the more-generic (and less
concrete) terms "Delimiter Separated Values" (of which this is a subset), "Comma Separated Values",
or "ASCII Delimited Text".

PURPOSE AND NEED

While the world probably doesn't need yet another file and data interchange format, this
specification aims to cement some of the best practices around creating delimited text files into
a named entity, so that users of the format can rest assured it will be easy to share and process.
While there are other ways to delimit text, we believe the ASCII Unit and Record separator
characters are the best tools for this job - and indeed, they were created just for such purpose.
And while other modern data interchange formats - XML, JSON, YAML - meet the need for data
interchange just file, nothing beats the simplicity, speed, and utility of a delimited text file -
*unless* the format is littered with problems and incorrectness which make it nearly impossible
to handle properly.

Comparison with CSV

Why do we need Unit and Record Separated Values when we already have CSV's?

Rather than being a single "format", CSV (which can be loosely interpreted as "Comma Separated
Values") is cumbersome and inadequate in many ways. The noble goal of writing simply-structued data
(in the form of fields and records) into a text file should not be so fraught with concerns such as
*which* delimiter to use despite the format's entrenched name, how to account for delimiters
embedded within the data, how to enclose the data (essentially lengthening our delimiters) when
the delimiters need to be transmitted within data values, and so on. We can do better.

Frankly, the choice of the ASCII comma (",") as a delimiter was a poor one, since it is so common
in the data trying to be interchanged with this format. This makes delimiter collisions nearly
inevetable, and attempting to combat this with quoting and escape characters quickly devloves into
an inane mess of code which is fraught with pitfalls and simply shouldn't need to exist. While there
are many good CSV readers and writers in many languages, it's all too easy to dump data to disk
without using one of them - and create a horrendous mess of text in the process.

Luckily, the creators of the ASCII encoding recognized this, and reserved some characters for us
*just* to make life easier in this arena. Like good programmers, we ignored them completely.

We also recognize that simply joining fields with unit separators, and rows with record separators,
and then writing to a text file, has a few drawbacks that have likely prevented their use in
practice. This format aims to solve those few problems simply and concisely to make their use
more acceptable in the real world.

Comparison with [US].join(fields) and [RS].join(rows)

- We like to scan our data in a text editor to "make sure it's correct" (lol)
- Text editors can't display these
- Allow some extra characters to make the format palatable to users
- Require some extra characters to make the format palatable to existing file reading software

SPECIFICATION

## TODO: Here are the main points I want to hit here:

- There will be no delimiter collisions allowed with this format.
- There will be no situations which required quoting with this format.
- There will be no situations which require escaping with this format.
- If your file has delimiter collisions, it may not be called "Unit and Record Separated Values",
and please do not save it with the .ursv extension :)
- Record separators *may* be combined with system line endings to promote readability in standard
text editors (although we wish text editors would display record separators on new lines, or
provide this option, there are many in use which never will, thus the concession)
- Fields *may* be quoted to promote readability in standard text editors (although it is *not*
necessary to prevent delimiter collisions, and simply makes lines start with ", makes middle
delimiters 3 characters ("[US]") instead of one, and makes the ending delimiter "[RS]\n instead of just
[RS]\n)

What This Is Not

- Done.
- The Unit and Record Separated Values format is *not* designed to transmit binary data, or raw data
which may or does have Unit and Record Separators themselves in the data. Such data may be
written using this specification, but will need to be encoded by the generating application (and
decoded by the receiving application) such that it will not produce a delimiter collision when
written, in order to be in accordance with the spec.

ACKNOWLEDGEMENTS

There will be many.
