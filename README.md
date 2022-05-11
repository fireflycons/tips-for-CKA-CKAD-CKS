# Tips for CKA-CKAD-CKS
Quick tips on preparation for these exams.

The Certified Kubernetes exams are all online-proctored. This means that you do them from your own workstation, not at a test centre while connected to a proctor who is watching you through your camera. 

They are also performance based. This means that you have to solve somewhere between 17 and 25 questions using a Linux terminal provided in the exam portal via your browser. So you have no nice GUI editors like VSCode etc - just `vim` or `nano` text based editors. You will need to get fast at editing YAML files in these editors!

## Proctor and Workspace

* Allow at least 15-20 minutes from when you first connect with the proctor to them actually launching the exam!
* Make sure there is nothing within 2 metres of where you are sitting, other than the computer equipment required for the exam. You are also allowed water in a clear glass. No pens, paper, any other clutter.
* Make sure you can move your camera. Proctor will want a 360 degree sweep of the area, and will want to see under your desk.
* The jury is out as to whether you can have two monitors, though given the requirements for what you can run in the next section there's little point in it, so better to disconnect/remove additional monitors. If using a laptop with connected external monitor, set external as primary and work with laptop lid closed (this will likely require you to have a plug-in USB camera).

## Your Workstation

* You may only use Chrome or Chromium browser for full compatibiliy with exam interface.
* You may only have one instance of this running, and no other foreground tasks. Proctor will likely ask you to run up your system's task manager application to verify this.
* You may have one additional browser tab open to view allowed documentation [CKA/CKAD](https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed#certified-kubernetes-administrator-cka-and-certified-kubernetes-application-developer-ckad), [CKS](https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed#certified-kubernetes-security-specialist-cks).
* You are allowed to use pre-created bookmarks to any page in the allowed documentation.
* You will be penalised if you view a page with is *not* within the allowed documentation.

## The Exam Portal

Once the proctor is satified and launches the exam, this is what you will get.

* You only get one exam terminal. If you want multiple terminals you must use [tmux](https://github.com/tmux/tmux/wiki) which is pre-installed in the exam environment. 4K monitor is bonus here so you're not stuck with really small panes.
* The `k` alias and bash autocomplete for `kubectl` are also pre-installed. You only need to add other aliases and exports to help you.
* Editors `vim` (`vi`) and `nano` are pre-intstalled
* You may not install additional software from package repos or other locations except when directed by an exam question, and only from the links it gives you.
    * **NOTE** You won't be asked to install anything (e.g. CNI plugins) for which a link isn't present in the allowed docs. You will be provided with a link in the question.


## My Personal Preferences

You are not allowed to paste any settings into the terminal (e.g. aliases, dotfiles etc) from another source. You must commit all these to memory and type them in at the beginning.

I found that as soon as the portal was launched, and while the environment was creating that I could start typing these into the exam notepad. By the time the command prompt appeared, I was mostly done and it was a simple copy/paste from the exam notepad to the terminal. This will save you up to a minute depending on how many alaises, config items etc you want to use.

### Preventing Early Exit from the Exam

If you exit the main terminal, then the proctor has to get you back in. The clock does *not* stop while this happens. Prevent this happening to you by entering these commands at the very first command prompt. This is the main exam terminal to which you should return after any question has had you ssh to another node.

```shell
set -o ignoreeof
alias exit='echo "No exit here!"
```

The first command prevents `CTRL`+`D` from exiting the shell; the second prevents the `exit` command from running and instead prints a message.

### Configuring VIM

I'm no `vim` expert, but these settings work well for YAML editing. If you type it up as follows into the exam notepad, you can paste straight to the command prompt

```shell
cat <<EOF > ~/.vimrc
set nu
set sw=2
set et
set ts=2
set ai
set pastetoggle=<F3>
EOF
```

What these do, in order:

1. Enable line numbers
2. Set shift width 2 chars
3. Expand tabs to spaces
4. Set tab stop to 2 chars
5. Enable auto indent
6. Set F3 key to toggle paste mode. This is super important when pasting from the Kubernetes docs. Enter insert mode `i` then press `F3` so the bottom line reads<br>`INSERT (paste)`<br>Once you've pasted, ensure to toggle paste mode OFF again, or `TAB` key will start inserting tab characters and `kubectl` will complain! 
