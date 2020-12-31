- I end up creating a lot of directories and find it helpful to have `mkdir` and `cd` in one command

```bash
function mkdircd {
  mkdir -p $1 && cd $1
}
```

- Why correct my typos when the computer can accomodate instead? :grin:

```bash
alias sl="ls -alrth"
alias ls="ls -alrth"
```