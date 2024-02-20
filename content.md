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

[Source](https://blog.appsignal.com/2022/10/05/security-best-practices-for-your-rails-application.html)

[More on common security problems and how to address them with Rails](https://guides.rubyonrails.org/security.html)

[Lecture Video](https://youtu.be/aIbkLU8av0A)
