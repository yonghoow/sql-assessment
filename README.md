# sql-assessment

Qn 2: First, use SELECT * from both tables and use your knowledge of queries and aggregate functions to get to know the data:

-What are the Top 25 schools (.edu domains)?

-How many .edu learners are located in New York?

-The mobile_app column contains either mobile-user or NULL. How many of these Codecademy learners are using the mobile app?

My Ans:

-- top 25 schools (.edu domains)

    SELECT COUNT(user_id), email_domain 
    FROM users
    GROUP BY email_domain
    ORDER BY COUNT(user_id) DESC
    LIMIT 25;

-- No. of learners in New York

    SELECT COUNT (user_id) FROM users
    WHERE city = 'New York';

-- No. of learners using mobile app

    SELECT COUNT (user_id) FROM users
    WHERE mobile_app = 'mobile-user';

Qn 3: Query for the sign up counts for each hour.

My Ans:

-- sign up counts for each hour

    SELECT sign_up_at, strftime('%H', sign_up_at), 
    COUNT(sign_up_at)
    FROM users
    GROUP BY strftime('%H', sign_up_at);

Qn 4: Join the two tables using JOIN and then see what you can dig out of the data!

- Do different schools (.edu domains) prefer different courses?

- What courses are the New Yorkers students taking?

- What courses are the Chicago students taking?

My Ans:

-- do different schools prefer different courses?

    SELECT users.email_domain, 
    COUNT (
        CASE
            WHEN progress.learn_cpp != ''
                THEN users.user_id END) AS cpp_enrolled,

    COUNT (
        CASE 
            WHEN progress.learn_sql != ''
                THEN users.user_id END) AS sql_enrolled,

    COUNT (
        CASE 
            WHEN progress.learn_html != ''
                THEN users.user_id END) AS html_enrolled,
    COUNT (
        CASE 
            WHEN progress.learn_javascript != ''
                THEN users.user_id END) AS javascript_enrolled,

    COUNT (
        CASE 
            WHEN progress.learn_java != ''
                THEN users.user_id END) AS java_enrolled

    FROM users INNER JOIN progress 
    ON users.user_id = progress.user_id;


-- what courses are New Yorkers students taking?

    SELECT users.email_domain, users.city,
    COUNT (
        CASE
            WHEN progress.learn_cpp != ''
                THEN users.user_id END) AS cpp_enrolled,

    COUNT (
        CASE
            WHEN progress.learn_sql != ''
                THEN users.user_id END) AS sql_enrolled,

    COUNT (
        CASE
            WHEN progress.learn_html != ''
                THEN users.user_id END) AS html_enrolled,

    COUNT (
        CASE 
            WHEN progress.learn_javascript != ''
                THEN users.user_id END) AS javascript_enrolled,

    COUNT (
        CASE
            WHEN progress.learn_java != ''
                THEN users.user_id END) AS java_enrolled

    FROM users INNER JOIN progress 
    ON users.user_id = progress.user_id
    WHERE city = 'New York';

-- what courses are the chicago students taking?

    SELECT users.email_domain, users.city,
        COUNT (
            CASE
                WHEN progress.learn_cpp != ''
                    THEN users.user_id END) AS cpp_enrolled,

        COUNT (
            CASE
                WHEN progress.learn_sql != ''
                    THEN users.user_id END) AS sql_enrolled,

        COUNT (
            CASE
                WHEN progress.learn_html != ''
                    THEN users.user_id END) AS html_enrolled,

        COUNT (
            CASE
                WHEN progress.learn_javascript != ''
                    THEN users.user_id END) AS javascript_enrolled,

        COUNT (
            CASE
                WHEN progress.learn_java != ''
                    THEN users.user_id END) AS java_enrolled

    FROM users INNER JOIN progress 
    ON users.user_id = progress.user_id
    WHERE city = 'Chicago';


# Reflection questions:

1. What did you like about this project?

I like that I can do the assessment using the Codecademy website to test my sql queries.

2. What did you struggle with in this project?

I struggled with count() and joining tables at the beginning. 

3. What would make your experience with this assessment better?

I think nothing in this area. The experience is quite good.
