# Automated Sendmail Configuration for AWS SES on Elastic Beanstalk

*An [ebextensions](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/ebextensions.html) solution for configuring an [Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/) deployment to be able to use the integrated mail client, [sendmail](https://linux.die.net/man/8/sendmail.sendmail), with Amazon's email service, [Amazon SES](https://aws.amazon.com/ses/)*

## Overview

The default linux image used by Amazon EC2 instances, [Amazon Linux AMI](https://aws.amazon.com/amazon-linux-ami/), includes
the email client, [sendmail](https://linux.die.net/man/8/sendmail.sendmail), that can be used to send emails.

This repository provides an [ebextensions](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/ebextensions.html) solution to configure sendmail to use Amazon SES.

**This solution only provides a way to automate the configuration described in [Amazon's official documentation](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/send-email-sendmail.html).**

**Please check the Prerequisites and read the documentation thoroughly before using this.**

## Installation

### Add Environmental Variables to EB

[Add the following environmental variables to your EB environment:](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/environments-cfg-softwaresettings.html#environments-cfg-softwaresettings-console)

* `MAIL_HOST` - The SMTP server to use EX `email-smtp.us-east-1.amazonaws.com` [(refer to smtp connection strings at the bottom of the page)](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/smtp-issues.html)
* `MAIL_USERNAME` - [Amazon SES](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/smtp-credentials.html) username
* `MAIL_PASSWORD` - [Amazon SES](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/smtp-credentials.html) password
* `MAIL_DOMAIN` - Verified domain to send mail from. [Must be qualified with Amazon SES](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-domain-procedure.html)

### Add ebextensions

Copy the `.ebextensions` folder to the top level of your application directory

### Usage

Sendmail usage is normal but you must specify the sender address as a [verified SES email address](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-email-addresses-procedure.html) using the `-f` option like so:

```bash
sudo /usr/sbin/sendmail -f sender@example.com to@example.com
```

## Contributing

Make a PR for some extra functionality and I will happily accept it :)

##  License

This repository is licensed under the [MIT license](https://github.com/FoxxMD/sendmail-ses-elasticbeanstalk/blob/master/LICENSE).