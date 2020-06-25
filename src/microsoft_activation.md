# The Proper Way to Activate Microsoft Products

Recently I had to install Microsoft Office on my mother's laptop.
While doing some research, I found that a lot of people relied on proprietary services like `KMSPico`, `AutoKMS` and `MSToolkit` for activating Windows or Office.

Not only we don't know what these applications are doing, these applications don't have an official website of sorts. So you don't know what you are downloading.
To make matters worse, these applications just don't work if the Antivirus is enabled.
Even on places like *r/piracy* I found threads where people stood by these applications.

So I thought I'd make a post describing the objectively better approach to activate Microsoft Products.

```
DISCLAMER: This article is only for edutainment purposes. I don't encourage using this information for malicious intent
```

## Requirements

- A Server (or another computer on the same network) running Linux

Yeah, that's pretty much it.

## Setting up the KMS Server

If you haven't guessed already, we are going to set up our own KMS Server and validate the License Keys against it.
In my case, I am using a *Raspberry Pi Zero W* for the KMS Server.

So firstly, we need to download `vlmcsd` which is a FOSS Microsoft Compatible KMS Server
```
git clone https://github.com/kkkgo/vlmcsd
```

Now, we are going to compile it
```
cd vlmcsd
make
```

Once the compilation finishes, the binaries will get stored in the `bin/` directory. We need to copy those to our `$PATH`
```
cp bin/vlmcs* /usr/local/sbin/
```

Now that the server has been installed, lets make an init script for it. Create a file `/etc/init.d/vlmcsd` with the following contents
```
#!/bin/sh

### BEGIN INIT INFO
# Provides:          vlmcsd
# Required-Start:    $remote_fs $syslog
# Required-Stop:     $remote_fs $syslog
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: KMS server
### END INIT INFO

# Do NOT "set -e"

if [ `id -u` != 0 ]; then
   echo "Must be root to run this"
   exit 1
fi

PATH=/usr/local/sbin:/sbin:/usr/sbin:/usr/local/bin:/bin:/usr/bin
DESC="Microsoft KMS daemon"

NAME=vlmcsd
DAEMON=/usr/local/sbin/$NAME
PIDFILE=/var/run/$NAME.pid
SCRIPTNAME=/etc/init.d/$NAME
LOGFILE=syslog
PORT=1688

# Read configuration variable file if it is present
[ -r /etc/default/$NAME ] && . /etc/default/$NAME

# Exit if the package is not installed
[ -x "$DAEMON" ] || exit 0

DAEMON_ARGS="-l $LOGFILE -p $PIDFILE -P $PORT"

# Load the VERBOSE setting and other rcS variables
. /lib/init/vars.sh

# Define LSB log_* functions.
# Depend on lsb-base (>= 3.2-14) to ensure that this file is present
# and status_of_proc is working.
. /lib/lsb/init-functions

#
# Function that starts the daemon/service
#
do_start()
{
   status="0"
   pidofproc -p $PIDFILE $DAEMON >/dev/null || status="$?"

   if [ $status -eq 0 ]; then
      log_action_msg "already running"
      return 3
   fi

   $DAEMON $DAEMON_ARGS $EXTRA_ARGS
   return $?
}

#
# Function that stops the daemon/service
#
do_stop()
{
   if [ ! -f $PIDFILE ]; then
      log_action_msg "service not running"
      return 4
   fi

   kill `cat $PIDFILE`
   return $?
}

case "$1" in
   start)
      log_daemon_msg "Starting $DESC" "$NAME"
      do_start
      case "$?" in
         0) log_end_msg 0 ;;
         *) log_end_msg 1 ;;
      esac
      ;;
   stop)
      log_daemon_msg "Stopping $DESC" "$NAME"
      do_stop
      case "$?" in
         0) log_end_msg 0 ;;
         *) log_end_msg 1 ;;
       esac
       ;;
   restart|force-reload|reload)
      log_daemon_msg "Restarting $DESC" "$NAME"
      do_stop
      sleep 1
      do_start
      case "$?" in
         0) log_end_msg 0 ;;
         *) log_end_msg 1 ;; # Failed to start
      esac
      ;;
   status)
      status_of_proc -p $PIDFILE $DAEMON $NAME && exit 0 || exit $?
      ;;
   *)
      echo "Usage: $SCRIPTNAME {start|stop|status|reload|restart|force-reload}" >&2
      exit 3
      ;;
esac
```

and make it executable
```
chmod +x /etc/init.d/vlmcsd
```

Now we need to start and enable the daemon
```
systemctl enable vlmcsd
systemctl start vlmcsd
```

and we are done!

## Activating MS Office

You need to have Command Prompt with Admin Privileges to proceed further.
Once you have that, we need to use the `ospp.vbs` script that is present in the root folder of the MS Office Installation.
```
cd C:\Program Files\Microsoft Office\Office15
cscript ospp.vbs /inpkey:<LICENSE-KEY>
cscript ospp.vbs /sethst:<SERVER-IP>
cscript ospp.vbs /act
```

Replace `<LICENSE-KEY>` with any valid product key of your version of MS Office and `<SERVER-IP>` with the IP Address or Hostname of your server.

You can find lots license keys online by just doing a simple search.

## Activating Windows

Although I haven't tried this, the following commands should work without any issues
```
slmgr.vbs -ipk <LICENSE-KEY>
slmgr.vbs -skms <SERVER-IP>
slmgr.vbs -ato
```

---

Sources:

- `vlmcsd`: <https://github.com/kkkgo/vlmcsd>
