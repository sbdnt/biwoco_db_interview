# Academic Institution Database Design

## Building
name,
location,


## Department
name,
dean_id,
bulding_id,

## Room
name,
deparment_id,

## Major
id,
name,
department_id,


##  Syllabus
id,
name,
major_id,


## Semester
name
major_id


## Course
name, 
instructor_id,
credit_hours,
schedule,
deparment_id,
semester_id,
description,


## Subject
name,
courses_id,
room_id,
description,


## Attendance
id,
student_id,
subject_id,


## Assignment
id,
name,
subject_id,


## Quiz
id,
name,
course_id,
description,


## Exam
id,
name,
semester_id,
description,


## LearningOutcome
id,
name,
semester_id,
student_id,


## Professor
id,
name,
deparment_id,

## Lecturer
id,
name,
department_id,

## TeachingAssistant
id,
name,
lecturer_id,


## Students
id, 
name,
major_id,
address,
phone_number,

## Publications,
id,
title,
type,
publication_date,
author_id


## ResearchProject
id,
name,
major_id,


## Club
id,
name,
deparment_id,


## Library
id,
name,
location,


## Book
id,
name,
author,
major_id,


## Resource
id,
name,
type,
room_id,

## SupportServices
id,
name,
description,


# Queries,


```python
- List all students enrolled in a specific course, along with their grades.

SELECT Students.student_id, Students.student_name, Enrollments.grade
FROM Students
JOIN Enrollments ON Students.id = Enrollments.student_id
JOIN Courses ON Enrollments.course_id = Courses.id
WHERE Courses.course_name = 'Specific_Course_Name';

```


```python
- Find all publications authored by a particular professor in the last five years.

SELECT Publications.id, Publications.title, Publications.publication_date
FROM Publications
JOIN Professor_Publication ON Publications.publication_id = Professor_Publication.publication_id
JOIN Professors ON Professor_Publication.professor_id = Professors.professor_id
WHERE Professors.professor_name = 'Specific_Professor_Name' AND Publications.publication_date >= DATE_SUB(CURDATE(), INTERVAL 5 YEAR);

```


```python
- Calculate the average GPA of students in a specific major.

SELECT Student.id, Student.name, AVG(Enrollment.grade) AS AverageGPA
FROM Student
JOIN Enrollment ON Student.id = Enrollment.student_id
JOIN Course ON Enrollment.course_id = Course.id
JOIN Major ON Course.major_id = Major.id
WHERE Major.name = 'Computer Science'
GROUP BY Student.id;

```


```python
- Retrieve the schedule of courses offered by a department in a given semester.

SELECT Course.name, Courses.schedule
FROM Course
JOIN Department ON Course.department_id = Department.id
JOIN Semester ON Course.semester_id = Semester.id
WHERE Department.id = 'Department ID'
AND Semesters.id = 'Semester ID';

```


```python
- Identify students who have utilized specific support services.

SELECT Student.id, Student.name
FROM Student
JOIN StudentSupportService ON Student.id = StudentSupportServices.student_id
JOIN SupportServices ON StudentSupportService.SupportService_id = SupportService.id
WHERE SupportService.name = 'Tutoring Services';

```
