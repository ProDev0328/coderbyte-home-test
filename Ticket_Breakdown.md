# Ticket Breakdown
We are a staffing company whose primary purpose is to book Agents at Shifts posted by Facilities on our platform. We're working on a new feature which will generate reports for our client Facilities containing info on how many hours each Agent worked in a given quarter by summing up every Shift they worked. Currently, this is how the process works:

- Data is saved in the database in the Facilities, Agents, and Shifts tables
- A function `getShiftsByFacility` is called with the Facility's id, returning all Shifts worked that quarter, including some metadata about the Agent assigned to each
- A function `generateReport` is then called with the list of Shifts. It converts them into a PDF which can be submitted by the Facility for compliance.

## You've been asked to work on a ticket. It reads:

**Currently, the id of each Agent on the reports we generate is their internal database id. We'd like to add the ability for Facilities to save their own custom ids for each Agent they work with and use that id when generating reports for them.**


Based on the information given, break this ticket down into 2-5 individual tickets to perform. Provide as much detail for each ticket as you can, including acceptance criteria, time/effort estimates, and implementation details. Feel free to make informed guesses about any unknown details - you can't guess "wrong".


You will be graded on the level of detail in each ticket, the clarity of the execution plan within and between tickets, and the intelligibility of your language. You don't need to be a native English speaker, but please proof-read your work.

## Your Breakdown Here
  # Ticket 1. Database design
    facility
    -id
    -name

    agent
    -id
    -name

    shift
    -id
    -agent_id
    -custom_id
    -facility_id
    -start_time
    -duration

  # Ticket 2. Storing data
    - While creating a shift at facility, we should check they're overlapping.
    - When booking a agent to shift, we should check that agent is booking on another shift at the same time.
    - When booking a agent to shift, we should generate a custom_id which can be used in reports.
        customer_id can be generated something like that `timestamp_${agent_id}_${facility_id}`

  # Ticket 3. Implementation
    - getShiftsByFacility - queries shift table by facility_id that quarter (should join agent table for meta data)
    - generateReport - get shifts data from calling getShiftsByFacility and convert them to pdf
