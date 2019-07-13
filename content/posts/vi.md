---
title: "Vi cheatsheet"
date: 2019-02-24T02:00:53Z
showDate: true
draft: false
tags: ["unix","vi", "tools"]
---

# Navigation

*hjkl:* left/up/down/right

*gg:* move to the start of the file

*Shift+g:* move to the end of file

*w:* move to the start of the next word 

*Shift+e:* move to the end of the next word

*Shift+$* move to the end of the line

*0* move to the start of the line

# Actions

*Esc*: Switch to visual mode

# Text Edit

*i:* Start Editing

*dd:* Delete line

# Commands

*help:* show vi documentation

*/word:* will search for occurences of "word" in the document

*!wq:* Save and exit

*s:* Replace pattern with string according to flags (:s/pattern/string/flags where flags one of g,c)
