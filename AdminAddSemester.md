# Introduction #

A subpage of [Admin](http://code.google.com/p/cs373-54270c/wiki/Admin).

This form will add a new semester to the database, using the following fields:
  1. Session (i.e. Fall, Spring, or Summer)
  1. Year

# URL #

local project: http://localhost:8080/admin/system/addsemester

live release: http://54270c.appspot.com/admin/system/addsemester

# Details #

Administrator will provide the following information:

  1. Session - valid input is:
    * one of "Summer", "Fall", or "Spring" selected.  This is enforced by ensuring that the value of the form field isn't an empty string.
  1. Year - valid input is:
    * exactly 4 digits