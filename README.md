# *minimal-emacs.d* - A Customizable Emacs `init.el` and `early-init.el` that Provides Better Defaults and Faster Startup
![](https://jamescherti.com/misc/made-for-gnu-emacs.svg)
![Build Status](https://github.com/jamescherti/minimal-emacs.d/actions/workflows/ci.yml/badge.svg)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

## Introduction

The **minimal-emacs.d** project is a lightweight and optimized Emacs base (`init.el` and `early-init.el`) that **gives you full control over your configuration** (without the complexity of, for instance, Doom Emacs or Spacemacs). It provides better defaults, an optimized startup, and a clean foundation for building your own vanilla Emacs setup.

Building the *minimal-emacs.d* `init.el` and `early-init.el` was the result of **extensive research and testing** to fine-tune the best parameters and optimizations for an Emacs configuration. *(More information about the *minimal-emacs.d* features can be found here: [Features](#features).)*

<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
## Table of Contents

- [*minimal-emacs.d* - A Customizable Emacs `init.el` and `early-init.el` that Provides Better Defaults and Faster Startup](#minimal-emacsd---a-customizable-emacs-initel-and-early-initel-that-provides-better-defaults-and-faster-startup)
    - [Introduction](#introduction)
    - [Looking for the ideal starter kit to customize Emacs? You have found it.](#looking-for-the-ideal-starter-kit-to-customize-emacs-you-have-found-it)
        - [Startup](#startup)
    - [Install minimal-emacs.d](#install-minimal-emacsd)
        - [Install minimal-emacs.d into `~/.emacs.d`](#install-minimal-emacsd-into-emacsd)
        - [Alternative: Install minimal-emacs.d into `~/.minimal-emacs.d`](#alternative-install-minimal-emacsd-into-minimal-emacsd)
    - [Update minimal-emacs.d](#update-minimal-emacsd)
    - [Customizations: Never modify init.el and early-init.el. Modify these instead...](#customizations-never-modify-initel-and-early-initel-modify-these-instead)
    - [Debug on error](#debug-on-error)
    - [Customizations: UI (pre-early-init.el)](#customizations-ui-pre-early-initel)
        - [How to enable the menu-bar, the tool-bar, dialogs, the contextual menu, and tooltips?](#how-to-enable-the-menu-bar-the-tool-bar-dialogs-the-contextual-menu-and-tooltips)
        - [Reducing clutter in `~/.emacs.d` by redirecting files to `~/.emacs.d/var/`](#reducing-clutter-in-emacsd-by-redirecting-files-to-emacsdvar)
    - [Customizations: Packages (post-init.el)](#customizations-packages-post-initel)
        - [Optimization: Native Compilation](#optimization-native-compilation)
        - [How to activate recentf, savehist, saveplace, and auto-revert?](#how-to-activate-recentf-savehist-saveplace-and-auto-revert)
        - [Activating autosave](#activating-autosave)
            - [auto-save-mode (Prevent data loss in case of crashes)](#auto-save-mode-prevent-data-loss-in-case-of-crashes)
            - [auto-save-visited-mode (Save file buffers after a few seconds of inactivity)](#auto-save-visited-mode-save-file-buffers-after-a-few-seconds-of-inactivity)
        - [Code completion with corfu](#code-completion-with-corfu)
        - [Configuring Vertico, Consult, and Embark](#configuring-vertico-consult-and-embark)
        - [Code folding](#code-folding)
        - [Changing the default theme](#changing-the-default-theme)
        - [Automatic removal of trailing whitespace on save](#automatic-removal-of-trailing-whitespace-on-save)
        - [Enhancing undo/redo](#enhancing-undoredo)
        - [Configuring Vim keybindings using Evil?](#configuring-vim-keybindings-using-evil)
        - [Configuring LSP Servers with Eglot (built-in)](#configuring-lsp-servers-with-eglot-built-in)
        - [Persisting and Restoring all buffers, windows/split, tab-bar, frames...](#persisting-and-restoring-all-buffers-windowssplit-tab-bar-frames)
        - [Configuring org-mode](#configuring-org-mode)
        - [Configuring markdown-mode (e.g., README.md syntax)](#configuring-markdown-mode-eg-readmemd-syntax)
        - [Tree-sitter Integration (Better Syntax Highlighting)](#tree-sitter-integration-better-syntax-highlighting)
        - [Auto upgrade Emacs packages](#auto-upgrade-emacs-packages)
        - [Safely terminating unused buffers](#safely-terminating-unused-buffers)
        - [Treemacs, a tree layout file explorer (Sidebar file explorer)](#treemacs-a-tree-layout-file-explorer-sidebar-file-explorer)
        - [Inhibit the mouse](#inhibit-the-mouse)
        - [Spell checker](#spell-checker)
        - [Efficient jumps for enhanced productivity](#efficient-jumps-for-enhanced-productivity)
        - [Asynchronous code formatting without cursor disruption](#asynchronous-code-formatting-without-cursor-disruption)
        - [Efficient template expansion with snippets](#efficient-template-expansion-with-snippets)
        - [A better Emacs *help* buffer](#a-better-emacs-help-buffer)
        - [Enhancing the Elisp development experience](#enhancing-the-elisp-development-experience)
        - [Showing the tab-bar](#showing-the-tab-bar)
        - [Changing the Default Font](#changing-the-default-font)
        - [Persist Text Scale](#persist-text-scale)
        - [Loading the custom.el file](#loading-the-customel-file)
        - [Which other customizations can be interesting to add?](#which-other-customizations-can-be-interesting-to-add)
    - [Customizations: pre-early-init.el](#customizations-pre-early-initel)
        - [Configuring straight.el](#configuring-straightel)
        - [Configuring Elpaca (package manager)](#configuring-elpaca-package-manager)
    - [Frequently asked questions](#frequently-asked-questions)
        - [Customizing Scroll Recentering](#customizing-scroll-recentering)
        - [How to display Emacs startup duration?](#how-to-display-emacs-startup-duration)
        - [How to get the latest version of all packages? (unstable)](#how-to-get-the-latest-version-of-all-packages-unstable)
        - [How to use MELPA stable?](#how-to-use-melpa-stable)
        - [How to load a local lisp file for machine-specific configurations?](#how-to-load-a-local-lisp-file-for-machine-specific-configurations)
        - [How to prevent Emacs from repeatedly performing native compilation on specific Elisp files](#how-to-prevent-emacs-from-repeatedly-performing-native-compilation-on-specific-elisp-files)
        - [How to load Emacs customizations?](#how-to-load-emacs-customizations)
        - [How to increase gc-cons-threshold?](#how-to-increase-gc-cons-threshold)
        - [How to prevent Emacs from loading .dir-locals.el files?](#how-to-prevent-emacs-from-loading-dir-localsel-files)
        - [How to make minimal-emacs.d use an environment variable to change ~/.emacs.d to another directory?](#how-to-make-minimal-emacsd-use-an-environment-variable-to-change-emacsd-to-another-directory)
        - [Are post-early-init.el and pre-init.el the same file in terms of the logic?](#are-post-early-initel-and-pre-initel-the-same-file-in-terms-of-the-logic)
        - [Why is the menu bar disabled by default?](#why-is-the-menu-bar-disabled-by-default)
        - [Why did the author develop minimal-emacs.d?](#why-did-the-author-develop-minimal-emacsd)
        - [How to keep minimal-emacs.d pre-\*.el and post-\*.el files in a separate directory?](#how-to-keep-minimal-emacsd-pre-el-and-post-el-files-in-a-separate-directory)
        - [How to make *minimal-emacs.d* install packages in the early-init phase instead of the init phase?](#how-to-make-minimal-emacsd-install-packages-in-the-early-init-phase-instead-of-the-init-phase)
        - [Testimonials from users](#testimonials-from-users)
        - [Minimal-emacs.d configurations from users](#minimal-emacsd-configurations-from-users)
    - [Features](#features)
    - [Author and license](#author-and-license)
    - [Links](#links)

<!-- markdown-toc end -->

## Install minimal-emacs.d

- **Important:** Ensure that the `~/.emacs` and `~/.emacs.el` files do not exist. These files cause Emacs to ignore `~/.emacs.d/init.el`. This behavior is due to the way Emacs searches for initialization files ([more information](https://www.gnu.org/software/emacs/manual/html_node/emacs/Find-Init.html#Find-Init)). **Simply delete the *~/.emacs* and *~/.emacs.el* files avoid this issue.**
- **Debug:** If a package or any other functionality is not working as expected, start Emacs with `emacs --debug-init` to enable debug mode and obtain the backtrace.
- **Prerequisite:** git

### Install minimal-emacs.d into `~/.emacs.d`

Execute the following command install this repository into `~/.emacs.d`:
```
git clone --depth 1 https://github.com/jamescherti/minimal-emacs.d ~/.emacs.d
```

## Customizations: Never modify init.el and early-init.el. Modify these instead...
**The `init.el` and `early-init.el` files should never be modified directly** because they are intended to be managed by Git during an update.

The minimal-emacs.d init files support additional customization files that are loaded at different stages of the Emacs startup process. These files allow you to further customize the initialization sequence:

- `~/.emacs.d/pre-init.el`: This file is loaded before `init.el`. Use it to set up variables or configurations that need to be available early in the initialization process but after `early-init.el`.

- `~/.emacs.d/post-init.el`: This file is loaded after `init.el`. It is useful for additional configurations or package setups that depend on the configurations in `init.el`.

- `~/.emacs.d/pre-early-init.el`: This file is loaded before `early-init.el`. Use it for configurations that need to be set even earlier in the startup sequence, typically affecting the initial setup of the Emacs environment.

- `~/.emacs.d/post-early-init.el`: This file is loaded after `early-init.el` but before `init.el`. It is useful for setting up configurations that depend on the early initialization but need to be set before the main initialization begins.

Always begin your `pre-init.el`, `post-init.el`, `post-early-init.el`, and `pre-early-init.el` files with the following header to prevent them from being byte-compiled and to activate lexical binding:
```elisp
;;; FILENAME.el --- DESCRIPTION -*- no-byte-compile: t; lexical-binding: t; -*-
```

Replace `FILENAME.el` with the actual name and DESCRIPTION with a brief description of its purpose.

*(Only if you know what you're doing: Removing `no-byte-compile: t;` from your init files allows Emacs to compile them, improving load and execution speed. However, if you do so, you may need to add required dependencies. For example, if you're using `use-package`, add `(require 'use-package)` at the top of `post-init.el` to ensure all necessary `use-package` variables and functions are loaded.)*

**Important:** The examples in this README reference pre/post init files in the `~/.emacs.d/` directory, but the files `pre-early-init.el`, `post-early-init.el`, `pre-init.el`, and `post-init.el` should be placed in the same directory as `init.el` and `early-init.el`, regardless of their location.

## Debug on error

During the development of your init files, the author strongly recommends adding the following line at the very beginning of your `~/.emacs.d/pre-early-init.el` file:

```elisp
(setq debug-on-error t)
```

Enabling `debug-on-error` at this stage allows you to catch errors that might otherwise cause Emacs to fail silently or behave unpredictably.

## Customizations: UI (pre-early-init.el)

### How to enable the menu-bar, the tool-bar, dialogs, the contextual menu, and tooltips?

**Note:** Enabling the tool-bar or menu-bar may slightly increase your startup time.

To customize your Emacs setup to include various user interface elements, you can use the following settings in your ``~/.emacs.d/pre-early-init.el``:

``` emacs-lisp
(setq minimal-emacs-ui-features '(context-menu tool-bar menu-bar dialogs tooltips))
```

These settings control the visibility of dialogs, context menus, toolbars, menu bars, and tooltips.

### Reducing clutter in `~/.emacs.d` by redirecting files to `~/.emacs.d/var/`

Emacs, by default, stores various configuration files, caches, backups, and other data in the `~/.emacs.d` directory. Over time, this directory can become cluttered with numerous files, making it difficult to manage and maintain.

A common solution to this issue is installing the no-littering package; however, this package is not essential.

An alternative lightweight approach is to simply change the default `~/.emacs.d` directory to `~/.emacs.d/var/`, which will contain all the files that Emacs typically stores in the base directory. This can be accomplished by adding the following code to `~/.emacs.d/pre-early-init.el`:
``` emacs-lisp
;;; Reducing clutter in ~/.emacs.d by redirecting files to ~/.emacs.d/var/
;; NOTE: This must be placed in 'pre-early-init.el'.
(setq user-emacs-directory (expand-file-name "var/" minimal-emacs-user-directory))
(setq package-user-dir (expand-file-name "elpa" user-emacs-directory))
```

**IMPORTANT:** The code above should be added to `~/.emacs.d/pre-early-init.el`, not the other files, as it modifies the behavior of all subsequent init files.
