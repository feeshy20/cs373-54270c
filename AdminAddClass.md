# Introduction #

A subpage of [Admin](http://code.google.com/p/cs373-54270c/wiki/Admin).

This form will add a new class to the database, using the following fields:
  1. Semester
  1. Course Designation
  1. Instructor Name
  1. Unique Number
  1. Expected Enrollment
  1. Number of TAs Needed
  1. Number of TAs Assigned

# URL #

local project: http://localhost:8080/admin/system/addclass

live release: http://54270c.appspot.com/admin/system/addclass

# Details #

Administrator will provide the following information:

  1. Semester - valid input is:
    * one of the available semesters from the dropdown menu.  This is enforced by checking if the input from the field is not an empty string.  The menu is populated with all the semesters from the database.
  1. Course Designation - valid input is:
    * one of the available course designations from the dropdown menu.  This is enforced by checking if the input from the field is not an empty string.  The menu is populated with all the course designations from the database.
  1. Instructor Name - valid input is:
    * one of the available instructors from the dropdown menu.  This is enforced by checking if the input from the field is not an empty string.  The menu is populated with all the instructors from the database.
  1. Unique Number - valid input is:
    * exactly 5 digits (must not be the same as an existing unique number of a class)
  1. Expected Enrollment - valid input is:
    * 1 - 3 digits
  1. Number of TAs Needed
    * 1 or 2 digits
  1. Number of TAs Assigned
    * 1 or 2 digits