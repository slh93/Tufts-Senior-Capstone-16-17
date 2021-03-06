
## Add colors and labels to bash profile to easily view branch names and statuses

Follow the steps outlined [here](http://neverstopbuilding.com/gitpro). For Step 5 however, use the following .bash_profile content:

~~~~
source ~/.git-completion.bash
source ~/.git-prompt.sh

WHITE="\[\033[0:37m\]"
MAGENTA="\[\033[0;35m\]"
YELLOW="\[\033[0;33m\]"
BLUE="\[\033[34m\]"
LIGHT_GRAY="\[\033[0;37m\]"
CYAN="\[\033[0;36m\]"
GREEN="\[\033[0;32m\]"

GIT_PS1_SHOWDIRTYSTATE=true

export LS_OPTIONS='--color=auto'
export CLICOLOR='Yes'
export LSCOLORS=gxfxbEaEBxxEhEhBaDaCaD

NOGIT=" (master *+|MERGING)"

export PS1=$WHITE"\u"$GREEN" \W"'$(
        if [[ $(__git_ps1)  == $NOGIT ]]
                # no git repo in this directory
        then echo ""
        elif [[ $(__git_ps1) =~ \*\)$ ]]
                # a file has been modified but not added
        then echo "'$YELLOW'"$(__git_ps1 " (%s)")
        elif [[ $(__git_ps1) =~ \+\)$ ]]
                # a file has been added, but not commited
        then echo "'$MAGENTA'"$(__git_ps1 " (%s)")
                # the state is clean, changes are commited
         else echo "'$CYAN'"$(__git_ps1 " (%s)")
    fi)'$WHITE": "
~~~~

