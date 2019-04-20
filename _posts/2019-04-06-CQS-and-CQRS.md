---
layout: post
title: "CQS and CQRS"
date: 2019-04-06
---

Of recently, usage of these two terms is increasing among programming. So what does these abbreviation stands for: 

CQS - Command Query Separation 

CQRS - Command Query Responsibility Segregation 

Doesn't both of these kind of means the same thing? Well, Yes and No.

At the base conceptual level they are indeed the same thing. They represent the separation of Queries and Commands. And, what are these Queries and Commands. 

Queries - These are the functions that have no side effect i.e. Queries must return a result and they should not update any value of the system. After execution of query the 'state of system' is same as before execution of the query.  

Command - These are the functions that have side effect. They update values i.e. they make modification in the state of system, either by updating Object or updating database or any other form of storage.  

CQS is a approach which states that Queries and Commands should be separate from each other. Or in other words it means that functions having no 'side-effect' should be separated out from one having 'side-effect'. An example of this can be following code snippet.

`public interface IEmployeeService
{
    Employee GetEmployeeById(long id);
    IEnumerable GetAllEmployee();
    void CreateEmployee(string firstName, string lastName, DateTime dateOfBirth);
    void UpdateEmployee(string firstName, string lastName);
}`

Here, we have two queries, GetEmployeeById and GetAllEmployee. Also, there are two commands namely CreateEmployee and UpdateEmployee. It is easy to see here that both of our queries are not meant to affect the 'state of system', while the commands on completion of their execution will bring about a change in values of database. Why is this separation required. Suppose you start working on an existing project. In this you have a method name

`GetEmployeeByIdOrName(int id, string name)` and while running the code you find out that method `GetEmployeeByIdOrName` not just provide you with an Employee object but also updates the Name of Employee for given id if search was not successful on provided 'name'.

Hence, there need to be a clear distinction on what the method would do. If the method name and return type suggests that it is querying the system, then it should only do that. 

And what is CQRS. CQRS is same as CQS in terms of command and query separation. It too states that both these functionality should be separate from each other interference. But, CQRS is an advancement over CQS. Wherein CQS you can make use of same models for both querying and updating, CQRS suggest using separate models for query and command. CQRS even suggests that queries and commands should we entirely separate flows. This implies creation of separate models, separate query and command handlers,  even to extent of having separate workflow for each BoundedContext. This approach also makes it useful where we have separate databases for reading and writing OR even separate database for different BoundedContext. 

Separation of models in CQRS helps in having cleaner Models. Read/query models only contain properties that are required for display or as per API requirement, while command model will only contain properties that will be used to update the 'state of the system' i.e. only required properties that need to create/update record in database. Separate models also help is reading and updating data from different database. Query can call NoSql to fetch the records and Command can insert data into RDBMS. 

It is suggested to use CQS approach for all classes/Entities in the application. This helps in adhering to the SOLID principles. While CQRS should only be applied where it is required. Following multi-model approach of CQRS can be cumbersome for small applications. Also, an application may have multiple BoundedContext and not all of them need to use CQRS. It should therefore be applied on BoundedContexts which would really benefit from the approach.