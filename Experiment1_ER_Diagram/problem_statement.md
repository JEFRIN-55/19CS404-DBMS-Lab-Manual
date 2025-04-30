# Experiment 1: Entity-Relationship (ER) Diagram

## 🎯 Objective:
To understand and apply the concepts of ER modeling by creating an ER diagram for a real-world application.

## 📚 Purpose:
The purpose of this workshop is to gain hands-on experience in designing ER diagrams that visually represent the structure of a database including entities, relationships, attributes, and constraints.

---

## 🧪 Choose One Scenario:

### 🔹 Scenario 1: University Database
Design a database to manage students, instructors, programs, courses, and student enrollments. Include prerequisites for courses.

**User Requirements:**
- Academic programs grouped under departments.
- Students have admission number, name, DOB, contact info.
- Instructors with staff number, contact info, etc.
- Courses have number, name, credits.
- Track course enrollments by students and enrollment date.
- Add support for prerequisites (some courses require others).

---

### 🔹 Scenario 2: Hospital Database
Design a database for patient management, appointments, medical records, and billing.

**User Requirements:**
- Patient details including contact and insurance.
- Doctors and their departments, contact info, specialization.
- Appointments with reason, time, patient-doctor link.
- Medical records with treatments, diagnosis, test results.
- Billing and payment details for each appointment.

---

## 📝 Tasks:
1. Identify entities, relationships, and attributes.
2. Draw the ER diagram using any tool (draw.io, dbdiagram.io, hand-drawn and scanned).
3. Include:
   - Cardinality & participation constraints
   - Prerequisites for University OR Billing for Hospital
4. Explain:
   - Why you chose the entities and relationships.
   - How you modeled prerequisites or billing.

# ER Diagram Submission - Student Name

## Scenario Chosen:
University 

## ER Diagram:
![WhatsApp Image 2025-04-30 at 15 08 59_6aceb566](https://github.com/user-attachments/assets/0ef7b5f5-08e4-40fa-83f6-538a44323751)

## Entities and Attributes:

Student  
   Attributes: admission number (ad.no), full name, date of birth (DOB), mobile number, email

Faculty  
   Attributes: staff number, name, mobile number, email

Program  
   Attributes: identifier, name, governing department

Courses  
   Attributes: course number, name, number of credits, total units
...

## Relationships and Constraints:

Enroll

   Between: Student and Program   
   Cardinality: Many students enroll in one program
   
Learn

   Between: Student and Courses  
   Cardinality: Many students learn many courses (Many-to-Many)

Teach

   Between: Faculty and Courses  
   Cardinality: One faculty can teach many courses; a course can be taught by one or more faculty

Prerequisite

   Between: Courses and Courses  
   Cardinality: One course can be a prerequisite for one or more other courses
...

## Extension (Prerequisite / Billing):
The "prerequisite" relationship is used to model course dependencies.
   Each course may require another course to be completed first.
   This is represented as a recursive relationship on the Courses entity.
 
## Design Choices:
Program is connected to the Student via an "enroll" relationship, showing student registration.
   Faculty and Student both connect to Courses via "teach" and "learn" relationships, respectively.
   The Courses entity includes standard attributes like course number, name, and credits.
   The Prerequisite is added as a recursive relationship, essential in university course planning.


## RESULT
Successfully designed and submitted an ER diagram for a University Database showing Students, Faculty, Courses, Programs, and the relationship among them including prerequisites.
