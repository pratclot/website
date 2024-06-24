+++
title = 'Using Talon From Scratch'
date = 2024-03-21T16:03:46+01:00
draft = true
+++

when I play heroes I need to hold control shift or alt for some time and perform clicks. This can be achieved with custom voice commands:

```talon
hold control shift:
    key(ctrl:down)
    key(shift:down)
    
release control shift:
    key(ctrl:up)
    key(shift:up)
```
