# System design preparation notes

## System design approach

Discuss how to approach system design interview and make a template to follow in the interview. Came up with this approach after referring to muliple resources.

### 1. Understand the goal of the app [1 min]
 Try to understand what the interviewer is asking us to design and ask generic questions about the application we are trying to build and the end users of the application. This understanding should help us in gathering the requirements of the system. 
 
 ### 2. Requirements clarifications
 End goal is to clarify the function and non-function requirements
 #### Non-function requirements
  |  Users/Customers| Scale| Perforamnce of the sytem |
  |-----------------|-------|--------------------------|
  | 1. Use cases of the system                      |How much data is queried per request| What is expected write to read delay |         
  | 2. How the sytem will be used (Usage patterns)  | How much data is processed/ written to the read quiries     | What is expected p99 latency for the read queries |                                                                      
  | 3. How many will use the system                 |  Can there be spike in the traffic| |
  | 4. who will use the system                      | How many read/wrire queries                 | |     


