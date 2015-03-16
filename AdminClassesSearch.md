# Introduction #

The Search subpage for AdminClasses will search the database of courses using the fields listed below.
  * An entry for all fields is not required for a valid search.

# URL #

local project: http://localhost:8080/admin/classes/search

live release: http://54270c.appspot.com/admin/classes/search

# Details #
None of the fields are required.  Leaving a field alone is a "no preference."  Thus, a submission with no preferences returns all applicants in the history of the datastore.

This form has criteria fields:

  1. Semester preference: Dropdown box (default value is all semesters).
    * Returns classes for a specified semester.
  1. Filled or Unfilled classes:  Dropdown box (default value is Both).
    * Returns only that have either been assigned the appropriate number of TAs or those that still need to be assigned its allotment.
  1. Native English speaker preference:  Checkbox
    * If checked, the search returns only classes that require native English speakers.
  1. Instructor preference:  Dropdown box.
    * Returns only classes taught by the specified instructor.
  1. Specialization preference:  Select field.
    * Returns only classes that require the selected specialization.
  1. TA preference: Select field.
    * Returns only classes that have been assigned the specified TA
  1. Unique Number search: Textbox field.
    * Returns the class that has the unique number entered, if any.  The unique number must be a valid 5-digit integer.

These fields can be combined in any way to filter results.

# Implementation #

The search works by building a dictionary where the key-value pairs consist of the datastore (google assigned) key for each ClassEntry, and a boolean value. Each field is tested for input. If input is present, a loop through all ClassEntrys to test for the appropriate property is performed. An example:

```
        if self.formFields[1].input != "" :
            for class_key in resultsDict.keys() :
                x = db.get(class_key)
                if self.formFields[1].input == "Filled" and x.numAssignedTAs != x.numNeededTAs :
                    resultsDict[class_key] = False
                elif self.formFields[1].input == "Unfilled" and x.numAssignedTAs == x.numNeededTAs :  
                    resultsDict[class_key] = False
```

This code decides whether a ClassEntry has been assigned its allotment of TAs (filled), or not (unfilled).  When results are returned, only those whose value in the key-value pair remains True are displayed.