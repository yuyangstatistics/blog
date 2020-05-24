---
title: Emacs Configuration
date: 2020-04-10 12:28:12 -0500
categories: [Tools]
tags: [emacs]
---
References:
- [Markdown Mode for Emacs](https://jblevins.org/projects/markdown-mode/)
- [Emacs: The Best Python Editor?](https://realpython.com/emacs-the-best-python-editor/)
- [Zenburn for Emacs](https://github.com/bbatsov/zenburn-emacs)

## Key settings
- Set `Command` as the meta key.
  ```lisp
  ;; key bindings
  (when (eq system-type 'darwin) ;; mac specific settings
	  (setq mac-option-modifier 'meta)
	  )
  ```
- Switch `Ctrl` and `Caps Lock` in System settings. `Caps Lock` is used less often and is more convient for Emacs use based on my habit.

## Initialization file settings

Before installing the required emacs packages, run `M-x list-packages` to upgrade packages.

After testing different themes, including doom themes, the default material theme, and many other themes in [MELPA](https://melpa.org/#/), I chose zenburn-theme. It is easy on my eyes and the coloring scheme fits me. Run `M-x package-install <Return> zenburn-theme` to install the package.

The following is my `~/.emacs` file. Check the comments for details.

```lisp
;; ==================  Update date: Apr. 10  ==================
;; set the spacing format of line numbers
(setq linum-format "%4d \u2502")
;; silence warnings about python indentation
(setq python-indent-guess-indent-offset-verbose nil)

;; show which parenthesis matches the one you are looking at
(show-paren-mode 1)
;; auto close bracket insertion
(electric-pair-mode 1)
;; ==============   Update date: Apr. 10  ==============
;; Reference: https://realpython.com/emacs-the-best-python-editor/
;; ===================================
;; MELPA Package Support
;; ===================================
;; Enables basic packaging support
(require 'package)

;; Adds the Melpa archive to the list of available repositories
(add-to-list 'package-archives
             '("melpa" . "http://melpa.org/packages/") t)

;; Initializes the package infrastructure
(package-initialize)

;; Installs packages
;;
;; myPackages contains a list of package names
(defvar myPackages
  '(better-defaults                 ;; Set up some better Emacs defaults
    elpy                            ;; Emacs Lisp Python Environment
    flycheck                        ;; On the fly syntax checking
    ein                             ;; Emacs IPython Notebook
    material-theme                  ;; Theme
    doom-themes                     ;; Doom-Themes
    )
  )

;; Scans the list in myPackages
;; If the package listed is not already installed, install it
(mapc #'(lambda (package)
          (unless (package-installed-p package)
            (package-install package)))
      myPackages)

;; ===================================
;; Basic Customization
;; ===================================
(setq inhibit-startup-message t)    ;; Hide the startup message
(load-theme 'zenburn t)          ;; Load Doom dark+ theme
;;(load-theme 'material t)            ;; Load material theme
(global-linum-mode t)               ;; Enable line numbers globally

;; ====================================
;; Development Setup
;; ====================================
;; Enable elpy
(elpy-enable)

;; Use IPython for REPL
(setq elpy-shell-echo-output nil
      python-shell-interpreter "ipython3"
      python-shell-interpreter-args "--simple-prompt -c exec('__import__(\\'readline\\')') -i")

;; Enable Flycheck
(when (require 'flycheck nil t)
  (setq elpy-modules (delq 'elpy-module-flymake elpy-modules))
  (add-hook 'elpy-mode-hook 'flycheck-mode))

;; User-Defined init.el ends here
(custom-set-variables
 ;; custom-set-variables was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 '(package-selected-packages
   (quote
    (markdown-mode zenburn-theme doom-themes material-theme better-defaults))))
(custom-set-faces
 ;; custom-set-faces was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 )


;; ===================  Update date: Apr. 8  ================
;; key bindings
(when (eq system-type 'darwin) ;; mac specific settings
  (setq mac-option-modifier 'meta)
  )
```









