# CampusAssist AI – Smart IT Support Portal and AI-Assisted Troubleshooting System in ServiceNow

## Overview

**CampusAssist AI** is a ServiceNow-based smart IT support portal designed to help students troubleshoot common campus technology issues through an interactive self-service assistant.

The system includes **CampusCare AI**, an interactive troubleshooting chatbot that guides students through predefined troubleshooting paths for **WiFi, Hardware, Software, and Account Lock** issues.

When an issue cannot be resolved through self-service troubleshooting, CampusAssist AI provides a **context-aware escalation mechanism** that redirects the student to a native ServiceNow request form with relevant issue information pre-populated.

The project demonstrates the integration of ServiceNow **Scoped Applications, Service Portal, custom tables, widgets, client-side logic, backend scripting, conversational state management, and native form integration**.

---

## Project Objectives

* Provide students with a centralized campus IT support portal.
* Enable self-service troubleshooting for common IT problems.
* Reduce unnecessary IT support requests.
* Guide students through structured troubleshooting steps.
* Maintain conversational state during troubleshooting.
* Support multiple IT issues within a single session.
* Escalate unresolved issues to IT support with relevant context.
* Integrate the chatbot with native ServiceNow request forms.
* Store structured student IT requests in a custom ServiceNow table.
* Demonstrate practical ServiceNow application development skills.

---

## Key Features

### 🤖 CampusCare AI Chatbot

An interactive ServiceNow Service Portal chatbot that guides students through troubleshooting workflows.

Supported issue categories:

* WiFi Issues
* Hardware Issues
* Software Issues
* Account Lock Issues

### 🔄 Multi-Issue Session Management

CampusCare AI maintains the current troubleshooting context while a student is working on an issue.

After an issue is resolved or completed, the conversational state is reset so that students can start another issue without the previous issue affecting the new session.

### 🧭 Guided Troubleshooting

The chatbot uses structured decision-tree logic to provide relevant troubleshooting steps based on the selected issue category.

### 🚨 Context-Aware Ticket Escalation

If troubleshooting does not resolve the problem, the chatbot provides an escalation path to IT support.

Relevant information collected during the troubleshooting process can be transferred to the ServiceNow request process.

### 📝 Pre-Filled ServiceNow Request

The system redirects the student to a native ServiceNow form and can use URL parameters such as `sysparm_query` to pre-populate relevant request information.

### 🗃️ Student IT Request Management

Escalated requests are stored in the custom Student IT Request table for further processing and tracking by IT support staff.

---

## Technology Stack

| Technology             | Purpose                                        |
| ---------------------- | ---------------------------------------------- |
| ServiceNow             | Application and IT service management platform |
| Scoped Application     | Application isolation and development          |
| Service Portal         | Student-facing support interface               |
| Service Portal Widgets | CampusCare AI chatbot interface                |
| HTML5                  | Widget and portal structure                    |
| CSS3                   | User interface styling                         |
| AngularJS              | Service Portal client-side interaction         |
| JavaScript             | Application and chatbot logic                  |
| Glide API              | ServiceNow backend interaction                 |
| ServiceNow Tables      | Structured request data storage                |
| ServiceNow Forms       | IT request submission                          |
| `sysparm_query`        | Context-based form pre-population              |

---

## ServiceNow Application

**Application Name:** CampusAssist AI

**Application Type:** Scoped Application

**Application Scope:** CampusAssist AI

**Service Portal Pages:**

* `campusassist_home`
* `campuscare_chatbot`

---

## Custom Data Model

### Student IT Request Table

**Table Name:**

```text
x_2065601_campus_0_student_it_request
```

### Fields

| Field          | Type   | Description                     |
| -------------- | ------ | ------------------------------- |
| `student_name` | String | Stores the student's name       |
| `student_id`   | String | Stores the student's identifier |
| `department`   | Choice | Stores the student's department |
| `issue_type`   | Choice | Stores the selected IT issue    |
| `description`  | String | Stores issue details            |
| `state`        | Choice | Tracks the request status       |

### Issue Type Choices

```text
wifi_issue
hardware_issue
software_issue
account_issue
```

---

## Project Architecture

```text
┌─────────────────────────────────────────────┐
│                 STUDENT                     │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│        CampusAssist AI Service Portal       │
│             campusassist_home               │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│          CampusCare AI Chatbot              │
│            campuscare_chatbot               │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│        Troubleshooting Decision Logic       │
│                                             │
│   WiFi │ Hardware │ Software │ Account      │
└──────────────────────┬──────────────────────┘
                       │
             ┌─────────┴─────────┐
             │                   │
             ▼                   ▼
      ┌─────────────┐     ┌─────────────────┐
      │   Resolved  │     │   Unresolved    │
      │    Issue    │     │      Issue      │
      └─────────────┘     └────────┬────────┘
                                   │
                                   ▼
                       ┌──────────────────────┐
                       │ Context-Aware        │
                       │ Ticket Escalation    │
                       └──────────┬───────────┘
                                  │
                                  ▼
                       ┌──────────────────────┐
                       │ Native ServiceNow    │
                       │ Request Form         │
                       └──────────┬───────────┘
                                  │
                                  ▼
                       ┌──────────────────────┐
                       │ Student IT Request   │
                       │ Custom Table         │
                       └──────────┬───────────┘
                                  │
                                  ▼
                       ┌──────────────────────┐
                       │    IT Support        │
                       └──────────────────────┘
```

---

## Project Workflow

The basic workflow is:

```text
Student Accesses Portal
        ↓
Opens CampusCare AI
        ↓
Selects IT Issue
        ↓
Troubleshooting Begins
        ↓
Issue Resolved?
     ↙       ↘
   YES        NO
    ↓          ↓
Session     Continue
Complete    Troubleshooting
               ↓
          Still Unresolved?
               ↓
          Escalate to IT
               ↓
       Pre-Filled ServiceNow
            Request Form
               ↓
          Submit Request
               ↓
       Student IT Request
             Record
```

---

## Multi-Issue Session Workflow

CampusCare AI supports sequential handling of multiple issues.

```text
Issue 1 Selected
      ↓
Troubleshooting
      ↓
Issue Resolved
      ↓
Session State Reset
      ↓
New Issue Selected
      ↓
New Troubleshooting Session
```

The session reset prevents information from a previous issue from incorrectly influencing the next troubleshooting interaction.

---

## Context-Aware Escalation

When self-service troubleshooting does not resolve an issue, the system transfers relevant information into the ServiceNow request process.

Possible contextual information includes:

* Student information
* Issue category
* Problem description
* Troubleshooting context

The purpose is to reduce duplicate data entry and provide IT support with better information about the reported problem.

---

## Project Phases

### 1. Ideation Phase

Focuses on identifying the campus IT support problem and developing the CampusAssist AI concept.

Documentation includes:

* Brainstorming Idea
* Problem Statement Context
* Empathy Map Canvas

### 2. Project Planning Phase

Defines the project scope, objectives, modules, implementation roadmap, milestones, testing strategy, and deliverables.

Documentation includes:

* Project Planning

### 3. Project Development Phase

Covers the implementation and validation of the CampusAssist AI solution in ServiceNow.

Activities include:

* ServiceNow application configuration
* Custom table configuration
* Service Portal configuration
* CampusCare AI development
* Troubleshooting logic
* Session management
* Ticket escalation
* Form integration
* Testing
* User acceptance testing

Documentation includes:

* ServiceNow Testing
* User Acceptance Report

### 4. Project Documentation

Contains the complete technical documentation of the implemented system.

Documentation includes:

* ServiceNow Capstone Documentation

### 5. Project Demonstration

Demonstrates the complete working system from student portal access through troubleshooting and ticket creation.

Includes:

* Demonstration document
* Screenshots
* Demo video

---

## Repository Structure

```text
CampusAssist-AI-Smart-IT-Support-Portal-and-AI-Assisted-Troubleshooting-System-in-ServiceNow/
│
├── 1. Ideation Phase/
│   ├── 1.1 Brainstorming Idea.pdf
│   ├── 1.2 Problem Statement Context.pdf
│   ├── 1.3 Empathy Map Canvas.pdf
│   └── README.md
│
├── 2. Project Planning Phase/
│   ├── 2.1 Project Planning.pdf
│   └── README.md
│
├── 3. Project Development Phase/
│   ├── 3.1 ServiceNow Testing.pdf
│   ├── 3.2 User Acceptance Report.pdf
│   └── README.md
│
├── 4. Project Documentation/
│   ├── 4.1 ServiceNow Capstone Documentation.pdf
│   └── README.md
│
├── 5. Project Demonstration/
│   ├── 5.1 Project Demonstration.pdf
│   ├── Screenshots/
│   ├── Demo Video/
│   └── README.md
│
└── README.md
```

---

## Installation & Setup

### Prerequisites

* ServiceNow Developer Instance
* Administrative or appropriate application-development access
* Basic knowledge of ServiceNow scoped applications
* Service Portal access
* ServiceNow application configuration knowledge

### Setup Process

#### Step 1 — Access ServiceNow

Log in to the designated ServiceNow Developer Instance.

#### Step 2 — Open the Application

Navigate to the CampusAssist AI scoped application.

#### Step 3 — Configure Application Components

Verify:

* Application scope
* Application menu
* Custom table
* Fields
* Choice values
* Service Portal pages
* Service Portal widget
* Required scripts and configurations

#### Step 4 — Configure the Service Portal

Verify the following pages:

```text
campusassist_home
campuscare_chatbot
```

#### Step 5 — Verify the Custom Table

Confirm that the following table exists:

```text
x_2065601_campus_0_student_it_request
```

Verify the configured fields and choice values.

#### Step 6 — Test CampusCare AI

Test:

* WiFi troubleshooting
* Hardware troubleshooting
* Software troubleshooting
* Account-lock troubleshooting
* Multi-issue sessions
* Escalation

#### Step 7 — Test Request Creation

Verify that unresolved issues can be transferred to the ServiceNow request form and that the submitted information is stored correctly.

---

## Usage

### Student Support Workflow

1. Open the CampusAssist AI portal.
2. Launch CampusCare AI.
3. Select the relevant IT issue.
4. Follow the troubleshooting instructions.
5. Confirm whether the issue is resolved.
6. If resolved, complete the session.
7. If unresolved, continue troubleshooting.
8. If the issue remains unresolved, select the escalation option.
9. Review the pre-filled ServiceNow request.
10. Submit the request.
11. IT support can process the resulting request.

---

## Testing

Testing covers the complete application lifecycle.

### Functional Testing

* Portal access
* Chatbot launch
* Issue selection
* WiFi troubleshooting
* Hardware troubleshooting
* Software troubleshooting
* Account-lock troubleshooting
* Session reset
* Multiple issue handling
* Escalation
* Request form population
* Request creation

### Integration Testing

* Chatbot-to-ServiceNow form integration
* Context transfer
* Custom table record creation

### User Acceptance Testing

Student-oriented scenarios are used to verify that the application provides the expected self-service support experience.

Detailed test results are available in:

```text
3. Project Development Phase/
```

---

## Troubleshooting

### Chatbot Does Not Load

Verify:

* Service Portal page configuration.
* Widget availability.
* Widget client controller configuration.
* Portal permissions.

### Issue Flow Does Not Start

Verify:

* Issue choice configuration.
* Client-side chatbot logic.
* Correct issue identifiers.

### Previous Issue Information Appears in a New Session

Verify that the chatbot session state is reset after the previous issue is completed.

### Escalation Does Not Open the Correct Form

Verify:

* Target ServiceNow table/form.
* URL parameters.
* `sysparm_query` configuration.
* Field names.
* Encoded query values.

### Request Is Not Created

Verify:

* Table configuration.
* Mandatory fields.
* User permissions.
* Form configuration.
* Record creation logic.

---

## Future Enhancements

Possible future improvements include:

* Natural-language AI-based issue understanding.
* ServiceNow Knowledge Base integration.
* Virtual Agent integration.
* Automated issue classification.
* Intelligent ticket prioritization.
* IT support analytics dashboards.
* Automated notifications.
* Multilingual support.
* Campus identity-system integration.
* Predictive analysis of frequently reported IT issues.

These enhancements are outside the current implemented scope unless explicitly added to the project.

---

## Project Outcome

CampusAssist AI demonstrates how ServiceNow can be used to create a campus-focused IT self-service solution.

The project combines:

* Scoped application development
* Service Portal
* Service Portal widgets
* Custom ServiceNow tables
* Choice configuration
* JavaScript
* AngularJS
* Glide APIs
* Guided troubleshooting
* Conversational state management
* Multi-issue sessions
* Context-aware escalation
* Native ServiceNow form integration
* Structured IT request management

The solution provides students with a centralized support experience while giving IT support staff better contextual information when an issue requires escalation.

---

## Author

**Santhosh Akkisetti**

### Project

**CampusAssist AI – Smart IT Support Portal and AI-Assisted Troubleshooting System in ServiceNow**

### Repository

[CampusAssist AI – GitHub Repository](https://github.com/santhoshakkisetti/CampusAssist-AI-Smart-IT-Support-Portal-and-AI-Assisted-Troubleshooting-System-in-ServiceNow?utm_source=chatgpt.com)

---

## License

This project is developed for **educational, academic, and portfolio purposes**.

---

## Acknowledgments

This project demonstrates the application of ServiceNow development concepts to a campus IT support scenario, combining self-service interaction, troubleshooting workflows, structured data management, and contextual IT request escalation.

---

**Version:** 1.0

**Last Updated:** August 2026

**Project Status:** Development / Demonstration
