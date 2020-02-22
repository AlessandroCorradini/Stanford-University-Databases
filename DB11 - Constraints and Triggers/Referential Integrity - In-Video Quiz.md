# Referential Integrity - In-Video Quiz

## Q1

Consider two tables Dorm(name,address), Student(name,dormName,roommateName). Suppose some students live in single rooms (roommateName is NULL) and no dorms are empty. Which of the following referential integrity constraints does NOT hold?

- Student.dormName to Dorm.name
- Dorm.name to Student.dormName
- **Student.name to Student.roommateName**
- Student.roommateName to Student.name

## Q2

Consider tables Dorm(name,address) and Student(name,dormName,roommateName) with referential integrity constraints: (1) Student.dormName to Dorm.name; (2) Dorm.name to Student.dormName; (3) Student.roommateName to Student.name. Which of the following modifications can NOT cause a referential integrity violation?

- insertion into Student
- deletion from Student
- update Student.roommateName
- **All of them can cause violations**
