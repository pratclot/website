+++
title = 'IP Camera Mail Relay'
date = 2024-03-09T22:01:22+01:00
+++

I ran an Odroid C2 off site for periodic temperature measurements, relay control via GPIO and a mail relay for IP cameras. It served me well for about 7 years with no maintenance needed.

There was a moment when Google deprecated SSL on their mail servers, and that made it impossible for Hikvision IP cams to send me pictures. Thankfully, it was possible to quickly hack together a relay on Odroid using Postfix which saved the day and worked ever since.