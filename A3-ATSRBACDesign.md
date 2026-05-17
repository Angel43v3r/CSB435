# Assignment 3: ATS Role-Based Access Control Design

## Part 1: Roles
A list of roles with brief descriptions

- **Recruiter** - User that manages recruiting operations and job candidates
- **Candidate** - User applying for jobs
- **Hiring Manager** - User who makes hiring decisions
- **Interviewer** - User who conduct interviews for the job application
- **HR** - User who oversee the job offers, requisition budget, and any HR related stuff.
- **Third Party** - Users that are third party recruiters
- **Admin** - Administrator of the app


## Part 2: Permissions
A list of permissions with brief descriptions

| **PERMISSIONS**         | **DESCRIPTIONS**                                                               |**ROLE**                                                |
|-------------------------|--------------------------------------------------------------------------------|--------------------------------------------------------|
| Manage Requisition      | Create, edit, publish, or delete a new job requisition                         | Admin, Recruiter, Hiring Manager, and HR               |
| Manage Candidate        | Send rejection letters, conduct reference checks, and schedule interview to candidates | Recruiter and HR                               |
| Manage Application      | Allow candidate to Withdraw or submit a job application to an open position    | Candidate                                              |
| Feedback                | Add notes or comments about a candidate (e.g. after performing an interview)   | Recruiter, Hiring Manager, HR, Interviewer, Third Party|
| View Candidate          | Access candidate contact information                                           | Recruiter, Hiring Manager, HR, Third Party             |
| Approve Budget          | Approve a job requisition budget                                               | HR                                                     |
| Extend Offer            | Extend a formal job offer                                                      | HR                                                     |
| Candidate Status        | Update a candidate's status (e.g. "Phone Screen", "Rejected", "Offer Extended")| Recruiter, Hiring Manager, HR, Third Party             |
| Application Status      | View their own application status                                              | Candidate                                              |
| View All Application    | View all applications for a specific job requisition                           | Recruiter, Hiring Manager, and HR                      |
| Archive Requisition     | Archive old requisitions                                                       | Admin, Recruiter, HR                                   |
| Integrate ATS           | Integrate the ATS with a job board (e.g. Indeed) for API-based job posting     | Admin                                                  |
| Manage users            | Add / Remove users from the ATS                                                | Admin                                                  |
| Delete Candidate        | Delete candidate data per privacy regulations                                  | HR, Admin                                              |
| View Report             | Run reports on hiring metrics and pipeline statistics                          | Recruiter, Hiring Manager, HR, Admin                   |
| Edit Profile            | Edit Profile Information such as password, picture, about, contact, and name   | ALL                                                    |
| Add resume              | Allow candidate to upload or update a resume on their profile                  | Candidate                                              |
| Search jobs             | Browse and search available job openings within the ATS platform               | ALL                                                    |
| View Assigned Interview | View candidate info and resume without sensitive info such as PII              | Interviewer, Hiring Manager                            |

## Part 3: Role-Permission Matrix
A clear mapping showing which permissions belong to which roles
| **PERMISSIONS**         | **ROLE**                                                |
|-------------------------|---------------------------------------------------------|
| Manage Requisition      | Admin, Recruiter, Hiring Manager, and HR                |
| Manage Candidate        | Recruiter and HR                                        |
| Manage Application      | Candidate                                               |
| Feedback                | Recruiter, Hiring Manager, HR, Interviewer, Third Party |
| View Candidate          | Recruiter, Hiring Manager, HR, Third Party              |
| Approve Budget          | HR                                                      |
| Extend Offer            | HR                                                      |
| Candidate Status        | Recruiter, Hiring Manager, HR, Third Party              |
| Application Status      | Candidate                                               |
| View All Application    | Recruiter, Hiring Manager, and HR                       |
| Archive Requisition     | Admin, Recruiter, HR                                    |
| Integrate ATS           | Admin                                                   |
| Manage users            | Admin                                                   |
| Delete Candidate        | HR, Admin                                               |
| View Report             | Recruiter, Hiring Manager, HR, Admin                    |
| Edit Profile            | ALL                                                     |
| Add resume              | Candidate                                               |
| Search jobs             | ALL                                                     |
| View Assigned Interview | Interviewer, Hiring Mananger                            |


## Part 4: Rationale
Brief explanations of key design decisions

### Separation of duties
Some sensitive operations are split between roles and I combined some permission that overlap to a single permission control to simplify it.
- **Candidate** should only have access to their job application, profile, to search job, and application status, but should not have access to other candidates or the management of job requisition.
- **HR** are responsible for requisition budget, approving offer, view candidate, and extending offer to the candidate but they should not be doing the interview.
- **Recruiter** manages recruiting and the job candidates but they shouldn't be able to access the HR specific stuff or doing the interview.
- **Hiring manager** makes hiring decisions and can view candidates, but they don't manage the job requisition or extend offers.
- **Interviewer** conduct interviews for the job application so they should only have limited view of the candidate info and resume, and view assigned interview. Other than those, they shouldn't have access to anything else.
- **Third Party** are third party recruiters so they should only see what job they are sourced to.
- **Admin** does Administrator of the app so they should have access to the system and user management but they shouldn't interfere with the hiring process.

### Principle of least privilege: Users should have only the permissions necessary to do their job
Users should only have the necessary permission to do their job, so I added separate permission for specific permission that only some candidate can do. Even though I have permissions like `Manage Candidate`, deleting candidate data per privacy regulation should only be handled by HR and the Admin so I made a separate permission `Delete Candidate`. I made sure that each role is granted only the minimum permission required to reduce any misuse or security risks. 

### Data sensitivity
Sensitive data like PII, salary info, and interview results should be restricted to only roles with permissions to have those info. For example, `View Assigned Interview` allows the interviewer and hiring manager to view candidate information and resume without the sensitive info like PII.

### External vs internal users
Each role type have different needs so each have different permission and access so role-based access is implemented on my design. For example third party recruiters can only access to requisition assigned to them so they should only have access to those requisition and the candidates that applied to those requisition. Candidates also have limited access and can only manage their own applications and profile. This helps protect sensitive information and data.

## Part 5: Unnecessary
List of things you decided are not necessary (if appropriate)
- I didn't add too many specific roles for each permission than what is necessary like `Budget Approver`. We don't want to make it too complex that its frustrating or confusing, we want to make it simple enough to see a distinct separation for each roles and permission. Roles like `Budget Approver` is unnecessary because thats handled by HR. 

## Part 6: Necessary
List of things you would include/flesh out if you had more than 2 hours (if appropriate)
- If I have more time then I would add more specific attributes to each role or permission. For example, I added View Assigned Interview which only shows interviewers and hiring manager the candidate information and resume with limited information. I could probably also add filters, like for searching jobs, add if they are looking for part time, full time, type of industry, job role type, etc. 


## Part 7: Weakness
Any areas you think are weak in your model, or you're less confident about
- There are some permissions that I made broad like `Manage Candidate`, this simplified the permission but it can also maybe mislead some of the users to have more access like having more access in handling the candidate, but the permissiono scope only covers `send rejection letters`, `conduct reference checks`, and `schedule interview to candidates`. 
