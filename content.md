# Security 🔒

Security is a huge topic in software. New vulnerabilities are being discovered all the time. Here are a few actionable best practices to think about with your own projects.

## Force SSL

You can force your Rails application to always use a secure connection with the HTTPS protocol. To do this, open the `config/environments/production.rb` file and set the following line:

```
config.force_ssl = true
```

## Secure Environment Variables

You should never hardcode your API keys, passwords, or other sensitive credentials in the source code. You might accidentally make them public or give someone who's not authorized access to some sensitive application resources. You should always use Environment variables or encrypted application credentials for this sensitive information.

## Strong Authentication and Authorization Rules

- **Authentication** - You validate a user's login and password against an application's database. [Reading: More on User Authentication with Devise](https://learn.firstdraft.com/lessons/195-authentication-with-devise).
- **Authorization** - You validate the role of a signed-in user and, based on that, render different information for different users. For example, a user with an admin role can access a list of users in an application, while in most cases, the typical user can't. You can set this up using [Reading: Authorization with Pundit 🔒](https://learn.firstdraft.com/lessons/202-pundit-authorization)

## Avoid SQL Injection

SQL injection is one of the most popular techniques used to access database information from the outside. The Rails framework tries to protect us from that threat, but we also need to write code that won't let this happen. In general, we should avoid passing user input directly as a part of a query.

[Read more](https://guides.rubyonrails.org/security.html#sql-injection)

## DDoS and Malicious Traffic

A distributed denial-of-service (DDoS) attack is where a large number of computers or devices, usually controlled by a single attacker, attempt to access a website or online service all at once. This flood of traffic can overwhelm the website’s origin servers, causing the site to slow down or even crash.

This is one of the reasons why you have to fill out CAPTCHAs (Completely Automated Public Turing test to tell Computers and Humans Apart).

You should monitor for suspicious traffic ( [Business Insights and Analytics 🕴️](https://dpi.instructure.com/courses/294/assignments/2068?wrap=1)). You may want to configure your domain to use a service like [Cloudflare](https://www.cloudflare.com/) to filter out malicious traffic or add the [rack-attack gem](https://github.com/rack/rack-attack) so you can easily decide when to *allow*, *block* and *throttle* based on properties of the request.

## Perform Security Audits

I don't mean expensive audits by external companies. Often, it is enough to install a tool like [Brakeman](https://brakemanscanner.org/) and scan code with every commit or pull request.

Also, it is a good idea to scan your Gemfile and find gems that need updating due to security issues discovered by the community. You can use [bundler-audit](https://github.com/rubysec/bundler-audit) to automate this process.

## Collect Logs

Console Logs are usually just thousands of lines of information you will never view. However, there might be a case where one of your users is attacked or experiences a suspicious action. If you have detailed and easily searchable logs, you can collect information that will help you prevent similar problems in the future.

## Quiz

- How can you force your Rails application to always use a secure connection with the HTTPS protocol?
- By setting `config.force_ssl = true` in the `config/environments/production.rb` file.
  - Correct! This configuration forces the application to use HTTPS.
- By setting `config.use_https = true` in the `config/application.rb` file.
  - Not quite. The correct setting is `config.force_ssl = true` in the `production.rb` file.
- By adding `<%= force_ssl %>` in the application layout file.
  - Not quite. The correct way is to configure it in the `production.rb` file.
{: .choose_best #force_ssl title="Forcing SSL" points="1" answer="1" }

- Why should you never hardcode API keys, passwords, or other sensitive credentials in the source code?
- It is not allowed by the Rails framework.
  - Not quite. While it's not a best practice, Rails does not enforce this restriction.
- It can slow down your application.
  - Not quite. The primary concern is security, not performance.
- You might accidentally make them public or give unauthorized access to sensitive resources.
  - Correct! Hardcoding sensitive information can lead to accidental exposure.
{: .choose_best #secure_env_variables title="Secure Environment Variables" points="1" answer="3" }

- What is the difference between authentication and authorization?
- Authentication validates a user's login and password, while authorization validates the role of a signed-in user and controls access based on that role.
  - Correct! Authentication is about verifying identity, while authorization is about controlling access.
- Authentication validates user roles, while authorization validates login credentials.
  - Not quite. Authentication verifies login credentials, while authorization verifies user roles.
- Authentication and authorization are the same.
  - Not quite. They serve different purposes in security.
{: .choose_best #auth_vs_author title="Authentication vs Authorization" points="1" answer="1" }

- What is the primary technique to avoid SQL injection in Rails applications?
- Encode all user inputs before storing them in the database.
  - Not quite. Encoding does not address SQL injection directly.
- Avoid passing user input directly as part of a query and use parameterized queries.
  - Correct! Using parameterized queries helps prevent SQL injection.
- Hash all user inputs before storing them in the database.
  - Not quite. Hashing is used for password security, not for preventing SQL injection.
{: .choose_best #avoid_sql_injection title="Avoiding SQL Injection" points="1" answer="2" }

- What is one way to protect your Rails application from DDoS attacks?
- Use a service like Cloudflare to filter out malicious traffic or the `rack-attack` gem to manage request behavior.
  - Correct! These tools can help mitigate the impact of DDoS attacks.
- Disable all external traffic to your application.
  - Not quite. This would prevent legitimate users from accessing your application.
- Require users to re-authenticate every minute.
  - Not quite. Frequent re-authentication does not address DDoS attacks effectively.
{: .choose_best #ddos_protection title="Protecting Against DDoS Attacks" points="1" answer="1" }

- What is a recommended way to manage sensitive credentials in your Rails application?
- Hardcode them in your source code.
  - Not quite. Hardcoding sensitive information can lead to security risks.
- Use environment variables or encrypted application credentials.
  - Correct! These methods help keep sensitive information secure.
- Store them in a plaintext file in your project directory.
  - Not quite. Storing sensitive information in plaintext is not secure.
{: .choose_best #manage_credentials title="Managing Sensitive Credentials" points="1" answer="2" }

- Why is it important to collect and keep detailed logs for your application?
- Logs can help you identify and prevent security issues by providing detailed information about suspicious actions.
  - Correct! Detailed logs are crucial for troubleshooting and preventing security incidents.
- Logs improve application performance.
  - Not quite. While useful for security, logs do not directly improve performance.
- Logs are required for deploying applications to production.
  - Not quite. Logs are not a deployment requirement but are important for security monitoring.
{: .choose_best #collect_logs title="Importance of Collecting Logs" points="1" answer="1" }

## Resources
- [Source](https://blog.appsignal.com/2022/10/05/security-best-practices-for-your-rails-application.html)
- [More on common security problems and how to address them with Rails](https://guides.rubyonrails.org/security.html)
- [Lecture Video](https://youtu.be/aIbkLU8av0A)
