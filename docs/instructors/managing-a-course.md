# Managing a Course in AI-VERDE

Once your course has been created, you’ll find it listed in your AI-VERDE dashboard.  From here, owners and instructors can update course details, manage members, monitor usage, and design AI-powered learning activities.


## Course Overview
The **Overview tab** is your course’s home base.  
Here, you can:

- **Change the course name and description**  
  - Update the title to match your course.
  - Add a clear description so students know the purpose.  
- **Set start and end dates**  
  - Determines when the course appears on members’ dashboards.  
  - Example: If you set a start date for Sept 1, the course will not appear on students’ dashboards before that date. Students can still sign in to AI-VERDE, but they will not see the course.  
  - After the end date, the course no longer appears on members’ dashboards.  
- **Adjust course activity status**  
  - Switch a course to **Active** when ready for students.  
  - Change to **Inactive** if you want to temporarily hide the course from members’ dashboards without deleting it.  

*A course appears on members’ dashboards only while it is Active and the current date is between its start and end dates.*


## Managing Members
The **Members tab** gives you full control over who is enrolled and what they can do.  

Features:

- **Add new members**  
  - Enter the user’s email address.  
  - Assign them a role at the time of adding.  
- **Remove members**  
  - Select a user and remove them from the course.  
  - Useful if a student drops the class or a TA changes.  
- **Edit member roles**  
  - Roles determine what access each user has (see below).  

### Roles

Each course has one **Owner** and may have any number of **Co-owners**, in addition to members with the **Instructor**, **TA**, or **Student** role.

| Action                                                  | Owner / Co-owner | Instructor | TA  | Student |
| ------------------------------------------------------- | :--------------: | :--------: | :-: | :-----: |
| Edit course name, description, dates, and status        | ✓                | ✓          |     |         |
| Add and remove members                                  | ✓                | ✓          | ✓   |         |
| Change a member’s role                                  | ✓                | ✓          |     |         |
| View course and individual usage                        | ✓                | ✓          | ✓   |         |
| Create, edit, and delete prompts                        | ✓                | ✓          | ✓   |         |
| Use the course chat and course prompts                  | ✓                | ✓          | ✓   | ✓       |
| Get a personal API key                                  | ✓                | ✓          | ✓   | ✓       |

*TAs can add members only with the Student or TA role.*

*Tip: If a student says they can’t see the course, check the Members tab first to make sure they are listed.*  


## Budget and Usage
AI-VERDE resources are tied to a budget, managed in coordination with the CyVerse team.  

- **Budgets are set by CyVerse**  
  - The course budget and any per-student budgets are set by CyVerse staff. To request a change, email **ai-verde-support@cyverse.org**.  
- **What you can do as an owner, instructor, or TA:**  
  - View **individual usage** → see how much each student has consumed.  
  - View **total course usage** → monitor whether the class is approaching budget limits.  
- **Why it matters:**  
  - Helps you plan assignments around available resources.  
  - Identifies students who may need guidance if their usage is unusually high.  



## AI Prompts and Content
The **Prompts feature** lets instructors and TAs design and share structured prompts for AI activities.  

How to use it:

1. Go to the **Prompts** tab.
2. Write a prompt (e.g., “Summarize today’s lecture into 5 key points”) and save it.
3. Every member of the course can see and use the prompt as soon as it is saved.

*This feature helps standardize assignments and ensures all students are working from the same AI instructions.*  



## API Keys and Integrations
Instructors can extend AI-VERDE beyond the platform using API keys.  

- **Generate API keys**  
  - Useful for advanced workflows, automation, or integrating AI-VERDE with other systems. See the [AI-VERDE API](../api/index.md) documentation.  
- **Why this matters:**  
  - Keeps AI-VERDE flexible, fitting into your department’s existing tools rather than operating as an isolated system.  


## Troubleshooting While Managing
- **Course doesn’t show up?** → Confirm with support that your course was created, that its status is Active, and that today is between its start and end dates.  
- **A student can’t see the course?** → Verify they are listed under Members. If not, add them. Also check the course status and dates.  
- **Budget concerns?** → Email **ai-verde-support@cyverse.org** to review or request an adjustment.  
- **Prompt not working as expected?** → Double-check the prompt’s wording and edit it in the Prompts tab; changes are visible to members immediately.  
