# Redirect all mail to local user

###### Original article can be found there: [Sendmail: redirect all mail for development](http://william.shallum.net/random-notes/sendmailredirectallmailfordevelopment)

### Install `sendmail`
```bash
$ sudo apt-get install sendmail
```

### Add next lines to `/etc/mail/sendmail.mc`
```bash
LOCAL_RULE_0
R$*     $#local $:username
```
+ `username` you must change to your system username. Can be found by the next command:
```bash
$ whoami
```
+ The space between `R$*` and `$#` is a `TAB` character. You must use a tab character `(ASCII 9)` here.

### Run `make` and reload configuration
```bash
$ cd /etc/mail && sudo make
$ sudo service sendmail reload
```

### Mail management
To read or delete redirected emails can be used simple and nice console application `mutt`, so:
```bash
$ sudo apt-get install mutt
```

### To test, you can use `sendmail -bt`:
```bash
$ sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> 3,0 someuser@example.com
canonify           input: someuser @ example . com
Canonify2          input: someuser < @ example . com >
Canonify2        returns: someuser < @ example . com . >
canonify         returns: someuser < @ example . com . >
parse              input: someuser < @ example . com . >
Parse0             input: someuser < @ example . com . >
Parse0           returns: someuser < @ example . com . >
ParseLocal         input: someuser < @ example . com . >
ParseLocal       returns: $# local $: username
parse            returns: $# local $: username
```

### Note that this will also redirect emails for local users, which may not be what you want:

```bash
$ sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> 3,0 root
canonify           input: root
Canonify2          input: root
Canonify2        returns: root
canonify         returns: root
parse              input: root
Parse0             input: root
Parse0           returns: root
ParseLocal         input: root
ParseLocal       returns: $# local $: username
parse            returns: $# local $: username
```