---
title: "Setting up Cobol major mode in Emacs with Spacemacs"
layout: # single
author_profile: # true
read_time: # true
comments: # true
share: # true
related: #true
excerpt: # Auto-generated page excerpt is added to the overlay text or can be overridden here.
excerpt_separator: "<!--more-->"
header:
  overlay_color: "#000000" 
  overlay_filter: "0.5" # 1.0 Darkest
  overlay_image: "/assets/images/2018/M05/Cobol-Punch-Card.jpg"
  image_description: "Cobol punch card"
categories:
  - HowTo
tags: 
  - cobol
  - emacs
  - spacemacs
  - mode
last_modified_at: 2018-05-29
---

Edit `.spacemacs` file, go to `dotspacemacs-additional-packages` and include
your packages separated by commas . Then press `<SPC f e r>` (Vim style) or
`<M-m f e r` (Emacs style) to install them without rebooting.

For example, the polymode package has not a configuration layer so you must install as follow:

```emacs-lisp
dotspacemacs-additional-packages '(polymode)
```



Edit `.spacemacs`, go to `dotspacemacs/user-config ()` section and add your
associations as follow in the next example:

```emacs-lisp
(defun dotspacemacs/user-config ()
  "Configuration function for user code.
This function is called at the very end of Spacemacs initialization after
layers configuration.
This is the place where most of your configurations should be done. Unless it is
explicitly specified that a variable should be set before a package is loaded,
you should place your code here."
  
;;; MARKDOWN
;;;  (add-to-list 'auto-mode-alist '("\\.Rmd" . markdown-mode))

;;; MARKDOWN
  (add-to-list 'auto-mode-alist '("\\.md" . poly-markdown-mode))

;;; COBOL
  (add-to-list 'auto-mode-alist '("\\.cob" . cobol-mode))

;;; R modes
  (add-to-list 'auto-mode-alist '("\\.Snw" . poly-noweb+r-mode))
  (add-to-list 'auto-mode-alist '("\\.Rnw" . poly-noweb+r-mode))
  (add-to-list 'auto-mode-alist '("\\.Rmd" . poly-markdown+r-mode))

  )

```


