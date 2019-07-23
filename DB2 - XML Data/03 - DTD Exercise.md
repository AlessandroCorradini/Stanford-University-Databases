# DTD Exercise

Instructions: For each question, you are to write a DTD that validates against the corresponding XML data set. Our back-end will validate the sample data with your DTD and display the result. When you're satisfied with your solution for a given problem, click the "Submit" button to check your answer. 

You may perform these exercises as many times as you like, so we strongly encourage you to keep working with them until you complete the exercises with full credit.

## Q1

In this question, you are to create a DTD for a small XML data set drawn from the Stanford course catalog. There are multiple departments, each with a department chair, some courses, and professors and/or lecturers who teach courses. The XML data is here. 

Write a DTD for the XML data set. 

Important: Do not include <!DOCTYPE Course_Catalog [...]> in your DTD. Your DTD should start with <!ELEMENT Course_Catalog (Department*)>.

```
<!ELEMENT Course_Catalog (Department)*>
<!ELEMENT Department (Title, Chair, Course*)>
<!ATTLIST Department Code CDATA #REQUIRED>

<!ELEMENT Title (#PCDATA)>
<!ELEMENT Chair (Professor)>
<!ELEMENT Professor (First_Name, Middle_Initial?, Last_Name)>
<!ELEMENT First_Name (#PCDATA)>
<!ELEMENT Middle_Initial (#PCDATA)>
<!ELEMENT Last_Name (#PCDATA)>

<!ELEMENT Course (Title, Description?, Instructors, Prerequisites?)>
<!ATTLIST Course Number CDATA #REQUIRED Enrollment CDATA #IMPLIED>
<!ELEMENT Description (#PCDATA)>
<!ELEMENT Instructors (Professor | Lecturer)*>
<!ELEMENT Lecturer (First_Name, Middle_Initial?, Last_Name)>
<!ELEMENT Prerequisites (Prereq+)>
<!ELEMENT Prereq (#PCDATA)>
```

## Q2

In this question, you are to create a DTD for a different version of the data set drawn from the Stanford course catalog. This version encodes the data using ID and IDREF(S) attributes. The XML data is here. 

Write a DTD for the XML data set. 

Hint: You may want to use your DTD from the previous question as a starting point, since the structure is similar. 

Important: Do not include <!DOCTYPE Course_Catalog [...]> in your DTD. Your DTD should start with <!ELEMENT Course_Catalog (Department*)>.

```
<!ELEMENT Course_Catalog (Department)*>
<!ATTLIST Department Code ID #REQUIRED Chair IDREF #REQUIRED>
<!ELEMENT Department (Title, Course*, (Professor|Lecturer)*)>
<!ATTLIST Professor InstrID ID #REQUIRED>
<!ATTLIST Lecturer InstrID ID #REQUIRED>
<!ELEMENT Course (Title, Description?)>
<!ATTLIST Course Number ID #REQUIRED Prerequisites CDATA #IMPLIED Instructors CDATA #REQUIRED Enrollment CDATA #IMPLIED>
<!ELEMENT Title (#PCDATA)>
<!ELEMENT Description (#PCDATA|Courseref)*>
<!ELEMENT Courseref (#PCDATA)>
<!ATTLIST Courseref Number IDREF #REQUIRED>
<!ELEMENT Professor (First_Name, Middle_Initial?, Last_Name)>
<!ELEMENT Lecturer (First_Name, Middle_Initial?, Last_Name)>
<!ELEMENT First_Name (#PCDATA)>
<!ELEMENT Middle_Initial (#PCDATA)>
<!ELEMENT Last_Name (#PCDATA)>
```


## Q3

In this question, you are to create a DTD for a small XML data set about world countries. This data is adapted from the Mondial 3.0 database as hosted by the University of Washington, and was originally compiled by the Georg-August University of Goettingen Institute for Informatics. Each country has a name, population, and area (in sq. km). Some countries also list languages (with percentages of the population that speaks each language) and/or cities (with names and populations). The XML data is here.

Write a DTD for the XML data set.

Important: Do not include <!DOCTYPE countries [...]> in your DTD. Your DTD should start with <!ELEMENT countries (country*)>.

```
<!ELEMENT countries (country)*>
<!ELEMENT country ((city*|language*)?)*>
<!ELEMENT city (name, population)>
<!ATTLIST country name CDATA #REQUIRED population CDATA #REQUIRED area CDATA #REQUIRED>
<!ATTLIST language percentage CDATA #IMPLIED>
<!ELEMENT name (#PCDATA)>
<!ELEMENT population (#PCDATA)>
<!ELEMENT language (#PCDATA)>
```
