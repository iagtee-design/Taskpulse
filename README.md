# Taskpulse
Taskpulse is an academic tracker that helps students prioritize activities, flags task due 24 hours and creates optimal study blocks

With many ways of doing activities and tasks in this current world, students are overwhelmed with assessments that could hurt them mentally and drain them physically. Even though their were solutions like manual planners they are tedious to maintain. This problem not just affects highschoolers but can also affect students until college who have many workload. Solving this problem can reduce anxiety and stop bad habits like cramming. 

By the end of the development we are looking to finish these objectives
1. Urgency characterization: Automatically tags activities due in 24 hours as required immediately while other are put into standard levels (low, medium, high)  .
2. Time block: Generates a daily study schedule dedicated to required activities due in a nearing period.
3. Completion Tracking: Provides visual progress that shows the percentage of completed tasks


For our planned features we wish to be able to
1.Characterize tasks based on urgency
2.Automated Time-Block Generator
3.Visual Progress Tracker

Desired Inputes
1. Task Submission Data: The task, the title, the course, the subject and the due date of the task.
2. Completion Checkmark: The student marks a specific task as finished or completed

Desired Outputs
1. Urgent Task visual Indicator: Displays tasks that are due in 24 hours and flags them with urgent text such as Required Immediately.
2. Structured Study Routine: A daily schedule that outlines what needs to be done or reviewed
3. Visual Progress : A display reflecting on academic requirements finished

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
             
              Else IF time_remaining > 24 hours AND time_remaining <= 72 hours:
        SET task.priority_level = "Medium Level"
        
    ELSE:
        SET task.priority_level = "Low Level"
            ENDIF
        ENDFOR
        
        // FEATURE 3 LOGIC: Completion Tracking
        SET total_count = COUNT ALL ITEMS IN task_database
        SET completed_count = COUNT ITEMS IN task_database WHERE task.status == "Completed"
        
        IF total_count > 0:
            CALCULATE visual_percentage = (completed_count / total_count) * 100
        ELSE:
            SET visual_percentage = 0
        ENDIF
        
        DISPLAY visual_percentage ON Progress Bar Interface
        DISPLAY Triage Dashboard (Urgent vs Standard Tasks)
        
        // STEP 3: Handle Planned Input Actions
        IF User selects "Create Task":
            INPUT user_task_title, user_subject, user_due_date
            CREATE new_task_record with status = "Pending"
            SAVE new_task_record TO task_database
            
        ELSE IF User selects "Mark Task Completed":
            UPDATE target_task.status = "Completed"
            
        // FEATURE 2 LOGIC: Study Block Generation
        ELSE IF User selects "Generate Study Blocks":
            FILTER task_database TO CREATE urgent_schedule_queue WHERE task.priority_level == "CRITICAL / REQUIRED IMMEDIATELY"
            SORT urgent_schedule_queue BY due_date ASCENDING
            
            DISPLAY "--- GENERATED STUDY BLOCKS FOR NEARING PERIOD ---"
            IF urgent_schedule_queue IS EMPTY:
                DISPLAY "No urgent tasks due within 24 hours. Your schedule is clear!"
            ELSE:
                FOR EACH urgent_item IN urgent_schedule_queue:
                    DISPLAY "[Dedicated Study Block] Focus on Assignment: " + urgent_item.user_task_title + " (" + urgent_item.user_subject + ")"
                ENDFOR
            ENDIF
        ENDIF
        
    ENDWHILE

END Taskpulse Program
