# Introduction #

Subpage of MainPage.

The main admin page contains links to subpages that implement the functionality listed below.
  * [Search Classes](http://code.google.com/p/cs373-54270c/wiki/AdminClassesSearch)
  * [Search Applicants](http://code.google.com/p/cs373-54270c/wiki/AdminSearchApplicants)
  * [Keyword Search](http://code.google.com/p/cs373-54270c/wiki/AdminKeywordSearch)
  * [Add a Semester](http://code.google.com/p/cs373-54270c/wiki/AdminAddSemester)
  * [Add a Course](http://code.google.com/p/cs373-54270c/wiki/AdminAddCourse)
  * [Add a Class](http://code.google.com/p/cs373-54270c/wiki/AdminAddClass)
  * [Add a Major](http://code.google.com/p/cs373-54270c/wiki/AdminSystemAddMajor)
  * [Add an Admin](http://code.google.com/p/cs373-54270c/wiki/AdminSystemAddUser)
  * [Add a Faculty Member](http://code.google.com/p/cs373-54270c/wiki/AdminSystemAddFaculty)
  * [Add a TA](http://code.google.com/p/cs373-54270c/wiki/AdminSystemAddTA)
  * [Add a Programming Language](http://code.google.com/p/cs373-54270c/wiki/AdminSystemAddProgrammingLanguage)
  * [Add an Area of Specialization](http://code.google.com/p/cs373-54270c/wiki/AdminSystemAddSpecialization)
  * [View Finalized Assignments](http://code.google.com/p/cs373-54270c/wiki/ViewFinalizedAssignments)
  * [Run SMP and finalize suggested Assignments](http://code.google.com/p/cs373-54270c/wiki/RunSMP)
  * [Finalize Suggested Assignments](http://code.google.com/p/cs373-54270c/wiki/FinalizeSuggestedAssignments)
  * [Override Suggested Assignments](http://code.google.com/p/cs373-54270c/wiki/OverrideAssignments)
  * [Manually create Assignments](http://code.google.com/p/cs373-54270c/wiki/ManuallyCreateAssignments)
  * [Edit Semester Permissions](http://code.google.com/p/cs373-54270c/wiki/AdminEditSemesterPermissions)

# URL #

local project: http://localhost:8080/admin

live release: http://54270c.appspot.com/

# Details #
Administrators will:

  1. Input, view, and edit the list of classes that need TAs. For each course, the administrators will input:
    1. the class number/name (e.g. cs302)
    1. the instructor's name
    1. the expected enrollment
    1. the number of TAs needed
    1. the number of TAs assigned.
  1. Make queries of the system, like:
    1. show me the Applicants who specify Networks as their area of specialization
    1. show me the Applicants, in rank order, who specify cs302 as a course they feel qualified to teach
    1. show me the Applicants, in rank order, who are native English speakers and have specified Operating Systems as their area of specialization
    1. show me the Applicants who have TA'ed cs352 previously
    1. show me the classes for which the estimated TA allotment is 2
    1. show me the classes that will be taught by Downing
    1. show me the classes that have not been assigned a TA
    1. show me the classes that John Doe is assigned to TA.
  1. Ask the system for suggested assignments via the SMP algorithm.
  1. View, edit the assignment of TAs to classes.