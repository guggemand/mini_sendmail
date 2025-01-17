# mini_sendmail

This fork includes some fixes from other forks, specifically:

* [Timestamp fix](https://github.com/rgpublic/mini_sendmail/commit/2432d0869885b7755a69114cf2ceea3403012da4)
* [Shared libraries](https://github.com/simonswine/mini_sendmail/commit/fb290c11486bc1e0ddf7f0d935e6435ed2d2c00e)

Fork **with minor modifications** of official mini_sendmail (https://acme.com/software/mini_sendmail/).

Author of this repository is not related to Jef Poskanzer in any way.

## Additional features/bugfixes of this fork

* Fix sending e-mail to addresses in format `Full Name <name@example.com>`.
* Support `chroot` jails without `/proc` and `utmp` (by using "app" instead of 
username upon failure to determine it).

# Original README for mini_sendmail
     mini_sendmail - accept email on behalf of real sendmail
                   version 1.3.7 of 03jul2014

mini_sendmail reads its standard input up to an end-of-file and
sends a copy of the message found there to all of the addresses
listed.  The message is sent by connecting to a local SMTP server.
This means mini_sendmail can be used to send email from inside a
chroot(2) area.

See the manual entry for more details.

Files in this distribution:

    README		this
    Makefile		guess
    mini_sendmail.c	source file
    mini_sendmail.8	manual entry

To build: If you're on a SysV-like machine (which includes old Linux systems
but not new Linux systems), edit the Makefile and uncomment the SYSV_LIBS
line.  Otherwise, just do a make.

After it's built, you must test it to make sure your local sendmail
daemon is (a) running and (b) accepting local mail for delivery
elsewhere.  Here's what a successful test run might look like:

    % echo 'Subject: test' | ./mini_sendmail -v jef@mail.acme.com
    <<<< 220 gate.acme.com ESMTP Sendmail; Thu, 16 Dec 1999 17:17:37 -0800 (PST)
    >>>> HELO localhost
    <<<< 250 gate.acme.com Hello localhost [127.0.0.1], pleased to meet you
    >>>> MAIL FROM:<jef@gate.acme.com>
    <<<< 250 <jef@gate.acme.com>... Sender ok
    >>>> RCPT TO:<jef@mail.acme.com>
    <<<< 250 <jef@mail.acme.com>... Recipient ok
    >>>> DATA
    <<<< 354 Enter mail, end with "." on a line by itself
    <<<< 250 RAA58877 Message accepted for delivery
    >>>> QUIT
    <<<< 221 gate.acme.com closing connection
    % 

And here's an unsuccessful run where there's no local sendmail
daemon running:

    % echo 'Subject: test' | ./mini_sendmail -v jef@mail.acme.com
    ./mini_sendmail: connect: Connection refused
    % 


Feedback is welcome - send bug reports, enhancements, checks, money
orders, etc. to the addresses below.

    Jef Poskanzer  jef@mail.acme.com  http://www.acme.com/jef/
