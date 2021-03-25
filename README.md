# ThirdAssesment-ARTILLERY

TO RUN THIS ONE: We have a script: "npm run artillerytesting"

scenarios:
  - flow:
      - get:
          url: "/rest/v1/tasks"
##This Scenario is for creating task on our main project.
      - post:
          url: "/rest/v1/tasks"
          json:
           content: "This is for you to take the cert exams."
           due_string: "tuesday at 12:00"
           due_lang: "en"
           priority: 0
           project_id: 2261220983
          capture:
           json: "$.id"
           as: "taskID"
      - log: "The task your creating is {{ taskID }}"

##This Scenario is for getting active task on our main project.
      - get:
          url: "/rest/v1/tasks/{{ taskID }}"
##This One  is for Updating the tasks on main project.
      - post:
          url: "/rest/v1/tasks/{{ taskID }}"
          json:
           content: "We're changing the duedate of the exams"
           due_string: "Friday at 20:00"
           priority: 2

##This Scenario is for closing the tasks on main project.           
      - post:
          url: "/rest/v1/tasks/{{ taskID }}/close"

##This Scenario is for Reopening tasks on main project.           
      - post:
          url: "/rest/v1/tasks/{{ taskID }}/reopen"

##This Scenario is for Deleting all tasks we created on main project. 
      - delete:
          url: "/rest/v1/tasks/{{ taskID }}"
