---
title: What is a NoSQL Injection Attack?
date: Mon, 13 Sep 2021 14:00:00 +0000
---
Before we talk about a NoSQL Injection, let's see what NoSQL is. NoSQL databases are precisely the opposite of what SQL databases are. NoSQL means no structured query language. The schema that is used in a NoSQL database is very dynamic and is highly scalable. One can add different fields dynamically without affecting the rest of the data. One example of NoSQL data is MongoDB. So what are NoSQL injections, and how do they work?NoSQL injections are when dynamic database queries can be used and manipulated by supplying an active and unexpected user input such as Binary and Query Object Types. If you are expecting a string as an input, it needs to be whitelisted. A popular NoSQL database is MongoDB. MongoDB's Query Objects can be used to circumvent server-side validation by using reconnaissance of client-side javascript to find API endpoints and payloads associated with them, as well as the using of object query injections. Query Objects can be leveraged to validate username/password, and they contain some level of logic where if more than one field is specified, it could signal to an AND query. 

db.accounts.find({username: "username_value", password: "password_value"})

Validation Issues arise when issues within an underlying library allow a malicious attacker to inject "username_value" and "password_value" with random characters. Imagine if unexpected characters are nested within the username_value or the password_value, and it is evaluated to "True." But sometimes, what if there are no issues with the underlying library? The answer is Nested Query Objects. There are other ways to trick or bypass validation operations.

username:"admin", password:"{$exist: True}"

To subvert validation checks, the malicious attacker will try and inject query objects that evaluate True. This checks for a username value in the admin database, and the password validation will be skipped because it will return as valid. In a Post request for URLs, validation checks can be bypassed by performing something similar. 

POST request: username[$eq]=admin&password[$exists]=true

The different types of query operators:Comparison: {$gt: 0}Logical: {$not: " "}Element: {$exists: true}Evaluation: $where <= An evaluation query generally matches documents that satisfy a Javascript Expression. 

db.collection.find({'$where' ⇒ 'this.name === ' + <Inject_EvilINPUT>}) ';

Comment: Through a comment query operator, an attacker can inject an XSS payload inside the comment tag. It can be used to reflect the XSS on server logs, and if an admin looking at them through their browser would potentially be vulnerable to remote code execution functionalities.

db.collection.find({ <query>, $comment: "<script> EVIL code </script>" })

Mitigation tactics against NoSQL injection attack:Make sure that the underlying library is Sanitized.User inputs must match the expected type. For example, if you expect a string, the string should not feature any dynamic value.Always use the least privilege principle when running an application.Always avoid using query operators in user inputs such as where, MapReduce, etc.For additional safety, set javascriptEnabled to False.