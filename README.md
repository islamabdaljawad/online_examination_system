# Online Examination System  
## Technical Documentation

**Type:** Technical Documentation  
**Tech Stack:** SQL Server · Windows Forms (.NET) · Power BI  

### Team Members
- Islam Abd Aljawad Ahmed  
- Ali Mohamed Ali  
- Passant Gamal Kamal  
- Passant Gamal Kamal  
- Maged Elshebeny  
- Assem Omar Mohamedy  

---

## 1. Overview

The **Online Examination System (OES)** is a complete digital examination platform designed for **real academic environments**, not just academic demos.

The system supports:
- Exam creation and management
- Student exam execution
- Automatic correction
- Performance analytics using Power BI

---

## 2. System Architecture

### 2.1 Architecture Layers

- **Database Layer** → SQL Server (`Online_examination_system`)
- **Application Layer** → Windows Forms (.NET)
- **Analytics Layer** → Power BI

```text
[Windows Forms Application]
          ↓
[SQL Server Database]
          ↓
[Power BI Dashboards]
```

---

## 3. Database Design

### 3.1 Design Principles

- Fully normalized schema (3NF)
- Junction tables for many-to-many relationships
- Strong referential integrity
- Real-world constraints and validations

---

## 4. Database Mapping

### 4.1 Academic Structure Mapping

**Branch → Department**  
- Relationship: One-to-Many  
- Branch.BranchID → Department.BranchID  

**Department → Student**  
- Relationship: One-to-Many  
- Department.DepartmentID → Student.DepartmentID  

**Department ↔ Course**  
- Relationship: Many-to-Many  
- Junction Table: `Department_Course`  

**Instructor ↔ Department**  
- Relationship: Many-to-Many  
- Junction Table: `Instructor_Department`  

**Instructor ↔ Course**  
- Relationship: Many-to-Many  
- Junction Table: `Instructor_Course`  

---

### 4.2 Examination Mapping

**Course → Exam**  
- Relationship: One-to-Many  
- Course.CourseID → Exam.CourseID  

**Exam ↔ QuestionBank**  
- Relationship: Many-to-Many  
- Junction Table: `Exam_QuestionBank`  

**QuestionBank → Choice**  
- Relationship: One-to-Many  
- QuestionBank.QuestionID → Choice.QuestionID  

**Student ↔ Exam**  
- Relationship: Many-to-Many  
- Junction Table: `Student_Exam`  

**Student → Student_Answer**  
- Relationship: One-to-Many  

---

## 5. Entity Relationship Diagram (ERD)

### 5.1 ERD Diagram

![[images/ERD.jpeg]]

<div style="page-break-after: always;"></div>

### 5.2 Mapping Diagram

![[images\mapping.jpeg]]

<div style="page-break-after: always;"></div>

### 5.3 ERD (Database Implementation)

![[images/ERD in Databse.jpeg]]

<div style="page-break-after: always;"></div>

---

## 6. Core Entities

### Branch
- BranchID (PK)
- Name
- Location

### Department
- DepartmentID (PK)
- Name
- BranchID (FK)

### Course
- CourseID (PK)
- Title

### Instructor
- InstructorID (PK)
- Name
- Email (Unique)
- BranchID (FK)

### Student
- StudentID (PK)
- Name
- Email (Unique)
- BranchID (FK)
- DepartmentID (FK)

---

## 7. Examination Module

### Exam
- ExamID (PK)
- Title
- CourseID (FK)
- InstructorID (FK)
- DurationMinutes

### QuestionBank
- QuestionID (PK)
- Text
- Type (MCQ | True/False)
- Mark
- CourseID (FK)

### Choice
- ChoiceID (PK)
- Title
- IsCorrect
- QuestionID (FK)

---

## 8. Relationship Tables

- Instructor_Course
- Instructor_Department
- Department_Course
- Student_Course
- Exam_QuestionBank

---

## 9. Exam Execution Flow

### Student_Exam
- StudentID (PK)
- ExamID (PK)
- Score
- TakenAt

### Student_Answer
- StudentID (PK)
- ExamID (PK)
- QuestionID (PK)
- ChoiceID (FK)

---

## 10. Automatic Exam Correction

1. Retrieve student answers  
2. Compare with correct choices  
3. Calculate total score  
4. Store results  

---

## 11. Power BI Integration

### Dashboards
- Students by department
- Student grades
- Instructor courses
- Exam analytics

---

## 12. Future Enhancements

- Essay questions
- Web version
- Power BI Service
- AI-based difficulty analysis

---

## 13. Conclusion

The **Online Examination System** is a scalable, production-ready academic platform.
