# Tips for CKA-CKAD-CKS
Quick tips on exam-day preparation.

The Certified Kubernetes exams are all online-proctored. This means that you do them from your own workstation, not at a test centre, while connected to a proctor who is watching you through your camera and your terminal via screen share.

They are also performance based. This means that you have to solve somewhere between 17 and 25 questions using a Linux terminal provided in the exam portal via your browser. So you have no nice GUI editors like VSCode etc - just `vim` or `nano` text based editors. You will need to get fast at editing YAML files in these editors!

# Am I Ready?

Always the burning question!

I think take the following into consideration.

* You can complete the mock exams and lightning labs (KodeKloud/Udemy Mumshad Mannambeth courses) faster than the instructor (where a solution video is posted) with no errors. Generally this means 20-30 min depending on the test.
* Now buy your exam. Wait for a decent coupon code to come up - these are always publicised on the KodeKloud slack channels. You have a year to actually schedule it.
* Do one of your two attempts at killer.sh. Reset it as many times as necessary in the 36 hours you have. You're aiming to complete it within 10 points of maximum score ideally in little more than 90 minutes. Killer is arguably *harder* than the real exam!
    * If you achieve that on the first session, you're probably ready.
    * If you don't - read and understand the killer solutions, go back, revise the lectures, redo the labs, give it a few weeks.
* Schedule the exam for say two weeks in the future
* Between scheduling and taking, do the second killer session. You will get the same questions so it should be easy this time.
* Take the exam - good luck!

# Proctor and Workspace

* Allow at least 15-20 minutes from when you first connect with the proctor to them actually launching the exam! The better prepared your work area is, the less fuss there will be and the sooner the proctor will launch the exam.
* Make sure there are no objects (other than furniture) within 2 metres of where you are sitting, other than the computer equipment required for the exam. You are also allowed water in a clear glass. No pens, paper, books, electronics or any other clutter or anything with text on (that could be seen by proctor as a cheat sheet), including on the walls.
* Remove smart watches.
* Make sure you can move your camera. Proctor will want a 360 degree sweep of the area, and will want to see under your desk.
* If there are removable drawers in your desk, best to remove them.
* Anything that's not easily moved like a big bookshelf, throw a sheet over it.
* The jury is out as to whether you can have two monitors, though given the requirements for what you can run, detailed in the next section, there's little point in it so better to disconnect/remove additional monitors. If using a laptop with connected external monitor, set external as primary and work with laptop lid closed if the external monitor is better although this will require you to have a plug-in USB camera - or remove external monitor and work on laptop only.
* If you live in an area with a high chance of power cuts, consider tethering your laptop to your phone. Ensure both are fully charged and will last the (anything up to 3 hours) required including proctor setup. If you have a desktop computer consider buying a small UPS.
* If you have made changes to your normal environment to fit the exam conditions (e.g. any of the above), test it thoroughly and ensure the exam compatibility check (on the exam scheduling page) is happy.

# Your Workstation

* You may only use Chrome or Chromium browser for full compatibility with exam interface and required screen share plugin.
* You may only have one instance of this running, and no other foreground tasks. Proctor will likely ask you to run up your system's task manager application to verify this.
* You may have one additional browser tab open to view allowed documentation [CKA/CKAD](https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed#certified-kubernetes-administrator-cka-and-certified-kubernetes-application-developer-ckad), [CKS](https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed#certified-kubernetes-security-specialist-cks).
* You are allowed to use pre-created bookmarks to any page in the allowed documentation.
* You will be penalised if you view a page with is *not* within the allowed documentation.
* You do not need to hide or remove bookmarks not relevant to the exam, you just have to not use them. Best to arrange all your exam documentation under a single bookmark folder.

# The Exam Portal

Once the proctor is satisfied and launches the exam, this is what you will get.

* You only get one exam terminal. If you want multiple terminals you must use [tmux](https://github.com/tmux/tmux/wiki) which is pre-installed in the exam environment. 4K monitor is bonus here so you're not stuck with really small panes.
* The `k` alias and bash autocomplete for `kubectl` are also pre-installed. You only need to add other aliases and exports to help you.
* Editors `vim` (`vi`) and `nano` are pre-installed.
* The portal includes a notepad feature (access from a menu top right) into which you can make notes during the exam. Pen and paper is not allowed.
* You may not install additional software from package repos or other locations except when directed by an exam question, and only from the links it gives you.
    * **NOTE** You won't be asked to install anything (e.g. CNI plugins) for which a link isn't present in the allowed docs. You will be provided with a link in the question.

**PRO TIP** Know as many imperative commands as you can. This will reduce the amount of YAML editing you need to do. For example if you are asked to create an nginx pod and set up a volume mount inside it, create the pod imperatively, then only make necessary edits to YAML to add the volume...

```shell
kubectl run my-pod --image=nginx --dry=run=client -o yaml > my-pod.yaml
vi my-pod.yaml
kubectl create -f my-pod.yaml
```

For objects that can't be created imperatively like Persistent Volumes, it is useful to have bookmarks directly to the YAML for these so you can copy/paste them before editing.

# Exam Environment Configuration

You are not allowed to paste any settings into the terminal (e.g. aliases, dotfiles etc) from another source. You must commit all these to memory and type them in at the beginning.

I found that as soon as the portal was launched, and while the environment was creating that I could start typing these into the exam notepad. By the time the command prompt appeared, I was mostly done and it was a simple copy/paste from the exam notepad to the terminal. This will save you up to a minute depending on how many aliases, config items etc you want to use.

Below are my personal preferences. You can and should practice these in all popular lab environments like KodeKloud and Killercoda and also when you get to it, killer.sh.

## Preventing Early Exit from the Exam

If you exit the main terminal, then the proctor has to get you back in. The clock *does not stop* while this happens so you will lose valuable time. Prevent this happening to you by entering these commands at the very first command prompt. Do this absolutely as the first task - before adding any personal configuration or attempting any question. Do *not* run these in any other terminal (e.g. inside `tmux`) or node you ssh to, or you will find it hard to get back out - absolutely *only* in the very first command prompt when the exam starts.

```shell
set -o ignoreeof
alias exit='echo No!'
```

The first command prevents `CTRL`-`D` from exiting the shell; the second prevents the `exit` command from running and instead prints a message.

## VIM (VI)

I'm no `vim` expert, but these settings work well for YAML editing. If you type it up as follows into the exam notepad, you can paste straight to the command prompt.

Note that in the exam environment `vi` is aliased to `vim`. `vi` is an older editor and does not read the following configuration.
In KodeKloud Alpine environments, this alias is not usually present so you must either create it or explicitly type `vim`

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

## TMUX

[tmux](https://github.com/tmux/tmux/wiki) allows you to have multiple terminal panes in the exam environment. I personally use two. With two panes you can do the following which will save you time, however `tmux` isn't for the faint hearted. If you don't know it, you must practice it *a lot* in lab environments!

* When debugging a YAML manifest, have the YAML open in `vi` in one pane, and a command prompt in the other...
    1. Make edits to YAML
    1. Save changes with `:w`
    1. In other pane `kubectl apply -f ...`
    1. If error in YAML repeat the above till it works
* Where a question asks you to ssh to other nodes e.g. when doing a cluster upgrade, you can have one prompt on the control plane and the other on a worker node.

### Installing in lab environments

Update: It seems that `tmux` may now be installed by default in KodeKloud labs. You can check in any lab environment (KK or otherwise) by running

```shell
which tmux
```

If not, then proceed with the following:

While `tmux` *is* preinstalled in the real exam and on killer.sh, in many lab environments it is not installed by default. To install it at the start of a lab session, do the following

1. Determine the OS distribution<br>`cat /etc/os-release`
1. If Ubuntu, run<br>`apt update && apt install tmux`
1. If Alpine, run<br>`apk add tmux`

### Configuration

I am certainly not a `tmux` ninja, but these settings work. If you type it up as follows into the exam notepad, you can paste straight to the command prompt.

```shell
cat <<EOF > ~/.tmux.conf
set -g mouse on
set -g default-shell /bin/bash
EOF
```

These settings enable the mouse for pane selection and copy-paste operations, plus ensure the shell is `bash` (otherwise it could use another default like `sh`).

Run `tmux` at the main exam terminal after performing the above Early Exit, `vim` and `tmux` configurations.

* To create a two-pane view with a horizontal split, type `CTRL`-`B` followed by `"`
* To create a vertical split, type `CTRL`-`B` followed by `%`
* Cancel a split by typing `CTRL`-`D` or `exit` at one of the command prompts
* Switch between panes by left mouse click
* If you have enough screen real estate (eg. 4K monitor), you can create splits within splits by repeating the above key sequences, however I find that two panes is generally sufficient.

**PRO TIP** The best place to practice `tmux` skills is on [Killercoda](https://killercoda.com/areas). This platform is by the same people that create killer.sh, therefore it is the closest you'll get to the real exam user interface - including the quirkiness of `tmux` which is slightly different in say KodeKloud.

### Quirks

For copying, pasting and selecting text to copy, be sure to hold the shift key when using the mouse to override `tmux` default mouse behaviour.

## Creating and using your own aliases and exports

You may want to do this to gain extra speed, for instance

```shell
alias kgp=`kubectl get pods`
export dry='--dry-run=client -o yaml`
```

...etc.

Again, type these to the exam notepad so you can paste them to command prompts. Since these are shell settings you need to paste them at every new shell you run - that means all panes you create in `tmux`, plus any node you ssh to if you expect to use `kubectl` commands at that node.

# Links

## Pre-Exam

* [Exam System Requirements](https://docs.linuxfoundation.org/tc-docs/certification/faq-cka-ckad-cks#what-are-the-system-requirements-to-take-the-exam)
* [Exam Workspace Requirements](https://docs.linuxfoundation.org/tc-docs/certification/faq-cka-ckad-cks#what-are-the-testing-environment-requirements-to-take-the-exam)
* [Exam ID requirements](https://docs.linuxfoundation.org/tc-docs/certification/faq-cka-ckad-cks#what-are-the-id-requirements-to-take-the-exam)

## CKA/CKAD

* [Exam Environment](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad#cka-and-ckad-environment)
* [Allowed Documentation](https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed#certified-kubernetes-administrator-cka-and-certified-kubernetes-application-developer-ckad)

## CKS
* [Exam Environment](https://docs.linuxfoundation.org/tc-docs/certification/important-instructions-cks#cks-environment)
* [Allowed Documentation](https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed#certified-kubernetes-security-specialist-cks)

## Other

* [vim Cheat Sheet](https://vim.rtorr.com/)
* [tmux Cheat Sheet](https://opensource.com/article/20/7/tmux-cheat-sheet)
* [Useful Exam Bookmarks](https://github.com/vjunior1981/cka-2022-bookmarks) - Courtesy of Vitor Jr. (KodeKloud)

## Specific Questions About The Exam
* [Specific Questions About Exam](https://trainingsupport.linuxfoundation.org/). Login here with your Linux Foundation credentials. You can raise a ticket to ask questions about anything to do with the exam. The answers you receive here are the ultimate source of truth and trump anything you may read on this page or in any public discussion forums. Expect 2-3 days for a response.

If you receive an answer from the LF ticketing system that contradicts anything you read on this page, or if you feel anything I've written here is incorrect or misleading, feel free to raise a pull request.
