# Important
This repository contain no source code, but the next 2 links are the links for the backend and the frontend of the project.

## Links
Backend Github: https://github.com/Teklar223/Shifter-backend

Frontend Github: https://github.com/khsabrina/shifter

You are more than welcome to use Shifter!

# Introduction
Welcome to Shifter. Shifter came as an alternative solution for comapnies and offer a comfortable platform to handle their man power.
Shifter offer many services like team managing, create desired schedules for next week, allowing the employees to fill their preferences and of course to use a scheduling algorithm to create a schedule for next week.

## Motivation
### Scheduling
Scheduling is a well known optimization problem in computer sceince, just like other optimization problems it based on a trade offs - what we want to gain and what we are willing to give away. In case of shift scheduling we have multiple problems we have to deal with in order to create even the most basic schedule:
1. Whether or not we consider the employees preferences.
2. Which is more necessary? to have more full shifts(shifts that have all the needed man power assigned) or to have more active shifts(shifts that have at least one employee assigned to it).
3. Work hours limitation(daily and weekly).
4. Weekly shift count limitations.
5. The need for multiple roles in a single shift.
And some more problems we have to deal with if we want to create a schedule for our team.
The next subject we need to think about is how to deal with different cases in which we cannot make a full schedule as planned from the start, it could happen if not enough employees submit their preferences of specific shifts.
Those are the cases where each of the problems mentioned above will not suppose to matter that much since we cannot complete the scheduling task.

### Team Handling
Control the man power is essential to manage the company. In order to complete multiple goals an owner will need to establish teams and assign a leader to each of them in order to manage the team and then create a team to achieve the wanted goal.

## Features
### Scheduling
#### Next week schedule template
A team leader of an owner can create a template schedule for next week that contains the hours of each shifts and the number of needed employees for each needed roles.
The system will later derive the schedule template into a preferences that the employees can fill.

#### Employee Preferences
As mentioned above, the system will derive the schedule template and create a preferences for the employees in which they can mark whether they can work in that shift or not.

#### Create a schedule
The system offer to use a scheduling algorithm that will explained further later in order to create a schedule based on the schedule template and the employees filled preferences and several constraints that the user can add. For example limit the daily work hours of an employee or limit the weekly work hours of an employee.

## Future features
### Team's tasks management ans analysis
### Team's favorite schedule templates
### Add more constraint types
### Add priorities for employees for new constraints

# Scheduling Algorithm
## Pre Processing
1. Get the schedule template from the DB.
2. Create multiple templates based on the roles
3. Get the team's preferences from the DB.
4. Divide the preferences based on the role.
5. Return the scheduling template and the preferences divided by role and the set of roles.

## Main function
1. Use preprocessing algorithm
2. Create an empty week assignment for next week = A
3. Create the empty dats for the next week D1, D2, ..., Dn*
4. for each role in the role set
  a. Run the scheduling algorithm and recieve an assignment for the role
  b. Add the assignment to A
5. Return A

## Main algorithm

### Advantages
1. The algorithm is simple to understand
2. The algorithm schedule one role at a time and by that solve one of the problems mentioned above.
3. The algorithm will always try to achieve the maximum amount of shift assignments in a way it will not violate any constraint, and by that it will always return the optimal schedule according to the employees preferences, schedule limitations and the needed constraints.
4. The algorithm use both abstraction and Strategy design pattern in a way that each type of constraint is a class that derive from a constraint base class and have an execution function that implemented differently for each constraint. By doing that we can have multiple constraints or multiple types of constraints and execute them without informing the algorithm which kind of constraint applied.
The Strategy desing pattern is the implementation of the execution function of the constraints, each constraint implemented differently and the algorithm will apply a list of constraint by using the execution function.
5. Easy to expand. Furthermore for what we wrote in #4, in order to create new type of constraint, we need to implement it in a new class, update a file of constants and update the parse function of the constraint.

Inputs:
1. Schedule template of specific role
2. list of employees Preferences template of specific role
3. Role dependent constraints.
4. Global constraints.

Output: Assignment for next week specific role

1. Create the shifts dictionary and keys
2. Limit the number of employee in each shift to the maximum allowed.
3. Apply all of the constraints.
4. Maximize the number of shift assignments.
5. Create the output assignment
6. Return the output assignment
