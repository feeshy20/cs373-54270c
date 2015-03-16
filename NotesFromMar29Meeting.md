# Introduction #

Add your content here.


# Details #

Admin Initialize Semester Page:
  * Dropdown box w/ Spring, Summer, Fall
  * Input box for year (validate as four digit number)
  * Validate that this semester doesn't exist
  * Upon successful validation, redirect to add/edit class page with current semester selected

Applicants:
  * Need to know more of the required functionality, specifically about application period window **ask on blackboard**

Instructors:
  * Same as Applicants **ask on blackboard**

Admin asks for a match:
  * Give bogus output on SuggestedAssignments.py **clarify "fake the match"**
  * Set up those same matches in database (maybe)

Datastore stuff:
  * Faculty
    * Instructor ID: Integer
    * Instructor Name: String
    * Instructor Password: String

  * Classes
    * Unique ID generated internally: Integer
    * Course Designation: String
    * Instructor ID: Integer
    * Expected Enrollment: Integer
    * Number of TA's needed: Integer
    * Number of TA's assigned: Integer(default to zero)
    * Native English Speaker Preferred: Boolean
    * Preferred Students: ListOfIntegers (key into Student table)
    * Non-preferred Students: ListOfIntegers (key into Student table)
    * Area of Specialization: ListOfStrings
      * potentially this could be a list of ints that keys into a Specializations table

  * Semesters
    * Semester: String
    * Unique Id of class as Primary Key into Classes table **could be actual Unique ID from UT, or not** : Integer

  * TAs
    * Unique ID generated internally: Integer
    * Phone Number: PhoneNumber type
    * Email: String (email type?)
    * Major: String
    * PhD: Boolean
    * UsCitizen: Boolean
    * EnglishSpeaker: Boolean
    * PreviousCourses: ListOfStrings
    * Admission Date: DateTime.DateTime
    * Supervising Professor: Integer or String **(needs clarification)**
    * ProgrammingLanguages: ListOfStrings
    * Area of Specialization: ListOfStrings
      * potentially this could be a list of ints that keys into a Specializations table
    * Courses qualified to teach: ListOfStrings