# GPG agent pinentry error fixer

Keywords: gpg, agent, pinentry, su, ssh, tty, curses

Treats: 

 * GPG error message "No manual entry for pinentry"
 * "gpg: problem with the agent: No pinentry"
 * "gpg: decryption failed: No secret key"

Try running the script in this repository.


## Fixer ideas

Set environment variables such as: 

    PINENTRY_USER_DATA="USE_CURSES=1"
    export PINENTRY_USER_DATA
    echo $PINENTRY_USER_DATA
    
    GPG_TTY=$(tty)
    export GPG_TTY
    echo $GPG_TTY
    
Do we have a viable pinentry that uses curses?

    which pinentry-curses

Set the GPG agent to use TTY by editing `~/.gnupg/gpg-agent.conf` and using a line such as one of these:
 
    pinentry-program /usr/local/bin/pinentry-curses

    pinentry-program /usr/bin/pinentry-tty

Kill any gpg-agent:

    killall gpg-agent

Start gpg-agent such as one of these:

    gpg-agent --daemon --pinentry-program /usr/local/bin/pinentry
    
    gpg-agent --daemon --keep-tty --use-standard-socket --pinentry-program=/usr/bin/pinentry-curses

