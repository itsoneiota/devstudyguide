Platform Developer Study Guide
==============================

##Key Skills

###Object Oriented Programming
Where we can, we like to model problems as objects. We have objects that represent real things (e.g. `Product`, `Customer`, `Cart`) and objects that perform particular roles handling API requests and data (e.g. `PaymentController` or `DeliveryMethodMapper`).

You should be comfortable talking about objects, and be familiar with the design decisions around how to divide functionality into objects.

####Recommended Reading
- [Head First Java](http://www.amazon.co.uk/dp/0596009208): It's a Java book, but has an excellent description of OOP concepts. OOP in PHP is largely ripped off from Java, so it will look pretty familiar. Feel free to skip the chapters on GUIs and Concurrency.

###Design Patterns
Design Patterns are a useful common vocabulary for larger software systems. We'll quite often talk about a Strategy or an Observer, which can be a useful shorthand for a structure involving several classes and interfaces.

####Recommended Reading
- [Head First Design Patterns](http://www.amazon.co.uk/dp/0596007124): Another Head First book. The books weigh a ton, but they do a great job of making some quite techy stuff readable. This is much more approachable than the classic [Gang of Four](http://www.amazon.co.uk/dp/0201633612).

###PHP
To say that PHP is our language of choice might be a bit strong. It's what we use. It has its idiosyncrasies, but it gets the job done.

An understanding of PHP isn't essential for new recruits --- people quickly learn to hate it like the rest of us --- but it may help to get a rough handle on it.

If you're coming from a statically typed language like Java or C#, you probably ought to know [some of the terrible things PHP does with types](http://php.net/manual/en/language.types.type-juggling.php).

Otherwise, some [string manipulation](http://php.net/manual/en/book.strings.php) and a bit of [array bashing](http://php.net/manual/en/book.array.php) should stand you in good stead.

It may also help to know what's in the [PHP Standard Library](http://php.net/manual/en/book.spl.php). It contains several common data structures and nice object interfaces to handle common tasks (e.g. iterating over the filesystem).

###Test-Driven Development
We're big fans of test-driven development. We use [PHPUnit](https://phpunit.de) for unit tests and [Behat](http://behat.org) for end-to-end API tests. Those particular tools are far less important than the general concept of writing automated tests, and designing systems so that they can be tested.

####Recommended Reading
- [Test Driven Development](http://www.amazon.co.uk/dp/0321146530) is the classic text on the practice, and is a good introduction.
- [The Google Testing Blog](http://googletesting.blogspot.co.uk) is a great resource once you're up and running. In particular, their [Testing on the Toilet](http://googletesting.blogspot.co.uk/search/label/TotT) series of short articles cover best practices and common mistakes.

### JSON
JSON is a human-friendly machine-readable format, which we use pretty heavily, for APIs, config files, storage, all sorts. [There's not much to know about JSON itself](http://json.org), but it might help you to have a look. It would also be good to look at [how PHP handles JSON](http://php.net/json).

If you're feeling adventurous, you could take a look at [JSON Schema](http://json-schema.org), which is a nice way of describing what can and should be in a JSON document. We use this to validate API requests, and to describe our APIs.

###REST
This one can inspire raging debates with pseudo-religious fervour. Don't get bogged down in that, and don't bother with [Roy Fielding's dissertation](http://www.ics.uci.edu/~fielding/pubs/dissertation/fielding_dissertation.pdf) unless you're feeling particularly scholarly. For us, all you really need to grok are:

- [URIs](https://en.wikipedia.org/wiki/Uniform_resource_identifier) as identifiers for resources
- [HTTP methods](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods) and what they do
- [Hypermedia as the Engine of Application State](https://en.wikipedia.org/wiki/HATEOAS)

####Recommended Reading
- [RESTFul Web Services](http://www.amazon.co.uk/dp/0596529260)
- [Richardson Maturity Model](http://martinfowler.com/articles/richardsonMaturityModel.html)

###Cloud Infrastructure
We run everything in the [Amazon Web Services](https://aws.amazon.com) cloud. We use quite a few of the services provided by AWS, such as [servers](https://aws.amazon.com/ec2), [storage](https://aws.amazon.com/s3), [relational databases](https://aws.amazon.com/rds), [NoSQL databases](https://aws.amazon.com/dynamo), [caches](https://aws.amazon.com/elasticache), [message queues](https://aws.amazon.com/sqs), [deployment tools](https://aws.amazon.com/elasticbeanstalk), [infrastructure as code](https://aws.amazon.com/cloudformation), and more. It would be good to understand what these are and how you might use them to build large web-scale systems. If you haven't used these before, it _might_ help to look at how AWS does things. If you're familiar with them from somewhere else, don't worry too much about the AWS-specific details.

####Amazon Web Services Terminology
We tend to assault new developers with a barrage of acronyms and initialisms. AWS is especially bad for this. If you're working on personal projects, you could do a lot worse than run them on AWS. That can give you a head start with the jargon.

###NoSQL Databases


###Relational Databases


###Cool Things We're Not Doing (Yet)
It's probably worth noting a few hot topics that we _don't_ have much use for at present. We wouldn't want to rule them out, but it's fair to say you'd be unlikely to use them on day one.

- Agile Methodologies
- Functional Programming
- Big Data (Hadoop, etc.)
- Machine Learning

##Project Ideas --- Useful

###Email Service

We send hundreds of emails daily for customer sign-up, order confirmation, despatch notifications, etc. At present, our emailing code is tied up in the main platform codebase, so we need to push a code change to production just to change the text in an email. We'd like to break out our emailing functions into a stand-alone service.

The service will need to:

- Store/edit email templates. These will be HTML and plain text, with placeholders for variables. They should be held in a database.
- Receive requests to send emails. It will need to put variables from the data given into placeholders, and integrate with Amazon Web Services' [Simple Email Service][SES] to send the email from the correct address.

We have some existing PHP code that could be used for parts of this.

###Database Waste Detector

We run a suite of tests on our platform frequently to check that new changes haven't broken anything. At the end of each test, we tidy up the database used, ready for the next test. It would be useful to have an automated tool look at the database and make sure that the code hasn't left any "waste" behind. For example, deleting orphaned rows. We don't use referential integrity constraints, so it's possible that a parent row can deleted without deleting all of its children. Given table/key relationships, the tool should find any rows that should have been deleted.

##Project Ideas --- Frivolous

We have an air hockey table in the office. There are a couple of software tools that could help us improve.

###Air Hockey Scoreboard

A scoreboard system could:

- Register players.
- Keep track of games played.
- Maintain leaderboard.
- Compute statistics (most consistent, best defence, etc.)
- Notify players if they haven't played for a while.

###Air Hockey Analysis

I'd love to see this done.

Basically, a limited version of [this project](http://cienciaycacharreo.blogspot.co.uk/2014/02/new-project-air-hockey-robot-3d-printer.html). Have a computer analyse the movement of the puck during an air hockey game and give its analysis.

- Use computer vision to analyse air hockey games.
- Classify shots played / scored.
- Generate match statistics (shots on target, etc.)
- Feed back to players on strengths weaknesses.

[HipChat]: https://www.hipchat.com
[SES]: https://aws.amazon.com/ses/
[PD]: http://www.pagerduty.com
[JIRA]: https://www.atlassian.com/software/jira/
