# Introduction #

A subpage of [Admin](http://code.google.com/p/cs373-54270c/wiki/Admin).

This form will allow the admin to edit the following permissions for the selected semester:
  1. Set to Current Semester
  1. Who is allowed into the system


# URL #
http://localhost:8080/admin/editsemesterpermissions

http://54270c.appspot.com/admin/editsemesterpermissions

# Details #

After selecting the desired semester to edit, the administrator will provide the following information:

  1. Set to Current Semester - valid input is:
    * one of "yes" or "no".  This is enforced by checking that the field input isn't an empty string.  Note: selecting "no" for this field will automatically lock out students and faculty for this semester.
  1. Who is allowed into the system - valid input is:
    * one of "Students", "Faculty", or "Neither".  This is enforced by checking that the field input isn't an empty string.  Note: only one user type (of Students and Faculty) can have access to the system at one time.