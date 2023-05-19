# DNDutils

This repository is a set of utilities, that make playing DnD a little easier. These utilities when taken together, will create all the spells (on the dnd wikidot) locally.

Furthermore, there are search tools to make it much easier to search for and preview any of the spells in DnD.

# Prerequisites

These must be installed on the system, before any of these utilities will work:

* fzf - fuzzy processor, preferably from https://github.com/junegunn/fzf
* pup - https://github.com/ericchiang/pup
* html2text - from your repository
* iconv - from your repository

# Usage

## Usage prerequisite and documentation

Before you can use most of these utilities, you must first create the local database.

```bash
$ createspells
```
This will create all the spells in the ~/Documents/dnd directory, unless you specify another directory in the environment variable "DND_DIRECTORY".

After it is finished you will have a directory structure like this:

* ${DND_DIRECTORY}/spells - which contains all the spells in text form
* ${DND_DIRECTORY}/spells/byclass - which contains each class (bard, druid, wizard etc.)

Under each class, there are directories which are [ 0 - n ], which denotes what levels are appropriate for the class. 

(Note not all classes will have a directory 0). Directory 0 is reserved as a Cantrip directory, if the class has one.
Ranger and Paladin do not have cantrips, hence no 0 directory.

So, for example, if you want to locate a spell under the druid class, level 2, you would look in the ${DND_DIRECTORY}/spells/byclass/druid/2/
directory.

You will also notice that under those byclass directories that each spell is a soft link to the actual spell located in the ~/Documents/dnd/spells directory.

This is to save disk space by not duplicating the text of the spell everywhere.

`dndpreview` is used to do a pretty print of a spell from its raw text form. This utility can be used on its own, but is used mainly for the preview part of the fzf utility.


## dndclass

The dndclass is used to find all spells for a particular class and maxlevel

usage: dndclass [ -l | classname maxlevel ]

`dndclass -l` -> will list all the available classes

`dndclass bard 2`   -> will display a list and preview

## dndfind

dndfind finds all spells that have the regexp in them.

usage: dndfind [ -l | classname maxlevel regexp ]

`dndfind -l` -> will list all the available classes which have the regexp in it

`dndfind druid 2 flam` -> will list all the availiable spells which have "flam" in them for the druid class up through level 2

## dndbonus

dndbonus is a quick way to find all spells that are bonus actions for the class and levels

usage: dndbonus [ -l | classname maxlevel ]

`dndbonus -l` -> will list all the available classes

`dndbonus druid 2` -> list all the bonus actions for all spells in the druid class up through level 2

# Final thoughts

I started out by using the wikidot website, on my cellphone. It was ok, but it was slow to use because of my cellphone coverage, and when I went back and forth between spells, or searching for spells, it was slow and cumbersome.
In addition to that, sometimes the internet was intermittent and wouldn't load at all, making me more frustrated.

This is why I decided to do all of this locally.

## making aliases to help you along the way

I am currently playing a druid of level 2, so after installing these dndutils on my system, and putting them in my PATH:

I created the following aliases, which I use, you can do similar:

* alias druidbonuses="dndbonus druid 2"
* alias druid="dndclass druid 2"
* alias dfind="dndfind druid 2"

The 3rd alias, dfind, requires a little more explanation here.

after sourcing in these aliases, to use the dfind alias you must supply the regexp. like so:

`dfind flam`

the above command will find all spells with 'flam' in them for the druid class levels 0-2

very handy.

Please enjoy.

