## I. Project Title
**Taskpulse**  
*An academic tracker that helps students prioritize activities, flags tasks due within 24 hours, and creates optimal study blocks.*

---

## II. Problem Statement
With many ways of doing activities and tasks in this current world, students are overwhelmed with assessments that could hurt them mentally and drain them physically. Even though there are solutions like manual planners, they are tedious to maintain. This problem not only affects high schoolers but can also affect students until college who have heavy workloads. Solving this problem can reduce anxiety and stop bad habits like cramming.

---

## III. Project Objectives
By the end of the first quarter, I aim to achieve the following objectives for Taskpulse:
* **Urgency Characterization Module:** Program a backend classification logic that automatically scans a user's task list and tags 100% of items due within 24 hours as "REQUIRED IMMEDIATELY" while sorting remaining tasks into accurate priority buckets (Low, Medium, High).
* **Automated Study-Block Generator:** Design a scheduling algorithm that filters tasks labeled "REQUIRED IMMEDIATELY," sorts them chronologically by due date, and dynamically outputs a structured daily study roadmap for the user.
* **Completion Progress Tracker:** Implement a real-time visual progress monitoring system that accurately calculates the percentage of finished assignments against total active tasks using the formula: `(completed_count / total_count) * 100`.

---

## IV. Planned Features
1. **Characterize Tasks Based on Urgency:** Automatically categorizes assignments based on remaining time.
2. **Automated Time-Block Generator:** Dynamically creates a focused daily study schedule around critical deadlines.
3. **Visual Progress Tracker:** Displays a calculated overview of completion statistics to maintain academic momentum.

---

## V. Planned Inputs and Outputs

### Desired Inputs
* **Task Submission Data:** The task title, the course/subject, and the explicit due date of the task.
* **Completion Checkmark:** A user action to flag a specific task record as finished or completed.

### Desired Outputs
* **Urgent Task Visual Indicator:** Displays tasks that are due in 24 hours and flags them prominently with a "REQUIRED IMMEDIATELY" status indicator.
* **Structured Study Routine:** A customized daily roadmap outlining precisely what needs to be reviewed or completed.
* **Visual Progress Bar:** A graphical dashboard interface showing the numerical percentage of completed requirements.

---

## VI. Logic Plan (Pseudocode)

```text
Start
    // STEP 1: Initialization
    INITIALIZE task_database AS Empty List
    
    // STEP 2: Execution Loop
    While program_is_active IS True:
        Set current_time = GetSystemTime()
        
        // FEATURE 1 LOGIC: Urgency Characterization
        FOR EACH task IN task_database:
            Calculate time_remaining = task.due_date - current_time
            
            IF time_remaining <= 24 hours AND task.status != "Completed":
                Set task.priority_level = "REQUIRED IMMEDIATELY"
            ELSE IF time_remaining > 24 hours AND time_remaining <= 72 hours:
                Set task.priority_level = "Medium Level"
            ELSE:
                Set task.priority_level = "Low Level"
            ENDIF
        ENDFOR
        
        // FEATURE 3 LOGIC: Completion Tracking
        Set total_count = COUNT ALL ITEMS IN task_database
        Set completed_count = COUNT ITEMS IN task_database WHERE task.status == "Completed"
        
        IF total_count > 0:
            Calculate visual_percentage = (completed_count / total_count) * 100
        ELSE:
            SET visual_percentage = 0
        ENDIF
        
        Display visual_percentage ON Progress Bar Interface
        Display Triage Dashboard (Urgent vs Standard Tasks)
        
        // STEP 3: Handle Planned Input Actions
        IF User selects "Create Task":
            Input user_task_title, user_subject, user_due_date
            Create new_task_record with status = "Pending"
            Save new_task_record TO task_database
            
        ELSE IF User selects "Mark Task Completed":
            Update target_task.status = "Completed"
            
        // FEATURE 2 LOGIC: Study Block Generation
        ELSE IF User selects "Generate Study Blocks":
            Filter task_database TO Create urgent_schedule_queue WHERE task.priority_level == "REQUIRED IMMEDIATELY"
            SORT urgent_schedule_queue BY due_date ASCENDING
            
            DISPLAY " GENERATED STUDY BLOCKS FOR NEARING PERIOD "
            IF urgent_schedule_queue IS EMPTY:
                Display "No tasks required in 24 hours. This day's schedule is clear!"
            ELSE:
                FOR EACH urgent_item IN urgent_schedule_queue:
                    DISPLAY "[Dedicated Study Block] Focus on Assignment: " + urgent_item.user_task_title + " (" + urgent_item.user_subject + ")"
                ENDFOR
            ENDIF
        ENDIF
        
    ENDWHILE
Isaiah Antonio G. Tee 8 - Ilang -Ilang
