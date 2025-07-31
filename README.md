# Online-Course-Management-System


#  Online Course Management System - OOP Design Interview

## Objective

Simulate a **System Design Interview** by modeling a real-world **Online Course Management System** using **Object-Oriented Programming (OOP)** concepts.

---

## Scenario Overview

Design a platform supporting:

- **User Roles:** Student, Instructor
- **Functionalities:** 
  - Course Creation
  - Enrollment Management
  - Assignment Upload and Grading
  - Role-based Access Control

---

##  Task 1: UML Class Diagram

<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/9f992f71-c6e5-4026-b500-e04632461368" />


### Includes:

- `User` superclass with subclasses `Student` and `Instructor`
- `Course`, `Assignment`, and `Grade` classes
- Inheritance & Association relationships
- Public/private members and at least one overridden method

---

##  Task 2: JavaScript Implementation (Core Classes)

```
class User {
  constructor(id, name, email, password) {
    this._id = id;
    this._name = name;
    this._email = email;
    this._password = password;
  }

  get id() { return this._id; }
  get name() { return this._name; }
  set name(newName) { this._name = newName; }
  get email() { return this._email; }
  set email(newEmail) { this._email = newEmail; }

  login() {
    console.log(`${this._name} logged in`);
  }

  logout() {
    console.log(`${this._name} logged out`);
  }
}

class Student extends User {
  constructor(id, name, email, password, studentId) {
    super(id, name, email, password);
    this._studentId = studentId;
    this._enrolledCourses = [];
  }

  login() {
    console.log(`Student ${this._name} logged in`);
  }

  enroll(course) {
    this._enrolledCourses.push(course);
    console.log(`${this._name} enrolled in ${course.title}`);
  }
}

class Instructor extends User {
  constructor(id, name, email, password, instructorId) {
    super(id, name, email, password);
    this._instructorId = instructorId;
    this._coursesTaught = [];
  }

  login() {
    console.log(`Instructor ${this._name} logged in`);
  }

  createCourse(title, description) {
    const course = new Course(Date.now().toString(), title, description, this);
    this._coursesTaught.push(course);
    return course;
  }

  gradeAssignment(grade, score, feedback) {
    grade.score = score;
    grade.feedback = feedback;
    console.log(`Assignment graded by ${this._name}`);
  }
}

class Course {
  constructor(id, title, description, instructor) {
    this._id = id;
    this._title = title;
    this._description = description;
    this._instructor = instructor;
    this._assignments = [];
  }

  createAssignment(title, description, dueDate) {
    const assignment = new Assignment(Date.now().toString(), title, description, dueDate);
    this._assignments.push(assignment);
    return assignment;
  }
}

class Assignment {
  constructor(id, title, description, dueDate) {
    this._id = id;
    this._title = title;
    this._description = description;
    this._dueDate = dueDate;
  }
}

class Grade {
  constructor(assignment, student, submission) {
    this._assignment = assignment;
    this._student = student;
    this._submission = submission;
    this._score = null;
    this._feedback = null;
  }

  calculateGrade() {
    if (this._score >= 90) return 'A';
    if (this._score >= 80) return 'B';
    if (this._score >= 70) return 'C';
    if (this._score >= 60) return 'D';
    return 'F';
  }
}

```

## Task 3: OOP Design Explanation

###  1.Abstraction
- Real-world entities like `User`, `Course`, `Assignment` are modeled as classes.

###  2.Encapsulation
- Private fields (e.g., `_id`, `_password`) are accessed using getter/setter methods.

###  3.Inheritance
- `Student` and `Instructor` classes inherit from `User`.

###  4.Polymorphism
- `login()` method is overridden in both `Student` and `Instructor` to demonstrate role-based behavior.

---

##  SOLID Principles Applied

| Principle | Description |
|----------|-------------|
| **S** - Single Responsibility | Each class does one job (e.g., `Grade` handles grading only) |
| **O** - Open/Closed | Easily extendable with new roles or features |
| **L** - Liskov Substitution | `Student`/`Instructor` can be used wherever `User` is expected |
| **I** - Interface Segregation | Only essential methods exposed |
| **D** - Dependency Inversion | High-level logic (grading) depends on abstraction not concrete classes |

---

