# Tips for CKA-CKAD-CKS
Quick tips on preparation for these exams.

The Certified Kubernetes exams are all online-proctored. This means that you do them from your own workstation, not at a test centre while connected to a proctor who is watching you through your camera. 

They are also performance based. This means that you have to solve somewhere between 17 and 25 questions using a Linux terminal provided in the exam portal via your browser. So you have no nice GUI editors like VSCode etc - just `vim` or `nano` text based editors. You will need to get fast at editing YAML files in these editors!

## Environment Outline

* Allow at least 15-20 minutes from when you first connect with the proctor to them actually launching the exam!
* Make sure there is nothing within 2 metres of where you are sitting, other than the computer equipment required for the exam. You are also allowed water in a clear glass. No pens, paper, any other clutter.
* Make sure you can move your camera. Proctor will want a 360 degree sweep of the area, and will want to see under your desk.
* You may only use Chrome or Chromium browser for full compatibiliy with exam interface.
* You may only have one instance of this running, and no other foreground tasks. Proctor will likely ask you to run up your system's task manager application to verify this.
* You may have one additional browser tab open to view allowed documentation [CKA/CKAD](https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed#certified-kubernetes-administrator-cka-and-certified-kubernetes-application-developer-ckad), [CKS](https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed#certified-kubernetes-security-specialist-cks).
* You are allowed to have pre-created bookmarks to any page in the allowed documentation.
* The jury is out as to whether you can have two monitors, though given the above requirements there's little point in it, so better to disconnect/remove additional monitors. If using a laptop with connected external monitor, set external as primary and work with laptop lid closed (this will likely require you to have a plug-in USB camera).
* You only get one exam terminal. If you want multiple terminals you must use [tmux](https://github.com/tmux/tmux/wiki) which is pre-installed in the exam environment. 4K monitor is bonus here so you're not stuck with really small panes.
* The `k` alias and bash autocomplete for `kubectl` are also pre-installed. You only need to add other aliases and exports to help you.
