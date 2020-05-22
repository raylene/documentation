# Security Best Practices

This document describes **security best practices** at U.S. Digital Response ("USDR"). If you have a good reason to request diverging from these policies, we need to hear from you at [info@usdigitalresponse.org](mailto:info@usdigitalresponse.org).

## Guiding Principles

- **Ask questions. Ask for help.** Nobody is expected to be a security expert. If you get the feeling that some part of your project needs some extra security eyes, please ask for guidance. USDR security team members are instructed to be helpful & solution oriented. Specifically, if you find yourself touching _encryption, authentication, or sensitive data_ please reach out in the [#security](https://usdrcovid19.slack.com/archives/C013NQERZ6K) channel!
- **Assume malicious.** Wherever a user will interact with your application, assume malicious intent! Be sure to properly validate input, restrict access, and safely store any data at all layers of your application.

## Web Application Security

This section covers security best practices to consider for web apps. These recommendations span all languages, frameworks, or deployment methods.

### Untrusted User Data & Input

If your web app collects data from users you can be at risk of cross site scripting (XSS), SQL and NoSQL injection (SQLi), and cross site request forgery (CSRF) among other vulnerabilities. The best thing to protect your application and users from these vulnerabilities is to **encode output** and **validate input**.

**Encoding output** is simple if you are using a frontend framework that automatically encodes output. React and Angular both automatically encode output by default, and are highly recommended to use. If your web framework does not support output encoding by default, make sure that you use a library to encode any user data returned to the client.

**Validating input** can be as simple as checking the range, size, or length of input returned from users. Checking that the data users are submitting is what you expect goes a long way towards security hygeine.

**Database queries** that include user input are at risk of being exploited by noSQL/SQL injection. Be sure to use _parameterized queries_ via a database library which will safely encode any user data passed in as parameters. **Do not string concatenate database queries.** (i.e. `db.query("SELECT * FROM users where email=${USER_PROVIDED_INPUT}")`) Attackers can manipulate the data they send to change the behavior of queries. This can lead to tables being dropped or user data being stolen.

### Authentication, Permissions, Access Control

If at all possible projects should allow another system to manage authentication. If working with a government entity, work with them to let their system handle any authentication or authorization requirements. If some sort of authentication is required, please reach out to [#security](https://usdrcovid19.slack.com/archives/C013NQERZ6K)!

Any sensitive data that gets returned to the client should perform permission checks **on the server-side** to ensure that its safe to return that data. Any permission checks that happen in the frontend can be bypassed by hitting an API endpoint directly.

### Dependency Management

USDR uses a tool called [Snyk](https://app.snyk.io/org/usdigitalresponse) for public Github repositories that automatically scans pull requests for vulnerabile dependencies. Snyk will often be able to recommend which version you need to upgrade to in order to fix the vulnerability. By default Snyk will fail a build on High severity vulnerabilities that have a patch available.

Reach out in the [#security](https://usdrcovid19.slack.com/archives/C013NQERZ6K) Slack channel to get your public Github repo integrated.

## Cloud Security

This section covers security best practices to consider for infrastructure running in a cloud provider. These recommendations are specific to [AWS best practices](https://aws.amazon.com/premiumsupport/knowledge-center/security-best-practices/), but generally apply to other cloud providers such as Azure, GCP, and Oracle.

### Identity and Access Management (IAM)

IAM is the AWS service that manages users, roles, and access. _Every_ project in AWS will require interacting with IAM.

Be sure to:

- Restrict the amount of permissions that a role has to only whats needed to do the job.
- Do not store long lived AWS credentials (AWS API keys) in source code or in plaintext anywhere.

Read here to learn about [IAM security best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html).

### Relational Database Service (RDS)

Read here to learn more about [RDS security best practices](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_BestPractices.Security.html).

### Simple Storage Service (S3)

Read here to learn more about [S3 bucket security best practices](https://docs.aws.amazon.com/AmazonS3/latest/dev/security-best-practices.html).

## Lambda

Read here to learn more about [lambda security best practices](https://docs.aws.amazon.com/lambda/latest/dg/lambda-security.html).
