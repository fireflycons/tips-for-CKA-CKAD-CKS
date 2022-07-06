# Tips for CKA-CKAD-CKS
Quick tips on exam-day preparation.

**IMPORTANT** Beginning June 25 2022, the exam is now delivered via the PSI Secure Browser which is software you must install from a download link provided during the exam registration process. You no longer conduct the exam from your own Chrome browser, therefore you can't use pre-prepared bookmarks.

The Certified Kubernetes exams are all online-proctored. This means that you do them from your own workstation, not at a test centre, while connected to a proctor who is watching you through your camera and your terminal via screen share.

They are also performance based. This means that you have to solve somewhere between 17 and 25 questions using a Linux desktop provided in the exam portal.

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

* Make sure there are no objects (other than furniture) within 2 metres of where you are sitting, other than the computer equipment required for the exam. You are also allowed water in a clear glass. No pens, paper, books, electronics or any other clutter or anything with text on (that could be seen by proctor as a cheat sheet), including on the walls.
* There is now going to be a pre check-in facility where you can upload a photo of yourself, your ID and a video of your work area.
* Remove smart watches.
* If there are removable drawers in your desk, best to remove them.
* Anything that's not easily moved like a big bookshelf, throw a sheet over it.

# Your Workstation

* Since this is a custom browser, you do not have the ability to use pre-prepared bookmarks.
* Make sure you can move your camera.
* Multiple monitors are not allowed as of June 2022. If you have more than one monitor, remove the others. If you have a laptop with an external monitor and the external monitor is better than the laptop display, then you must work with the laptop lid closed ensuring that the laptop display is disabled (your display settings should only register the external monitor), and connect USB keyboard/mouse/camera.
* If you live in an area with a high chance of power cuts, consider tethering your laptop to your phone. Ensure both are fully charged and will last the (anything up to 3 hours) required including proctor setup. If you have a desktop computer consider buying a small UPS. Make sure that if you are tethering to mobile, that your mobile is well out of reach, covered and in silent mode.<br>**IMPORTANT** This method has not yet been proven, so raise a ticket with Linux Foundation to check that use of phone wi-fi is acceptable.
* If you have made changes to your normal environment to fit the exam conditions (e.g. any of the above), test it thoroughly in advance of exam day!
* You are _strongly_ recommended to use a high-res monitor, e.g. 4K or close. If you're only using a standard 1920x1080 HD display, you will get very little screen real-estate for the Linux desktop environment, due to the side panel for the questions, and the control menu bar at the top.
* On a lighter note, there *should* be fewer issues connecting with the proctor and getting screen sharing working.

Additionally

* Log into your computer using an account with Admin/root privilege - you'll need it during preparation.

# Launching the Exam.

You are allowed to launch the session 30 minutes before your scheduled time. You will need all those 30 minutes, so connect promptly, as before you even talk to the proctor, you need to complete the self check-in process. This goes as follows:

* Use the link provided to download the PSI software
* Install and run it
* It will then do a system check - here is where you will need your admin privileges!
    * It will check only one monitor is active
    * It will then check for programs that should not be running, some of which may be operating system services. You have to stop all these things and keep re-running the check until it is happy. This includes, but is not limited to
        * Any foreground process other than the PSI software
        * Hypervisor services
        * Command prompts (even if they are started by a service). This got me for a bit, as I had an Icecast server running as a service and this opened an invisible command prompt.
        * Services related to interfacing with phones.
* Now you have to do all the photo and video fun! It is well worth having an external camera on a USB port with a fairly long cable for this. All the video segments record for 15 seconds. You get the option to re-take or continue after each photo and video. You have to
   1. Take a photo of your ID
   1. Perform a 360 degree sweep of the room beginning with the wall on your left
   1. Perform a sweep of your desk area from floor up to ceiling
   1. Perform a sweep of your desktop from left to right, finishing with showing your phone and then placing it out of reach behind you.
   1. Perform a sweep of your head, showing both ears (they're looking for ear buds), and any eye wear.
   1. Perform a sweep of both wrists to prove the absence of smart-wear.
   1. Take a photo of your face, sort of passport perspective.
* Once you have completed all the above, you then wait until the proctor activates the chat window and gives final instructions. If you have followed all of the above well, then the proctor should allow you to proceed to the exam, otherwise he may ask you to re-show him stuff with the camera/move stuff etc.

# The Exam Portal

Once the proctor is satisfied and launches the exam, this is what you will get.

* The "base node", i.e. the system from which you conduct the exam is an XFCE desktop on Ubuntu 20.04. It is entered via the Remote Desktop control near the top.
* You are allowed to use any of the utilities that are included with the desktop, which includes and is not limited to
    * `Terminal Emulator` - you may open as many terminal windows as you like.
    * `File Manager` - May or may not be of use. Remember that it can only see the file system of the desktop host, not any other host that may be involved in the exam. Note also that the host that the terminal emulator opens on is _not_ the desktop host. I have tested this - any files created in the home directory in the terminal do not show in the home directory that File Manager is looking at!
    * `Text Editor` - (called `Mousepad`) can be used to take notes in place of the old Exam Notepad. **Remember** that the desktop filesystem is _not_ the same file system as the terminal emulator, so you can't edit YAML in this then expect to find the saved file in the terminal's filesystem!
    * `Firefox` - is included on the desktop for viewing documentation. They helpfully pass this through a proxy which blocks access to all but permitted documentation, so no chance of accidentally going elsewhere. You may open multiple tabs in Firefox.
* Links to documentation, *considered most helpful to complete your work*, have been added to a Quick Reference box within each item’s instructions. Clicking on any of these links opens a tab in Firefox.
* The `k` alias and bash autocomplete for `kubectl` are also pre-configured, so will function in all terminal windows launched. You only need to add other aliases and exports to help you.
* Editors `vim` (`vi`) and `nano` are pre-installed.
* You may not install additional software from package repos or other locations except when directed by an exam question, and only from the links it gives you.
    * **NOTE** You won't be asked to install anything (e.g. CNI plugins) for which a link isn't present in the allowed docs. You will be provided with a link in the question.
* Until such time as killer.sh update their user interface, it will no longer be a close representation of the real exam environment, however they are now working on it - [preview here](https://killercoda.com/kimwuestkamp/scenario/cks-cka-ckad-remote-desktop). You should still do killer though, even on the old UI for the question experience.

**A note about Terminal Emulator**

If it is running as root, then you may get a nag dialog when pasting text from another application. You can disable this with

```
Edit -> Preferences
```

...then uncheck `Show unsafe paste dialog`, bottom right near Close button.

## Issues with the Exam Portal

Since the launch of the new portal, many issues have been raised about lag (unresponsiveness of the desktop), copy/paste issues and the like. Personally (and having to use an Amazon Workspace in my job), I found the lag was about as expected. There were issues with the exam portal not being launched in the examinee's closest cloud region, but I think those have been resolved now.

As for copy/paste:
* To copy from the question panel, click `Copy` link with the mouse where it is present, else a click on highlighted text auto-copies it (even when the `Copy` link appears with mouse hover - you can't actually click that).
* To copy and paste _within_ the desktop, it's easiest to use the right-click context menu - I know some of you would prefer to use keyboard shortcuts.
* Shift + double click will select words, filepaths etc in the terminal.
* I could not get `pastetoggle` to work in `vi` for some reason. This means you have to enter the `:set paste` and `:set nopaste` commands in normal mode.

Please read https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/exam-user-interface.

**PRO TIP** Know as many imperative commands as you can. This will reduce the amount of YAML editing you need to do. For example if you are asked to create an nginx pod and set up a volume mount inside it, create the pod imperatively, then only make necessary edits to YAML to add the volume...

```shell
kubectl run my-pod --image=nginx --dry=run=client -o yaml > my-pod.yaml
vi my-pod.yaml
kubectl create -f my-pod.yaml
```

# Exam Environment Configuration

You are not allowed to paste any settings into the terminal (e.g. aliases, dotfiles etc) from another source. You must commit all these to memory and type them in at the beginning.

Below are my personal preferences. You can and should practice these in all popular lab environments like KodeKloud and Killercoda and also when you get to it, killer.sh.

## VIM (VI)

Since the exam desktop does not come with an IDE (VSCode, Intellij etc.) I would still advise you to use `vi` in a terminal window for YAML editing, as if you know your `vi` commands, it's easier to get the formatting right.

Note that in the exam environment `vi` is aliased to `vim`. `vi` is an older editor and does not read the following configuration. In KodeKloud Alpine environments, this alias is not always present so you must either create it or explicitly type `vim`

I'm no `vi` expert, but these settings work well for YAML editing.

In a terminal at the start of the exam, do `vi ~./vimrc`, enter up the following and save

```shell
set nu
set sw=2
set et
set ts=2
set ai
set pastetoggle=<F3>
```

What these do, in order:

1. Enable line numbers
2. Set shift width 2 chars
3. Expand tabs to spaces
4. Set tab stop to 2 chars
5. Enable auto indent
6. NOTE - this was not working properly as of 2022-07-06. See Issues with Exam Portal section above.<br>Set F3 key to toggle paste mode. This is super important when pasting from the Kubernetes docs. Enter insert mode `i` then press `F3` so the bottom line reads<br>`INSERT (paste)`<br>Once you've pasted, ensure to toggle paste mode OFF again, or `TAB` key will start inserting tab characters and `kubectl` will complain!

## TMUX

With the new GUI desktop-based exam environment, use of `tmux` is somewhat deprecated as you can open multiple terminal windows. The one scenario where it is still useful is the case where you may want to enter the [same sequence of commands](https://medium.com/@thehackadda/synchronize-panes-in-tmux-5cd6bc54ca83) at more than one node simultaneously. Ensure you have `ssh`-ed to the target nodes in each pane before activating sync.

If you have a low res monitor, such that the desktop area is really small, you may still consider `tmux` in a single terminal window.

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
