# User Story: Reschedule an Appointment

## User Story

As a patient,  
I want to reschedule my scheduled appointment,  
so that I can choose a new appointment time that better fits my availability.

## Description

Patients need the ability to change an existing appointment when they cannot attend at the originally scheduled time.

If a patient requests to reschedule less than 24 hours before the original appointment, the system must identify the request as a late change. The system must still update the appointment if the requested time is available, notify the Notification Service, and show the patient the updated appointment details.

## Acceptance Criteria

```gherkin
Scenario: Patient reschedules an appointment within 24 hours

Given a patient has a scheduled appointment for "2026-10-15T10:00:00Z"
And the patient submits a reschedule request less than 24 hours before the original appointment time
When the patient requests to reschedule the appointment to "2026-10-16T14:00:00Z"
Then the system should update the appointment to "2026-10-16T14:00:00Z"
And the system should apply a late-change flag
And the system should emit an "AppointmentRescheduled" event to the Notification Service
And the system should display a confirmation message with updated appointment details to the patient
```

## Business Rules

- A reschedule request made less than 24 hours before the original appointment time is a late change.
- The system must apply a late-change flag for a late change.
- The system must update the appointment only when the requested new appointment time is available.
- The system must send an `AppointmentRescheduled` event after a successful reschedule.
- The system must display a confirmation message after the appointment is successfully updated.

## Expected Confirmation Message

> Your appointment has been rescheduled to October 16, 2026 at 14:00 UTC. A late-change flag has been applied because the request was made less than 24 hours before the original appointment time.
