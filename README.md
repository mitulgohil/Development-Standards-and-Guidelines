# Table of Contents
1. [Objective](#objective)
2. [Development Process](#development-process)
3. [Coding Standards](#coding-standards)
4. [Profiling](#profiling)
5. [JS Common Mistakes](js-common-mistakes)
6. [Test Cases](#test-cases)
7. [Code Review](#code-review)
8. [Code Repository](#code-repository)
9. [Deployment](#deployment)
10. [Continuous Integration](#continuous-integration)
11. [Tools and Technologies](#tools-and-technologies)
12. [Documentations](#documentations)
# Objective
It is important to standardize on the development processes to be followed on a project so that all team members adhere to the same practices enhancing the maintainability of the project. Here we are going to define our development process and coding standards. Coding standards helps improve the code readability, quality and maintainability. 
# Development Process
As a practice, we use agile software development processes. Agile software development is a people-oriented, collaborative development approach with the flexibility to respond quickly to changes. Our development process includes SCRUM (project management framework), Feature-Driven development(FDD)[FDD is a client-centric and architecture-centric process] and Test-Driven development(TDD) [TDD which combines test-first development, Where you write a test cases before you write just enough production code to fulfill that test and refactoring].
### Sprint Planning & Tracking
All the features and issues/bugs are listed in a single place. We use pivotal-tracker to maintain our stories(feature list). You have to make sure that the story should be present in pivotal-tacker, before you start working on any feature. If not then first add a story and then start working on it.
 
 - **Following is the pivotal workflow we follow:**
  
  1. PRE: Ensure you have a story in pivotal for anything you are working on. Also, put in an estimate in a number of points before you start.
  2. START: Mark the story as `Started` in pivotal, create a branch from the development branch feature-<pivotal_id>, push the empty branch to Gitlab/Github.
  3. EXECUTION: Make regular commits to the feature branch with adequate comments, keep posting updates to pivotal.
  4. FINISH: Make final commits to the feature branch perform unit tests, once satisfied create a pull request and assign a peer developer to review your code and mark the story as `Finished`.
  5. DELIVER: Once peer approves the pull request Merge the pull request into Development branch and deploy to Test Environment or make a Test Build in the case of mobile apps.  Test the feature for any integration issues with the Development branch on the Test Environment / App and if all is well, mark the story as `Delivered`.
  6. ACCEPT / REJECT: Business owner marks the story as `Accepted` or `Rejected` as per their satisfaction

# Coding Standards
Coding standards are guidelines for code style and documentation. We need to write code that minimizes the time it would take someone else to understand it. This document helps a developer to write a well-structured code in a uniform manner. Instead of each developer coding in their own preferred style.

### Indentation & Spacing
A consistent use of indentation makes the code more readable, and easy to debug, easier to understand, easier to modify, easier to maintain and easier to enhance.
 
  - Use soft tabs with a four space indent.
  - Use spaces around operators, after commas, colons and semicolons, around { and before }.
  - Never leave trailing whitespace.
  - End each file with a newline.
  
### Naming Conventions
It is important that complete project must follow the same naming conventions. It makes developer and others(reviewers) life easier.
 
 - **Directory and File name:** The name of the file should represent its role. The name should always be in lowercase and we need to use underscore as a word separator.
``` ruby
- Directory
    #bad
        launch_module/
    #good
        login/
        authentication/

- File
    #bad
        launchpage.component.ts
    #good
        login.component.ts
        authentication.component.ts
```
 - **Functions:** Functions name should also be descriptive. We don't want to write functions called things like "stristr()". We don’t want to keep function name to be too long or too short. It has to be balanced by a little bit of common sense and it should be in camelCase.
``` ruby
    #bad
        camtotal()
    #good
        campaignTotal()
```
For, forEach or any of the loop iterator name should be meaningful it should not like i,j,n etc. Any function should not have more then 20 lines of code. If logics are too big then break it into small functions. Don't write multiple logics in a single function. Funcion should not return multiple things.
    
 - **Variables:** Variable names should be in camelCase, Names should be self-explanatory, but concise. We don't want huge sentences as our variable names, but typing an extra couple of characters is always better than wondering what exactly a certain variable is for. Following is the example.
``` ruby
    # Incorrect 
        @currentuser
        u = User.where(id: 1).first  # avoid short names
    # Correct
        @currentUser 
        user = User.where(id: 1).first
```
    
 - **Class and Modules:** Class and Modules name should be descriptive and must follow the language conventions. 
For example in ruby, classes and modules name written in CamelCase and Keep acronyms like HTTP, RFC, XML in uppercase.
While describing any class keep in mind that It should not fulfill multiple purposes. In simple words, it should follow single responsibility principle.
### Functional programming
Its a style of programming where you focus on transforming data through the use of small expressions that ideally don’t contain side effects. It will alway return the same result. This is achieved by immutable data typical of a functional language.
Function should be as small as possible.

``` ruby
var triple = function(value){
    return value * 3
}
var calculate = triple;
calculate(3)
```

``` ruby
var animals = [
    {name:'Sunny', species:'rabbit'},
    {name:'Tiger', species:'dog'},
    {name:'Alex', species:'dog'},
    {name:'Jimmy', species:'fish'}
]
var dog = animals.filter(function(animal){
    return animal.species === 'dog'
})
``` 
``` ruby

var animals = [
        {name:'Sunny', species:'rabbit'},
        {name:'Tiger', species:'dog'},
        {name:'Alex', species:'dog'},
        {name:'Jimmy', species:'fish'}
    ]
var names = animals.map(function(animal){
    return animal.name
})
```
### Documentation & Comments
We don't want you to write comments on your own code. Instead, we want you to write a code in a way that, It do not need any substitute(i.e. comment) to explain. We recommend to write self-documenting code (It  follow naming conventions and structured programming conventions that enable use of the system without prior specific knowledge)
> Good code is like a good joke: it needs no explanation. 
> -[Russ Olsen](http://eloquentruby.com/blog/2011/03/07/good-code-and-good-jokes/)
Don't write comments doesn't mean we don't like documentation. We believe in API documentation and we want each API should be properly documented with request, response parameters and exceptions.
### Logs
Some time mysterious crash happen in our application that we can’t reproduce then we have to ask user for a screenshot of the page JavaScript console. It’s happened to us too many times.
Log-Driven Development solves all of these problems. The idea is that by driving the business logic of an app via logs, we are able to automatically capture information that helps us reproduce bugs, resolve user issues, and understand user behavior without additional work.

`ColdFusion` provides several logs for different server functions. It leverages the Apache `Log4j` libraries for customized logging. It also provides logging tags to assist in application debugging. We can generate many types of log files. Like application.log, exception.log, server.log etc.

We should use log rotation utility. Log rotation refers to the practice of archiving an application’s current log, starting a fresh log, and deleting older logs.

### Error Handling
We should handle exceptions and errors to prevent app crashes. Handler function should be global. We should use try / catch / finally that can generate an exception. In catch blocks, always order exceptions from the most specific to the least specific. Use a finally block to clean up resources, whether you can recover or not. For some conditions that are likely to occur but might trigger an exception, consider handling them in a way that will avoid the exception. 

E.g. If you try to close a connection that is already closed, you'll get an InvalidOperationException. You can avoid that by using an if statement to check the connection state before trying to close it.
Error handling code sould be specific to some functionality. It should not for all functionality.

Angular defines an ErrorHandler class that will allow us to override it and handle custom logic. [Angular error handler](https://angular.io/api/core/ErrorHandler)
### Security mindset
Security is one of the most important part of our applications.

- **Preventing XSS:**
The cross-side scripting (XSS) is one of the more usual vulnerabilities we can have in our web application. They allow potential attackers to inject malicious scripts in pages viewed by end-users.
But if we follow the common architecture in our projects that separates the HTML templates from the JS controllers, most of our work is done! Due to the fact the majority of the frameworks we use nowadays for rendering our templates escape the HTML code.
We should create Microservices.

- **Avoiding reverse tabnabbing:**
Reverse tabnabbing is a phishing attack, where an attacker replaces a page tab with a malicious document by using window.opener.location.assign().
But we can avoid this just simply using noopener and noreferrer in the rel attributes of a link.
By adding the noopener keyword, the new / other page cannot access the window object via window.opener. And the noreferrer keyword tells the browser not to collect HTTP referrer information when the link is followed.

- **Content security policy:**
Include a header in the HTTP responses for restricting the domains that can load content in our application. 
``` ruby
Content-Security-Policy: script-src 'self' static.p41.com
```
This policy will allow to run only the scripts hosted in the same server as the application (self) and the ones hosted in static.p41.com. Hence, it will mitigate potential XSS and data injection attacks performed by scripts hosted in external domains.
Minimize the use of global variables. This includes all data types, objects, and functions. Global variables and functions can be overwritten by other scripts.Use local variables instead.

- **SQL Injection:**
1. SQL injection usually occurs when you ask a user for input, like their username/userid, and instead of a name/id, the user give you an SQL statement that you will unknowingly run on your database.
``` ruby
txtuserId = getRequestString("UserId");

txtSQL = "SELECT * FROM Users WHERE UserId = " + txtuserId;
```
In above example if there is nothing to prevent a user from entering wrong input, the user can access all the user data using:
``` ruby
userId = 105 OR 1=1
    
then, the SQL statement will look like this:

SELECT * FROM Users WHERE UserId = 105 OR 1=1;
```
The SQL above is valid and will return ALL rows from the "Users" table, since OR 1=1 is always TRUE.
2. SQL Injection based on "=" is alwas true
``` ruby
uName = getRequestString("username");

uPass = getRequestString("userpassword");

SQL = 'SELECT * FROM Users WHERE Name ="' + uName + '" AND Pass ="' + uPass + '"'
```
If user enter wrong input. Like:
``` ruby
uName = " or ""="

uPass = " or ""="

SQL = SELECT * FROM Users WHERE Name ="" or ""="" AND Pass ="" or ""=""
```
The SQL above is valid and will return all rows from the "Users" table, since OR ""="" is always TRUE.
3. SQL Injection based on batched SQL statements.
A batch of SQL statements is a group of two or more SQL statements, separated by semicolons.
``` ruby
txtUserId = getRequestString("UserId");

txtSQL = "SELECT * FROM Users WHERE UserId = " + txtUserId;
```
The SQL above is valid. If user enter wrong input. Like:

``` ruby
txtUserId = 105; DROP TABLE Suppliers;

SELECT * FROM Users WHERE UserId = 105; DROP TABLE Suppliers;
```
To protect a web site from SQL injection, we can use SQL parameters.
SQL parameters are values that are added to an SQL query at execution time, in a controlled manner.
E.g.
``` ruby
txtUserId = getRequestString("UserId");

txtSQL = "SELECT * FROM Users WHERE UserId = @0";

db.Execute(txtSQL,txtUserId);
```
Parameters are represented in the SQL statement by a @ marker.
 
# Profiling
Profiling is a form of dynamic program analysis that measures memory, time complexity of a program, the usage of particular instructions or the frequency and duration of function calls. Profiler gathers a lot of data for each request. Use this data to check the number of database calls, the time spent in the framework, etc.

- **Flat profiler:**
Flat profilers compute the average call times, from the calls, and do not break down the call times based on the callee or the context.

- **Call-graph profiler:**
Call graph profilers show the call times, and frequencies of the functions, and also the call-chains involved based on the callee.

- **Input-sensitive profiler:**
Input-sensitive profilers add a further dimension to flat or call-graph profilers by relating performance measures to features of the input workloads, such as input size or input values. They generate charts that characterize how an application's performance scales as a function of its input.


# JS Common Mistakes

 - **Accidentally Using the Assignment Operator:**

JavaScript programs may generate unexpected results if a programmer accidentally uses an assignment operator (=), instead of a comparison operator (==) in an if statement.
``` ruby
var x = 0;
if(x==10)

Above statement returns false but if developer create any mistake like:

var x = 0;
if(x=10)

Above statement returns true.
```
- **Expecting Loose Comparison:**

In regular comparison, data type does not matter.
``` ruby
var x = 10;
var y = "10";
if (x == y)

Above statement returns true.
```
In strict comparison, data type does matter. 
``` ruby
var x = 10;
var y = "10";
if (x === y)

Above statement returns false.
```
- **Confusing Addition & Concatenation:**
Addition is about adding numbers.
Concatenation is about adding strings.
In JavaScript both operations use the same + operator.
Because of this, adding a number as a number will produce a different result from adding a number as a string:
``` ruby
var x = 10 + 5;          
// the result in x is 15

var x = 10 + "5";
// the result in x is "105"
    
var x = 5 - "5";
// the result in x is 0

var x = 5 + "5" - 5;
// the result in x = "50"; 
```
- **Undefined is Not Null:**
With JavaScript, null is for objects, undefined is for variables, properties, and methods.
To be null, an object has to be defined, otherwise it will be undefined.
If you want to test if an object exists, this will throw an error if the object is undefined:
``` ruby
Incorrect
if (myObj !== null && typeof myObj !== "undefined") 
Correct
if (typeof myObj !== "undefined" && myObj !== null)
```

# Test Cases
Writing test cases is a valuable practice it helps in scaling a project in good shape. Test cases also give us the confidence that our application/code is bug-free. 
We should write tast cases before start coding. We majorly focus on two type of tests.

 - **Unit Tests:** It should cover all the integrated model methods and controller actions. Unit testing is a software testing method where individual units or components of a software are tested. A unit is the smallest testable part of software. It usually has one or a few inputs and usually a single output.
 
 - **Integration Tests:** It should cover the complete flow of each individual API.
 
 - **E2E testing:** End to end testing is a technique used to test whether the flow of an application right from start to finish is behaving as expected. The entire application is tested for critical functionalities such as database, interfaces, communication with the other systems. We can use `Protractor` for E2E testing.
We will use `rspec` to write test cases. We will also use `faker` and `factory_girl` to create dummy test data for test cases.
# Code Review
This is one of the important parts of our development process. We will not allow even a single line of code to be shipped without it being reviewed by someone else. Once developer is code complete and all his test cases have passed, he can submit code for review.
Following are the steps involved in code review process.

 - Commit & push code to the respective feature branch.
 - Create PR(Pull Request) from feature branch to merge into the development branch.
 - Assign the PR to the reviewer and make him/her a reviewer of the PR.
 - Code review: The reviewer and developer should exchange comments and notes on the PR until both the reviewer and developer are satisfied with the feature implementation.
 - Merge PR to the development branch.
 
Once reviewer completes the code review, the developer needs to merge the PR into the development branch. Code reviewer is equally responsible for the code he reviewed.
# Code Repository
We will use git as a source control and follow the feature branch workflow.
Following is the structure of our git branching.

 - **Master:**
This is our main branch. We will do all our production deployment through the master branch. We will not allow anyone to commit directly to the master branch. We will only allow merge of `staging` branch to `master`.

 - **Staging:**
This branch is created from the master branch. Once the feature branch is verified on QA environment. We can merge the feature branch into the staging branch. Staging branch can be directly merged into the master branch. Similar to the master branch, we will not allow any direct commit to the staging branch.

 - **Development:**
This branch is created from the master branch. We will deploy to the QA environment through the development branch. We will merge our feature branches into this branch.

 - **Feature branch:**
This branch will be created from the `master` branch. We can create this for any feature/release/bug. Branch name must follow the conventions. Branch name start with feature/bug then followed by the feature/bug title and then followed by story number(pivotal ticket id).
eg. `feature/user-login-123456` or `bug/user-login-123456`

# Deployment
We will deploy our code on three different environments. The frequency of deployment is based upon sprint plan and development.
 
 - **QA(Test)**
 This environment is use for QA and demo purpose. We will use this environment for testing an implemented feature.
We will use `Heroku` as a QA environment. Once `feature` branch is merged into the `development` branch, we will deploy development branch to QA environment.
 
 - **Staging**
 This environment is meant to have everything as closely replicated to the production environment as possible, so that we can maximize our chances to deliver error free code to production.
 Once a feature is verified on QA environment, we will merge our `feature` branch with `staging` branch.
 
 - **Production**
 Once a feature is verified on staging environment, we will merge our `staging` branch with `master` branch and the master branch will be deployed to production.

# Continuous Integration
Continuous integration(CI) is an integral part of an agile software development setup. Sprint after sprint, teams strive to "not break the build" while delivering incremental features. 
To achieve these objectives, continuous integration relies on the following principles. 

 - Maintain a code repository.
 - Automate the build.
 - Make the build self-testing.
 - Every commit (to baseline) should be built.
 - Test in a clone of the production environment.

We will use `circleci` as a continous integration tool. We will Integrate our git repository to `circleci`, so that whenever we create and merge a PR. It will run all the test cases and attach test execution report back to the associated PR.

# Tools and Technologies
We are going to use different tools and technologies for the different part of an application, which helps us to build a robust application.
We will have separate code repository for backend and frontend.
### Backend with ROR
Ruby as a language with `Rails API` framework. We will create all our API’s in ROR.
#### Gems

Following are the list of common gems which will be our helping hand. This list will gradually increase as per the development requirements.

- rails
- mysql2
- devise
- jbuilder
- sass-rails
- uglifier
- angular_rails_csrf
- dotenv-rails
- pry
- rspec
- faker
- factory_girl_rails

#### Directory Structure
Following will be the standard structure of our application, and the components should be organized in the following manner only.
>app/
>
>---- controllers/
>
>-------- application_controller.rb
>
>-------- concerns/
>
>---- helpers/
>
>-------- application_helper.rb
>
>---- mailers/
>
>---- models/
>
>-------- concerns/
>
>---- views/
>
>-------- layouts/
>
>------------ application.html.erb
>
> bin/
> 
>---- bundle/
>
>---- rails/
>
>---- rake/
>
>---- setup/
>
>---- spring/
>
> config/
> 
>---- application.rb
>
>---- boot.rb
>
>---- database.yml
>
>---- routes.rb
>
>---- secrets.yml
>
>---- environment.rb
>
>---- environments/
>
>-------- development.rb
>
>-------- production.rb
>
>-------- test.rb
>
>---- initializers/
>
>---- locales/
>
>-------- en.yml
>
> config.ru
> 
> db/
> 
>---- seeds.rb
> Gemfile
> 
> Gemfile.lock
> 
> lib/
> 
>---- assets
>
>---- tasks
>
> log/
> 
> public/
> 
> Rakefile
> 
> README.rdoc
> 
> test/
> 
>---- controllers/
>
>---- fixtures/
>
>---- helpers/
>
>---- integration/
>
>---- mailers/
>
>---- models/
>
>---- test_helper.rb
>
> tmp/

### Front-end with Angular
AngularJS `(1.x)` and Angular `(2 & 4.x)` both are different. Whole concept of application structure has changed in Angular. Angular is adopting component-based UI. Angular is basically based on TypeScript which is actually an extension of ECMAScript6.0. Angular is much faster then AngularJS.
#### Angular Dependency

To start with Angular development we need to setup our development environment.

 1. Install [Node.js](https://nodejs.org/en/) if it is not install in our system.
 2. Install Angular/CLI using `npm install -g @angular/cli`.

#### Start Development Using Angular CLI

To creating new angular project use:
  ``` ruby
  ng new project-name
  ```
  To run project use:
  ``` ruby
  cd project-name
  ng serve
  ```

`ng serve` use for dev server.

Navigate to http://localhost:4200/. The app will automatically reload if you change any of the source files.

`ng build --prod` use for production. The build artifacts will be stored in the `dist/` directory.

To create new component | module | service | pipe use:
``` ruby
ng g component component-name
ng g module module-name
ng g service service-name
ng g pipe pipe-name
```
#### Directory Structure

>
>      app/
>
>      app.component.html
>      app.component.ts
>      app.component.scss
>      app.component.spec.ts
>      app.module.ts --> (app module is the root module of the application and it contains app module component)
>      app-routing.module.ts --> (app-routing module contains route of app module)
>      home/ --> (Home directory contains all component of home module)
>           home.component.html
>           home.component.ts
>           home.component.scss
>           home.component.spec.ts
>           home.module.ts --> (home module contail home module component)
>           home-routing.module.ts --> (home-routing contains route of home module)
>           master-view/ -->(master-view directory contains all files of master-view component)
>                       master-view.component.html
>                       master-view.component.ts
>                       master-view.component.scss
>                       master-view.component.spec.ts
>           detail-view/
>           campaign-analysis/
>           dashboard/
>           home-services/
>                        home-service.service.ts --> (home-service contains api call functions of home modules components)
>                        home-service.service.spec.ts
>                        http-call.service.spec.ts
>                        http-call.service.ts --> (http-call service contains http methos - GET,POST,PUT,DELETE)
>
>      assets/ --> (directory contains all external img,js,fonts,css/scss)
>
>      index.html
>

Every module shoud have their own route, services and components. Reusable component should be seperate component. Reusable logics should be in service. So we can share it with all component.

# Documentations

### API Documentation
In order to create a rest API and API documentation, We will use `swagger` to create an API document.
Following is the process of API creation and documentation.

- Create API stub.
- Write test cases using RSpec.
- Generate swagger API doc. We will use `rswag` gem for swagger integration.

### Readme file
It is often the first thing a visitor will see when visiting your repository and it must include following sections.

- What the project does.
- How to use it.
- Installation instructions.
- Dependancies
- Configuration instructions.
- Version information.
- License information.

[This](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2) is a good template for a README file.
