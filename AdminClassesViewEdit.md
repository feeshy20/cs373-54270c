# Introduction #

A subpage of AdminClasses.

This page queries the database and lists all classes and each classes' data.  Each course name will have a link to an [Edit Class](http://code.google.com/p/cs373-54270c/wiki/AdminClassesEditClass) page, similar to the Add New class page.

# URL #

local project: http://localhost:8080/admin/classes/view

live release: http://54270c.appspot.com/admin/classes/view

# Details #

A table is displayed with all current classes in the database.  The columns are as follows (from left to right):
  * Course Designation
  * Instructor name
  * Expected Enrollment
  * TA's Assigned
  * TA's Needed

The course designation entry is a link to the [Edit Class](http://code.google.com/p/cs373-54270c/wiki/AdminClassesEditClass) for that class, created dynamically by AdminClassesEditClass.py.