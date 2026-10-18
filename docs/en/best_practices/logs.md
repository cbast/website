# Syslog

Syslog is a standard Linux interface for applications to send log messages to a system logging service.

## Example

Write a log message using the C syslog API:

```c
#include <syslog.h>

int main(void) {
	openlog("learn-app", LOG_PID, LOG_USER);
	syslog(LOG_INFO, "Application started");
	closelog();
	return 0;
}
```

Read the messages from the systemd journal with Bash:

```bash
#!/usr/bin/env bash
# Display this application's messages from today.
journalctl -t learn-app --since today
# Follow new messages as they arrive.
journalctl -t learn-app -f
```

## Reference

- [GNU C Library Manual: Overview of Syslog](https://www.gnu.org/software/libc/manual/html_node/Overview-of-Syslog.html)
- [systemd `journalctl` manual](https://www.freedesktop.org/software/systemd/man/latest/journalctl.html)
