# Introduction #

The Search Applicants subpage for [Admin](http://code.google.com/p/cs373-54270c/wiki/Admin) will search the database of TA's using the fields listed below.
  * An entry for all fields is not required for a valid search.

# URL #

local project: http://localhost:8080/admin/searchapplicants

live release: http://54270c.appspot.com/admin/searchapplicants

# Details #

None of the fields are required.  Leaving a field alone is a "no preference."  Thus, a submission with no preferences returns all applicants in the history of the datastore.

This form has criteria fields:

  1. Semester preference: Dropdown box (default value is all semesters).
    * Returns applicants that applied for a specific semester. If left alone, applicants across all semesters are returned.
  1. Assigned or Unassigned applicants:  Dropdown box (default value is Both).
    * Returns only applicants who are assigned or unassigned, or both if left alone.
  1. Native English speaker preference:  Checkbox
    * If checked, the search returns only applicants who are native English speakers.
  1. U.S. Citizen preference:  Checkbox
    * If checked, the search returns only applicants who are U.S. Citizens.
  1. Supervising professor preference:  Dropdown box.
    * Returns only applicants whose supervising professor is selected.
  1. Specialization preference:  Multi-select field.
    * Returns only applicants who have listed ALL selected specializations.
  1. Assigned to specific courses: Multi-select field.
    * Returns only applicants who are assigned to the selected class
  1. Previously taught course preference: Multi-select field.
    * Returns only applicants who have taught a specified course
  1. Programming language preference: Multi-select field.
    * Returns only applicants who have listed ALL programming languages specified.

These fields can be combined in any way to filter results.

# Implementation #
The search works by building a dictionary where the keys for all applicants in the datastore are the keys, with boolean values for the values.  Then each field is tested for input.  If input is present, a loop through all applicants to test for the appropriate property is performed.  An example:

```
        if self.formFields[4].input != "" :
            for applicant_key in resultsDict.keys() :
                x = db.get(applicant_key)
                if x.supervisingProfessor != self.formFields[4].input :
                    resultsDict[applicant_key] = False
```

The above code finds applicants who do not list the specified instructor as a supervising professor.  It then sets that applicants value to False in the dictionary.  When results are returned, only those whose values in the dictionary are still True will be displayed.