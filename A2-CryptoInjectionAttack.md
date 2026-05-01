# Assignment 2: Crypto and Injection Attack

## Part 1: Injection Vulnerability Analysis

### Snippet 1 Questions:
1. What type of injection vulnerability exists here?
- SQL Injection
2. Write an example attack payload that would exploit this
- An example attack payload that can exploit this is `‘ OR ‘1’ = ‘1` which makes the condition always true so the query will return all rows in the patient record.
3. What damage could an attacker do with this vulnerability?
- The attacker can get all, modify, or delete the patient records which is a breach of patient’s privacy. 


### Snippet 2 Questions:
1. What type of injection vulnerability exists here?
- Command injection
2. Write an example attack payload
- `; evil-cmd`
3. What could an attacker do with this vulnerability?
- This code is using the command shell and you can use a semicolon which is a command line separator to run an executable command 
4. Explain why shell commands with user input are dangerous
- This allows attacker to run their own shell command on your system


### Snippet 3 Questions:
1. Identify TWO different injection vulnerabilities in this code
- SQL Injection and JavaScript Injection
2. For each vulnerability:

#### SQL Injection:
1. What type of injection is it?
- SQL Injection
2. Provide an attack payload example 
- `‘ OR ‘1’ = ‘1`
3. Explain the impact
- The attacker can get all, modify, or delete the note records and reveal patient data.

#### JavaScript Injection:
1. What type of injection is it?
- JavaScript Code Injection
2. Provide an attack payload example 
- `<script>windows.location=’https://example.com’</script>`
3. Explain the impact
- The attacker can add a malicious website or fake data on the website. 


### Snippet 4 Questions:
1. This code has SQL injection in TWO different parameters. Identify both.
- `Patient_id` and `medication`
2. For the patient_id parameter:
- Why is it vulnerable even without quotes?
    - Because even without quotes the attacker can just use other things like a semicolon or a space to trick the system into thinking it's part of the logic or command.
- Provide an attack payload
    - `‘ OR ‘1’ = ‘1`
3. For the medication parameter:
- Write a UNION injection that would dump all patient data
    - `‘ UNION SELECT id, username, password, email FROM users –`
- Explain how this attack works
    - The `‘` will end the last command and so the next line becomes a new command which will perform a UNION which in the case above grabs users data.



### Snippet 5 Questions:
1. What injection vulnerability exists here?
- Command Injection
2. Provide an attack payload that would execute arbitrary commands on the server
- `; rm -rf /`
3. Explain step-by-step how the attack works
- The semicolon tricks the system into thinking the `rm -rf /` is part of the logic and this particular command will delete every file on the server.
4. When should shell=True be used in python subprocess?
- You should never use `shell=True` unless because this will give the attacker access to your shell command, your system.



## Part 2: Cryptography Mistakes

### Snippet 6 Questions:
1. Identify TWO major cryptography mistakes in this code (there are more than two)
`password_hash = hashlib.md5(password.encode()).hexdigest()`
- **Mistake 1:** weak hashing algorithm
- **Mistake 2:** no salting added
2. For each mistake:
#### Mistake 1:
- What's wrong?
    - Mistake 1 is using md5 to hash the password
- What attack does this enable?
    - MD5 is an old hashing algorithm that is fixed-sized 128-bit hash value so the attacker can use brute force collision attack.
- How would you fix it?
    - Use a different more modern hashing algorithm like SHA-256 and SHA-3.

#### Mistake 2:
- What's wrong?
    - Mistake 2 is not adding salt to the password
- What attack does this enable?
    - Without salt added to the password, the attackers can use the pre-computed tables like Rainbow Tables to guess the password
- How would you fix it?
    - Use a built in, vetted hashing algorithm that has a pre-built salting like Argon2.

3. Does the check_password function have an exploitable timing attack vulnerability? Explain why it does or doesn't in your opinion. 
- It has a timing attack vulnerability since it’s using the == comparison operator.  The attacker can use this to measure the response time to guess and figure out the password.


### Snippet 7 Questions:
1. What cryptography mistake makes this token generation insecure?
- I think the mistake here is using .random for the token
2. How could an attacker predict these session tokens?
- Because `.random` in Python uses the Mersenne Twister formula which is public knowledge, so the attacker can use this formula to guest the tokens used on the server.
3. How long (length) should session tokens be? Why?
- Tokens should be at least 128-bits because it is large enough that the odds of collision is almost zero.
4. What's the difference between random and secrets modules in Python?
- The difference between `random` and `secrets` modules is that `random` uses a formula Mersenne Twister which is not secure and `secrets` is more secure it uses entropy so there is no seed or mathematical pattern that can be reversed engineered by the attacker. 


## Part 3: Risk Assessment
Provide your risk categorization for ALL the vulnerabilities you found (Snippets 1-7) from most to least dangerous in a markdown table.
The columns should be 'Rank' (0-6, 0 being 'worst'), 'Snippet #', 'Vulnerability name', and 'Severity' (Critical / High / Medium / Low).


| Rank | Snippet | Vulnerability Name                  | Severity |
|------|---------|-------------------------------------|----------|
|1     |5        |Command Injection                    |Critical  |
|2     |2        |Command Injection                    |Critical  |
|3     |3        |SQL Injection + JavaScript Injection |Critical  |
|4     |4        |SQL Injection                        |High      |
|5     |1        |SQL Injection                        |High      |
|6     |7        |Weak Hashing Vulnerability           |High      |
|7     |6        |Timing Attack                        |Medium    |

### Then answer:
1. Which single vulnerability would you fix first if you only had time for one? Why? (~paragraph)
- The single vulnerability that I would first fix on the FroggyHealthPortal would be Snippet 5 because it has the most critical vulnerability. The shell=True was added to the code. This gives the attacker access to the server command shell (pretty much the system), so this is a very serious security issue. The attacker can exploit characters such as semicolons to execute codes on the server and tell it to do anything. They can install viruses, delete and steal files, or install backdoors to the system.
2. Which vulnerability do you think would take the longest to fix? (~paragraph)
- The vulnerability that would take the longest to fix would probably be Snippet 6 because it’s about password storage which involves fixing the password database and most of the time, the actual user password are unknown since it’s stored in md5, so you will probably have to force everyone to redo their password.
3. How much do you plan to charge for your security review? (~sentences)
- I am not really sure how much I would charge for a security review, it will depend on the job and the time it would take, so I will probably charge hourly and according to an online search the average in Seattle, WA is $100 per hour. 
4. Do you plan to sign up for FroggyHealthPortal? Explain why / why not. (~sentences)
- No, because on the 7 snippets alone, it has a lot of critical and high security risks so I don't feel like my privacy and information is secure or safe.
