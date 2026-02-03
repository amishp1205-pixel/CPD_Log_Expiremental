# Project Spec: CPD Log Project Expiremntal

---

## 1. Project Goal

Primary goal:
Prototyping to see if something is possible


**Goal statement:**
To create a web based continuing professional development log for UK pharmacists and level 3 dispensing technicians which makes making and viewing entries easier

**What does success look like?**
when it takes half the time it does compared to the manual process of making a CPD entry for a learning 

---

## 2. Milestones

**What are the phases of functionality you want?**

### MVP (Milestone 1)
- Feature: Ask user what they have learnt set fields for this
- Feature: Convert the learning entry into an output which meets the reuirements and guidance set down by the UK pharmacy regulalator the GPhC for continuing professional development (CPD) entries for pharamcists and level 3 dispensing technicians 
- Feature: Allow user to edit the CPD output  
- Feature: Allow user to download a version of the CPD output 
  

**What are you okay leaving out of the MVP?**
> User registration and login and authentication and payment gateway

### Version 2 (Milestone 2)

- Feature: user registration and authentication includes google authentication, payment
- Feature: build a log of cpd entries for the user which the user can view

### Future Versions
- check for similar entries to encourage varied learning
- to keep track the required number of entries have been made and issue alerts if they have not
- have a section of resorces to provide learning
-  allow a print out of cpd entries over a user specified date range
- have categories for cpd entry 
- dashboard which displays number of cpd donefor the year and number pending and cpd entries by category
---

## 3. Product Requirements

### Who is this for?

**Target user:**
> UK registered pharmacist and level 3 dispensing technicians

**User context:**
> when ever a pharmacist and level 3 dispensing technicians undertakes a learning they would use this application to create a cpd entry for it

### What problems does it solve?

1. Problem: takes time to think how to make a cpd entry of the learning 
2. Problem: creates frustration as learning should be positive not encumbered with a cpd entry process which adds extra work
3. Problem: no current application which does this

### What should the product do?

**Be specific about user interactions.** Don't just say "users can create entries" — describe the experience.

User Action 1
- on the main page a button record learning is displayed and when selected carry out the below

What Happens 
- display title Learning Entry with fields for learning entry questions listed below and a submit button under it

learning entry questions
- Q1 what did you learn
- Q2 How did you plan the learning include training sources
- Q3 what topics and areas did the learning cover 
- Q4 how will you apply this learning in practice
- Q5 if you have applied it give examples of how in practice
- Q6 key benefits of service users from your learning 
- Q7 how do you feel the service you offer has been enhanced by your learning


User Action 2
- submit button selected for the learning entry 

What Happens 
- call on an ai tool to generate a cpd entry based on the gphc standards for making cpd entries. 
- there is a reference file for examples of good quality cpd entries. 
 - cpd entry is displayed with an option for user to edit and also for the use to download the entry

 
**Key user flows to define:**
> make an entry of the learning they submit and an output of a cpd entry is created. user can edit and download this

## 4. Technical Requirements

### Tech Stack
*need claude code to help determine this*
can you please decide the tech stack but need to use replit



### Technical Architecture

**System overview:**
> [High-level description of how the major pieces fit together]

**Key components:**
1. Component: _______________ — Purpose: _______________
2. Component: _______________ — Purpose: _______________
3. Component: _______________ — Purpose: _______________

**Database schema (initial):**
> [List your main entities/tables and their key fields]

**API design (if applicable):**
> [List your main endpoints or describe your API approach]

### Infrastructure to Provision

Before building, set up:
- [ ] Database instance
- [ ] Hosting environment
- [ ] API keys for: _______________
- [ ] Domain name (optional)
- [ ] Other: _______________

---

---

## 6. Out of Scope

Explicitly list what you are NOT building (to prevent scope creep):

- an ecommerce site
- 
- _______________
- _______________

---

## Summary

**One-liner:** tool to aid easier cpd entries

**MVP scope:** learning entry and cpd entry generator 

**Tech stack:** replit

**First milestone "done" looks like:** it generates a cpd entry in line with uk pharmacy regulators 

---

> **Next step:** Once this spec is complete, move to the [Setup Checklist](./avthar_new_project_checklist.md) to configure Claude Code for your project.
