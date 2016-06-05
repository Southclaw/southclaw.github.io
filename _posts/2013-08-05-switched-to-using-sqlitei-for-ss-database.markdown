---
layout:     post
title:      "Switched To Using SQLitei for SS Database"
date:       2013-08-05 10:03:46
categories: reviews
---
I've never liked SQL, at least not in the Pawn language. I find it so awkward to write, you have to declare some huge string, then format it with a bunch of words and data that usually goes off the edge of the screen unless you split it across lines. All the functions are in_lower_case_with_tons_of_underscores which looks so ugly to me!
<!--more-->

I've avoided it as much as possible so far, only using it when necessary and when it can do what files can't. But then SQLitei (SQLite-improved by Slice) came to shine some light on my horrible SQL code! Don't get me wrong, the SQL concept is very powerful and I admire it in general, I just don't like it's implementation in Pawn or other programming languages where I must write the SQL "functions" inside a string to send off by a "query". I'm just so used to regular imperative functions, I'd probably prefer something that actually limits the capability of SQL. But that's where SQLitei comes in, it _does_ use more functions for the SQL features while maintaining that flexibility of putting SQL queries into a string. The feature I love the most is the ability to **prepare** queries in what are referred to as 'statements'. The old way: 
    
    
    new
        query[116],
        DBResult:result,
        numrows;
    
    format(query, sizeof(query), "SELECT kills FROM Users WHERE name = '%s' AND score > '%d' OR deaths < '%d'", name, score, deaths);
    result = db_query(gAccountsDatabase, query);
    numrows = db_num_rows(result);
    
    if(numrows > 0)
    {
        for(new i; i < numrows; i++)
        {
            db_functions(...);
            db_next_row(result);
        }
    }
    

This is some very basic but familiar SQL code for Pawn, there are a bunch of variables to declare, format the string, query it, loop the rows then you have to gather data on each iteration via db functions. One of the many great things about prepared statements is, they actually bind _variable pointers_ meaning you tell the statement what variable to store the result field data in, loop the fields and while it's fetching each row it actually stores that data into the variables you told it to without you needing to do anything! Once you fetch the row, all your variables are ready to be used! Here's that same code again, but simplified with SQLitei: 
    
    
    new DBStatement:gStmt_Statement1;
    
    public OnGameModeInit()
    {
        gStmt_Statement1 = db_prepare(db, "SELECT kills FROM Users WHERE name = ? AND score > ? OR deaths < ?");
    }
    
    // somewhere else inside a function
    
    new kills;
    
    stmt_bind_value(gStmt_Statement1, 0, DB::TYPE_STRING, name, 24);
    stmt_bind_value(gStmt_Statement1, 1, DB::TYPE_INTEGER, score);
    stmt_bind_value(gStmt_Statement1, 2, DB::TYPE_INTEGER, deaths);
    
    stmt_bind_result_field(gStmt_Statement1, 0, DB::TYPE_INTEGER, kills);
    
    if(stmt_execute(gStmt_Statement1))
    {
        while(stmt_fetch_row(gStmt_Statement1))
        {
            printf("kills variable is already filled with data! Here it is: %d", kills);
            // No need to advance to the next row, it's automatic, just like how result freeing is automatic!
        }
    }
    

Sure, there are technically more lines here but only if you count the ones written in the global space and on OnGameModeInit (where the query is prepared) nevertheless, I find it **much** easier to understand compared to the long string query. And the ability to bind variable pointers is fantastic as Pawn doesn't even natively support pointers! I'd recommend this to anyone, however I did find the documentation a little thin, there was no real explanation to the pointer thing or other things. I wouldn't use it as a beginner to coding or SQL but it's great to upgrade to once you feel experienced enough to understand how the pointers work and basic SQL code. This include was developed by Slice, a great scripter in the SA:MP community who has released many incredibly useful scripts! Check out his [GitHub](https://github.com/oscar-broman) and [forum topic for SQLitei](http://forum.sa-mp.com/showthread.php?t=303682). As usual, if you want any help, tips, code, review requests, etc, email me or drop a comment!
