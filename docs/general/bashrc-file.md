# .bashrc File

These are my additions to my `.bashrc` file.

## `nvm`

When installing, `nvm` automatically loads this to the `.bashrc`, but in case it does not:

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
```

## `screen`

In WSL `screen` is not available by default. This enables it.

```bash
# This one enables the screen tool
export SCREENDIR="$HOME/.screen"
[ -d $SCREENDIR ] || mkdir -p -m 700 $SCREENDIR
```

## SSH Agent

This automatically loads the SSH agent at terminal boot, enabling a single password prompt for persistent access to the key during this session.

```bash
# This one enables auto ssh for git
env=~/.ssh/agent.env

agent_load_env() { test -f "$env" && . "$env" >|/dev/null; }

agent_start() {
    (
        umask 077
        ssh-agent >|"$env"
    )
    . "$env" >|/dev/null
}

agent_load_env

# agent_run_state: 0=agent running w/ key; 1=agent w/o key; 2= agent not running
agent_run_state=$(
    ssh-add -l >|/dev/null 2>&1
    echo $?
)

if [ ! "$SSH_AUTH_SOCK" ] || [ $agent_run_state = 2 ]; then
    agent_start
    ssh-add
elif [ "$SSH_AUTH_SOCK" ] && [ $agent_run_state = 1 ]; then
    ssh-add
fi

unset env
```

## GPG

This enables automatic GPG signing for git commits.

```bash
# This one is for GPG signing
export GPG_TTY=$(tty)
source "$HOME/.cargo/env"
```

## PS1 Customization

My extensive customisation of the PS1 command line prompt. This will show your user and system name, which directory you are in, your project name and version, your git branch, and the system time.

```bash
function parse_git_branch() {
    BRANCH=$(git branch 2>/dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/\1/')
    if [ ! "${BRANCH}" == "" ]; then
        echo "${BRANCH}"
    else
        echo "null"
    fi
}

function parse_npm_version {
    PACKAGE_DATA=$(npm version | cut -d$'\n' -f 2)
    PACKAGE_NAME=$(echo ${PACKAGE_DATA} | cut -d : -f 1 | sed -E -e "s/('|,)//g")
    PACKAGE_VERSION=$(echo ${PACKAGE_DATA} | cut -d : -f 2 | sed -E -e "s/(\s|'|,)//g") 
    if [ ! "${PACKAGE_NAME}" == "npm" ]; then
        echo $PACKAGE_NAME v$PACKAGE_VERSION
    else
        echo "no project"
    fi
}

export PS1="\[\e[35m\]\u\[\e[m\] on \[\e[35m\]\h \[\e[m\]is in \[\e[36m\]\W\[\e[m\] editing \[\e[33m\]\`parse_npm_version\`\[\e[m\] on branch \[\e[32m\]\`parse_git_branch\`\[\e[m\] at \[\e[34m\]\t\[\e[m\]\n\[\033[0;32m\]└─\[\033[0m\033[0;32m\] \$\[\033[0m\033[0;32m\] ▶\[\033[0m\] "
```
