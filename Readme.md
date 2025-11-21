Developed this app during my previous employment to help train new joinees and interns for basic OWASP Vulnurabilities

Damn Vulnerable Web Application
=========
This is a vulnerable app written for training purposes. This app contains traning for:
1. SQL Injection
2. Cross Site Scripting
3. IDOR

STEPS TO RUN THE APP
=====================
1. To run this app, clone the repo onto your local machine
2. Open terminal and install virtualenv for python using this Command
        </n><code>pip install virtualenv</code>
3. Now open terminal in the FlaskApp Folder and start your virtual env using this command.
         <code>source env/bin/activate</code>
4. Run the app.py file using this command 
          <code>python app.py</code>
5. The application will run on your localhost, open any browser and go to the localhost IP to start using the app
6. Deactivate the virtual env once you close the app using this command
          <code>deactivate</code>
      
Mitigation
=====================

SQL Injection
--------------
Primary Defenses¶

Option 1: Use of Prepared Statements (with Parameterized Queries)
Option 2: Use of Properly Constructed Stored Procedures
Option 3: Allow-list Input Validation
Option 4: STRONGLY DISCOURAGED: Escaping All User Supplied Input

In the safe Java example below, if an attacker were to enter the userID as tom' or '1'='1, the parameterized query would look for a username that literally matches the entire string tom' or '1'='1. Thus, the database would be protected against injections of malicious SQL code.

The following code example uses a PreparedStatement, Java's implementation of a parameterized query, to execute the same database query.

```{
// This should REALLY be validated too
String custname = request.getParameter("customerName");
// Perform input validation to detect attacks
String query = "SELECT account_balance FROM user_data WHERE user_name = ? ";
PreparedStatement pstmt = connection.prepareStatement( query );
pstmt.setString( 1, custname);
ResultSet results = pstmt.executeQuery( );
```

Cross Site Scripting
---------------------
When you need to safely display data exactly as a user types it in, output encoding is recommended. Variables should not be interpreted as code instead of text.
when you wish to display data as the user typed it in, start with your framework’s default output encoding protection. Automatic encoding and escaping functions are built into most frameworks.

If you’re not using a framework or need to cover gaps in the framework then you should use an output encoding library. Each variable used in the user interface should be passed through an output encoding function. A list of output encoding libraries is included in the appendix.

There are many different output encoding methods because browsers parse HTML, JS, URLs, and CSS differently. Using the wrong encoding method may introduce weaknesses or harm the functionality of your application.

IDOR
---------
To mitigate IDOR, implement access control checks for each object that users try to access. Web frameworks often provide ways to facilitate this. Additionally, use complex identifiers as a defense-in-depth measure, but remember that access control is crucial even with these identifiers.

Avoid exposing identifiers in URLs and POST bodies if possible. Instead, determine the currently authenticated user from session information. When using multi-step flows, pass identifiers in the session to prevent tampering.

