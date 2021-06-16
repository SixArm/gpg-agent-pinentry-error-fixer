# GPG agent pinentry error fixer

<img src="README.png" alt="GnuPG" width="450" height="153"/>

Keywords: gpg, agent, gpg-agent, gnupg, pinentry, su, ssh, tty, curses

Treats: 

 * GPG error message "No manual entry for pinentry"
 * "gpg: problem with the agent: No pinentry"
 * "gpg: decryption failed: No secret key"

Try running the script in this repository:

  * [gpg-agent-pinentry-error-fixer](gpg-agent-pinentry-error-fixer)


## What else to try

Set environment variables such as: 

    PINENTRY_USER_DATA="USE_CURSES=1"
    export PINENTRY_USER_DATA
    echo $PINENTRY_USER_DATA
    
    GPG_TTY=$(tty)
    export GPG_TTY
    echo $GPG_TTY
    
Do we have a viable pinentry that uses curses or tty?

    which pinentry-curses
    which pinentry-tty


## Install pinentry

For macOS and brew:

    brew install pinentry

For Debian and Ubuntu:

    apt-get install pinentry
    apt-get install pinentry-curses

The pinentry program has many versions:

    pinentry
    pinentry-curses
    pinentry-emacs
    pinentry-gnome3
    pinentry-gtk2
    pinentry-qt
    pinentry-tty


## Set pinetry

Set the GPG agent to use the pinentry program.

Edit `~/.gnupg/gpg-agent.conf`

Add a line such as:
 
    pinentry-program /usr/local/bin/pinentry-curses

Try now.


## Reload

Reload the agent:

    gpg-connect-agent reloadagent /bye

Try now.


## Restart

If GPG still isn't working, and has the same error message, then try kill and restart.

Kill any gpg-agent:

    killall gpg-agent

Start gpg-agent such as one of these:

    gpg-agent --daemon --pinentry-program /usr/local/bin/pinentry
    
    gpg-agent --daemon --keep-tty --pinentry-program=/usr/bin/pinentry-curses

Try now.

