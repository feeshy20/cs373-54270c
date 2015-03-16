# Preference Rank #

A class needs some way to give preference to one TA verses another when constructing its preference list and vice versa.  There will be three ranking levels for both, Rank 1 being the highest.  In a class's preference list, if two or more TA's have the same rank then their preference is decided by who is added into the preference list first. i.e. [taWithRank1a, taWithRank1b] taWithRank1a will be prefered over taWithRank1b since he/she came first in the list, even though they have the same rank.

## TA Ranks for Classes ##
  * Rank 1: TA has class in class history (its my assumption that if a student has a class in their history, then they are also qualified to teach it)
  * Rank 2: TA is qualified to teach but does not have class in class history
  * Rank 3: TA has never taught class nor is TA qualified to teach

## Class Ranks for TAs ##

Ranks 1a, 2a and 3a are only activated if the Class instance prefers a native english speaker.  Otherwise native and non-native speakers are both lumped into the normal ranks.

  * Rank 1: TA is preferred
  * Rank 1a: TA is preferred but is not native english speaker
  * Rank 2: TA is neither preferred nor unpreferred
  * Rank 2a: TA is neither preferred nor unpreferred and is not native english speaker
  * Rank 3: TA is not preferred
  * Rank 3a: TA is not preferred and is not a native english speaker

# Helper Classes #

There will be a Class object and a TA object, both which inherit from a base class SMP object:

## SMP Class ##
The SMP class will have the following member variables:
  * idNum : int = -1
    * int that the project 4 SMP algorithm will use
  * prefList : int = [.md](.md)
    * list of preferences, ordered by rank, containing their int idNum
  * key : key()
    * object to TA table for the TA or Class entry this object represents
  * rank1 : List of key()
    * all the key's to ClassEntry entrys that this TA or Class ranks as 1
  * rank2 : List of key()
    * all the key's to ClassEntry entrys that this TA or Class ranks as 2
  * rank3 : List of key()
    * all the key's to ClassEntry entrys that this TA or Class ranks as 3

## Class Class (gwahaha) ##
The Class Class will have the following member variables:
  * numSlots : int
    * number of open TA slots in current class, found from Table
  * prefersEnglish : boolean
    * indicates whether or not this class prefers native english speakers
  * rank1a : List of key()
    * all the key's to ClassEntry entries that this Class ranks as 1a. only initialized if prefersEnglish == True
  * rank2a : List of key()
    * all the key's to ClassEntry entries that this Class ranks as 2a. only initialized if prefersEnglish == True
  * rank3a : List of key()
    * all the key's to ClassEntry entries that this Class ranks as 3a. only initialized if prefersEnglish == True

## TA Class ##
The Class Class will have the following member variables:

# Main Algorithm #

The purpose of this algorithm is to be the middle man between our database and the SMP algorithm that was created for project 4.  The algorithm only understands integer represetations for the "men" and "women" (classes and TA's in our case), thus we will convert the Classes, TA's and their preferences to ints.

Its likely this algorithm will live in its own class.

## Global/Instance variables ##
The algorithm will require a few global variables to facilitate the id number representation of each TA and class.

  * taCounter : int = 1
    * to assist with the assigning of idNums to ta Entries
  * classCounter : int = 1
    * to assist with the assigning of idNums to class Entries
  * studentIds : dict( TAtable.key() : idNum ) (or list of ( key(), int) tuples)
    * a dictionary in which the ta key is the key and the idNum for that entry is the value
  * classIds : dict( ClassEntry.key() : idNum) (or list of ( key(), int) tuples)
    * a dictionary in which the ClassEntry key is the key and the idNum for that entry is the value
  * assignments : list of tuples of ints?
    * a list of the assignements given by the SMP algo, each assignment store as a tuple of 2 ints unless we come up with a better idea
  * unassignedClasses : list of Class objects
    * class objects that still need to be run through SMP
  * unassignedTAs : list of TA objects
    * TA objects that still need to be run through SMP

## Initialization of id dictionaries ##
The algorithm must first initialize the studentIds dict and classIds dict

  * For each entry in TA table:
    1. studentIds[ta.key()] = taCounter
    1. taCounter += 1
  * Ditto for classIds and classCounter

## Set up Class Preferences ##
This section of the algorithm will produce an integer preference list of each class entry class object.

For each class in the ClassEntry table:
  1. Initialize a Class object
  1. initialize idNum. can be found from classIds dict()
  1. initialize key. key() to class entry can be found from ClassEntry object
  1. initialize numSlots.  can be found in ClassEntry table.
  1. if prefersEnglish == False
    1. populate rank1 list.  this is the list of prefered students for the ClassEntry object, be sure to get the key object for that student.
    1. populate rank3 list.  list of nonprefered students
    1. populate rank2 list.  remaining students in TA table that don't exist in rank1 or rank3.
    1. populate prefList.
      1. for each member of rank1, append idNum (using studentIds dict)
      1. for each member of rank2, append idNum
      1. for each member of rank3, append idNum
  1. if prefersEnglish == True
    1. populate rank lists (including lists rank1a, 2a and 3a) accordingly.  See above for rules on each rank.
  1. add to unassignedClasses

## Set up TA Preferences ##
This section of the algorithm will produce an integer preference list of each ta entry ta object.

For each ta entry in the TA entry table:
  1. Initialize a TA object
  1. initialize idNum. can be found from studentIds dict()
  1. initialize key. key() to ta entry can be found from ta table object
  1. populate rank1 list.  list of history classes
  1. populate rank2 list.  list qualified classes that aren't also in history classes
  1. populate rank3 list.  remaining classes that arent in rank1 or rank2
  1. populate prefList.
    1. for each member of rank1, append idNum (using classIds dict)
    1. for each member of rank2, append idNum
    1. for each member of rank3, append idNum
  1. add to unassignedTAs

## SMP usage ##
So we need to call SMP multiple, see the "Multiple calls to SMP" section below.

After Setting up initial preferences...
Loop until unassignedTA's is empty:
  1. Run SMP using integer translations
  1. make a tempAssignments list (list of tuples of ints)
  1. for each TA in tempAssignments:
    1. remove from unassignedTAs
    1. for each Class in unassignedClasses
      1. remove TA from rank1/rank2/rank3 list and from prefList
  1. for each class in tempAssignments:
    1. if class exists in unassignedClasses:
      1. decrement numSlots by 1
      1. if numSlots == 0
        1. remove class from unassignedClasses
        1. for each TA in unassignedTA
          1. remove class from rank1/rank2/rank3 list and from prefList
  1. add all tempAssignments to assignments

# Important Differences from Project 4 #

## 1 to 1 relation ##

In project 4 there was a 1 to 1 relation between men and women (1 man for every woman and vice versa).  Keep in mind this is not the case for this project.

Ideally, I think each TA will only have 1 class but each class can have multiple TA's.  Running with that, the ta is the WOMAN and the class is the MAN.  Take a look at the SMP assignment [page](http://www.cs.utexas.edu/users/downing/projects/python/smp/) and just do a little word swapping.

## Multiple calls to SMP ##

Since each class can potentially have more than 1 TA we'll need to make multiple runs with the SMP algorithm.  Right now, swapping the words around it looks like this:
  1. identify a free Class
  1. identify the highest-ranked TA to whom it has not yet attempted to match with
  1. if the TA is currently matched, identify their current Class
  1. for a TA t and two classes c and c', decide which of c or c' is preferred by t

We can see that running through these steps one time potentially leaves us with left over TA's with no assignment if we have more TA's than classes.  Worse, it only gives each class 1 TA each.

Adam proposed the idea of running the algorithm again using only the left over TA's.  After running the algorithm, we should take the TA's which have not yet been assigned and the classes which still have open slots and run the algorithm again.
  * Each time the algorithm is "re-run" we will need to:
    1. Remove Assigned TA's
      * one run of the SMP algorithm will return a list of assignments, it will be easy to figure out which TA's are assigned
    1. Remove Classes which have no open slots
      * ditto on number 1
    1. Recompute prefLists for remaining classes and TA's
      * we can store the given assignments each time we run SMP in the assignements list given as a global/instance variable above

# New DB table #
> We'll need some sort of new table to store assignments.  The admin should be able to modify this table.

AssignmentEntry:
  * taKey : key into TA table
  * classKey : key into ClassEntry table

This should be fairly easy to populate using the assignments list from the main algorithm and the studentIds and classIds containers.  To get the assignments for a given class, we simply query this table where key() = the key for that class.