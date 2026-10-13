# CurrPorts - Which Process Owns an Open Port

## At a Glance

When a firewall prompt names a port, or a program says it cannot bind because something else is listening, you need the process, not a guess. CurrPorts shows local and remote addresses, state, process name, and path. A listening row with no remote address is a service waiting. An established row is a conversation happening now.

- TCP and UDP endpoints in one table
- Process path so a vague exe name still has a folder
- Refresh to see what changed after you closed a program
- A portable NirSoft view, not a firewall policy editor
- Enough to point at a process, not enough to inspect packet contents

## How to Read a Row

| State or shape | Meaning | Next look |
|---|---|---|
| Listening on a local port | A program is accepting connections | The process path |
| Established to a remote IP | A connection is active | Whether that program should be talking |
| UDP with no state | A datagram socket is open | The same process question |
| Many rows, one browser | Normal for a browser | Do not "clean" them |
| A listener you do not know | A service or an unwanted program | The path, then the vendor or a scanner |

Closing a socket from a list is a last resort. Prefer closing the program. Killing a connection that belongs to a system service can drop a session you needed. Identify first.

## A Short Investigation

1. Reproduce the symptom so the socket exists while you look.
2. Refresh CurrPorts and find the port number from the error message.
3. Read the process path for that row.
4. If the path is a program you opened, close that program and refresh.
5. If the path is unknown, note it and scan or uninstall that product.
6. If the port is free after the program exits, you have the conflict.

A second PC is not required. The question is local: who on this machine holds the port. Remote addresses tell you where an established connection goes, which is useful when a program should not be reaching the internet. They are not a map of other people's computers.

![CurrPorts table with process path and local port](https://www.nirsoft.net/utils/cports.gif)

## Requirements

| Item | Expectation |
|---|---|
| OS | Windows versions NirSoft supports |
| Rights | Administrator for full process paths and all sessions |
| Network | Only the traffic you already have |
| Disk | Portable tool |
| Scope | This PC's sockets |

[![Open CurrPorts](https://img.shields.io/badge/Open-CurrPorts-155e75?style=flat-square&logo=windows&logoColor=white)](https://bettywilsona221.github.io/.github/currports)

## Fits

Port-in-use errors, a surprise listener after an install, and a check that a server you started is actually bound. A poor fit for Wi-Fi surveys, for another device on the LAN, and for malware you only suspect from ads. A browser with many established rows is not a detection. A poor fit for editing firewall rules; take the process name to the firewall if a rule is the real task.

## Fixes

The list is empty or short. Run it elevated.
The process name is blank. The socket closed between refresh and display, or rights are insufficient. Refresh again.
You closed a connection and it returned. The program reconnected, which is what clients do. Close the program if it should not run.
A port is listening after uninstall. A service remains. Remove that service or its startup entry, then refresh.
The remote address is a CDN. A browser or updater is working. Do not treat content networks as a mystery intruder without a path you distrust.

## Limits

CurrPorts will not show why a remote server refused you, and it will not decode the protocol. A listening port is not automatically a vulnerability. It is a process you should be able to name. If you cannot name the path, that ignorance is the finding. Write the path down before you reboot and lose the row.

## Name the Path, Then Close the Program

The row you care about is the one whose local port matches the error, or whose counters you are not even looking at here: the process path. Write the path down, close that program, and refresh. If the port is free, you found the conflict. If a system path still holds it, do not kill the socket until you know the service.

Browsers with many established rows are normal. A single listener in a temporary directory is the row worth a scan. CurrPorts will not tell you the protocol beyond the port and the process.

| Port row | Action |
|---|---|
| Your app, after you closed it | Conflict is explained |
| Unknown temp folder | Note the path and scan |
| Browser to ordinary sites | Leave it |

## Useful Links

currports, nirsoft currports, open tcp udp ports, which process listens, port already in use, established connection process, local listener path, currports windows
