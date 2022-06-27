# Tips for CKA-CKAD-CKS
Quick tips on exam-day preparation.

The Certified Kubernetes exams are all online-proctored. This means that you do them from your own workstation, not at a test centre, while connected to a proctor who is watching you through your camera and your terminal via screen share.

They are also performance based. This means that you have to solve somewhere between 17 and 25 questions using a Linux desktop provided in the exam portal via the PSI Secure Browser which you download and install as part of the exam registration process.

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
* There is now going to be a pre check-in facility where you can upload a photo of yourself, your ID and a video of your work area.
* Remove smart watches.
* Make sure you can move your camera. Proctor will want a 360 degree sweep of the area, and will want to see under your desk.
* If there are removable drawers in your desk, best to remove them.
* Anything that's not easily moved like a big bookshelf, throw a sheet over it.
* Multiple monitors are not allowed as of June 2022. If you have more than one monitor, remove the others. If you have a laptop with an external monitor and the external monitor is better than the laptop display, then you must work with the laptop lid closed ensuring that the laptop display is disabled (your display settings should only register the external monitor), and connect USB keyboard/mouse/camera.
* If you live in an area with a high chance of power cuts, consider tethering your laptop to your phone. Ensure both are fully charged and will last the (anything up to 3 hours) required including proctor setup. If you have a desktop computer consider buying a small UPS. Make sure that if you are tethering to mobile, that your mobile is well out of reach, covered and in silent mode.
* If you have made changes to your normal environment to fit the exam conditions (e.g. any of the above), test it thoroughly in advance of exam day!

# Your Workstation

Beginning June 25 2022, the exam is now delivered via the PSI Secure Browser which is software you must install from a download link provided during the exam registration process. There are some important points to note

* Since this is a custom browser, you do not have the ability to use pre-prepared bookmarks.
* The "base node", i.e. the system from which you conduct the exam is an Ubuntu 20.04 desktop environment.
* You are allowed to use any of the utilities that are included with the desktop, which includes and is not limited to
    * `Terminal Emulator` - you may open as many terminal windows as you like.
    * `File Manager`
    * `Text Editor` - you may still prefer to use `vi` in a terminal to edit YAML files, as plain old text editor won't be as smart and may insert TAB characters with will break `kubectl`!
    * `Firefox` - is included on the desktop for viewing documentation. They helpfully pass this through a proxy which blocks access to all but permitted documentation, so no chance of accidentally going elsewhere. You may open multiple tabs in Firefox.
* Links to documentation, *considered most helpful to complete your work*, have been added to a Quick Reference box within each item’s instructions.
* Until such time as killer.sh may or may not update their user interface, it will no longer be a close representation of the real exam environment. You should still do killer though, for the question experience.
* On a lighter note, there should be fewer issues connecting with the proctor and getting screen sharing working.

Additionally

* Ensure no other foreground processes are running.
* If you have phone integration software (e.g. My Phone on Windows), ensure this is disabled.

Please read https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/exam-user-interface.

# The Exam Portal

Once the proctor is satisfied and launches the exam, this is what you will get.

* The `k` alias and bash autocomplete for `kubectl` are also pre-configured, so will function in all terminal windows launched. You only need to add other aliases and exports to help you.
* Editors `vim` (`vi`) and `nano` are pre-installed. You may also use the desktop's Text Editor, but not really recommended for YAML editing.
* The Secure Browser includes a notepad feature (part of Secure Browser and separate from the Linux desktop) into which you can make notes during the exam - you can also use Text Editor on the desktop. Pen and paper is not allowed.
* You may not install additional software from package repos or other locations except when directed by an exam question, and only from the links it gives you.
    * **NOTE** You won't be asked to install anything (e.g. CNI plugins) for which a link isn't present in the allowed docs. You will be provided with a link in the question.

**PRO TIP** Know as many imperative commands as you can. This will reduce the amount of YAML editing you need to do. For example if you are asked to create an nginx pod and set up a volume mount inside it, create the pod imperatively, then only make necessary edits to YAML to add the volume...

```shell
kubectl run my-pod --image=nginx --dry=run=client -o yaml > my-pod.yaml
vi my-pod.yaml
kubectl create -f my-pod.yaml
```

# Exam Environment Configuration

You are not allowed to paste any settings into the terminal (e.g. aliases, dotfiles etc) from another source. You must commit all these to memory and type them in at the beginning.

I found that as soon as the portal was launched, and while the environment was creating that I could start typing these into the exam notepad. By the time the command prompt appeared, I was mostly done and it was a simple copy/paste from the exam notepad to the terminal. This will save you up to a minute depending on how many aliases, config items etc you want to use.

Below are my personal preferences. You can and should practice these in all popular lab environments like KodeKloud and Killercoda and also when you get to it, killer.sh.

## VIM (VI)

Since the exam desktop does not come with an IDE (VSCode, Intellij etc.) I would still advise you to use `vi` in a terminal window for YAML editing, as if you know your `vi` commands, it's easier to get the formatting right.

Note that in the exam environment `vi` is aliased to `vim`. `vi` is an older editor and does not read the following configuration. In KodeKloud Alpine environments, this alias is not always present so you must either create it or explicitly type `vim`

I'm no `vi` expert, but these settings work well for YAML editing. If you type it up as follows into the exam notepad, you can paste straight to the command prompt.

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

With the new GUI desktop-based exam environment, use of `tmux` is somewhat deprecated as you can open multiple terminal windows. The one scenario where it is still useful is the case where you may want to enter the [same sequence of commands](https://medium.com/@thehackadda/synchronize-panes-in-tmux-5cd6bc54ca83) at more than one node simultaneously. Ensure you have `ssh`-ed to the target nodes in each pane before activating sync.

Here is a workable `tmux` configuration that supports mouse selection of panes and `CTRL + X` to toggle sync mode. If using `tmux`, enter the following to a terminal window at the start of the exam.

```shell

cat << EOF > ~/.tmux.conf
set -g default-shell /bin/bash
set -g mouse on
bind -n C-x setw synchronize-panes
EOF
```

## Creating and using your own aliases and exports

You may want to do this to gain extra speed, for instance

```shell
alias kgp='kubectl get pods'
export dry='--dry-run=client -o yaml'
```

...etc.

Since these are shell settings, you will need to add them to `.bashrc` to ensure they are active in all terminal emulators you start, therefore at the beginning of the exam open a terminal and do

```shell
vi ~/.bashrc
```

and add your exports and aliases at the end of the file. Hitting `SHIFT + G` will take you directly to the last line.


# Links

## Pre-Exam

* [Exam System Requirements](https://docs.linuxfoundation.org/tc-docs/certification/faq-cka-ckad-cks#what-are-the-system-requirements-to-take-the-exam)
* [Exam Workspace Requirements](https://docs.linuxfoundation.org/tc-docs/certification/faq-cka-ckad-cks#what-are-the-testing-environment-requirements-to-take-the-exam)
* [Exam ID requirements](https://docs.linuxfoundation.org/tc-docs/certification/faq-cka-ckad-cks#what-are-the-id-requirements-to-take-the-exam)

## All Exams

* [Exam Desktop](https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/exam-user-interface)

## CKA/CKAD

* [Exam Environment](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad#cka-and-ckad-environment)
* [Allowed Documentation](https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed#certified-kubernetes-administrator-cka-and-certified-kubernetes-application-developer-ckad)

## CKS
* [Exam Environment](https://docs.linuxfoundation.org/tc-docs/certification/important-instructions-cks#cks-environment)
* [Allowed Documentation](https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed#certified-kubernetes-security-specialist-cks)

## Other

* [vim Cheat Sheet](https://vim.rtorr.com/)
* [tmux Cheat Sheet](https://opensource.com/article/20/7/tmux-cheat-sheet)

## Specific Questions About The Exam
* [Specific Questions About Exam](https://trainingsupport.linuxfoundation.org/). Login here with your Linux Foundation credentials. You can raise a ticket to ask questions about anything to do with the exam. The answers you receive here are the ultimate source of truth and trump anything you may read on this page or in any public discussion forums. Expect 2-3 days for a response.

If you receive an answer from the LF ticketing system that contradicts anything you read on this page, or if you feel anything I've written here is incorrect or misleading, feel free to raise a pull request.
