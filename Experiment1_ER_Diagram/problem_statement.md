# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario: City Library Event & Book Lending System

## Business Context
The Central Library wants to manage book lending and cultural events.

## Requirements
- Members borrow books, with loan and return dates tracked.
- Each book has title, author, and category.
- Library organizes events; members can register.
- Each event has one or more speakers/authors.
- Rooms are booked for events and study.
- Overdue fines apply for late returns.

---

## ER Diagram

<img width="1246" height="951" alt="Untitled Diagram drawio" src="https://github.com/user-attachments/assets/8bae1834-1307-4697-bedc-909bc1c0b0d7" />


---

## Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Members | member_id (PK), name, mobile_number | Stores library member details |
| Book | book_id (PK), title, author, category | Stores information about books |
| Event | event_id (PK), name, date_time | Stores cultural/library events |
| Speaker | speaker_id (PK), name, domain | Stores speaker/author details |
| Room | room_id (PK), type, capacity | Rooms used for events/study |
| Registration | register_id (PK), member_id (FK), event_id (FK) | Tracks member registrations for events |
| Borrow | member_id (FK), book_id (FK), loan_date, due_date, return_date, fine_amount | Tracks borrowing and overdue fines |
| Event_Speaker | event_id (FK), speaker_id (FK) | Represents speakers participating in events |

---

## Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|-------------|---------------|-------|
| Members — Borrow — Book | 1 : M | Partial | One member can borrow many books |
| Members — Registration — Event | M : N | Partial | Members can register for many events |
| Event — Event_Speaker — Speaker | M : N | Total on Event | Each event has one or more speakers |
| Event — Room | M : 1 | Total on Event | Each event is assigned to one room |

---

## Assumptions

- A member can borrow multiple books.
- Fine amount is calculated when return date exceeds due date.
- Each event must be assigned to exactly one room.
- An event can have multiple speakers.
- Members can register for multiple events.

---
