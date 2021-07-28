
# system resources

key info in /proc/

cpuinfo..

meminfo..
free -h (human readable) for more memory info

//disk space
df -ht ext4   /// - view state of storage devices mounted to system


iftop is good network tool (top for networking)

ip addr // to get network interfaces, eg eth0. pass this to iftop
sudo iftop -i eth0




# system processes

ps - with no arguments will list processes running in the current shell


ps aux - will give all processes across the entire system


dmesg - managing messages coming from the kernel ring buffer



## unwanted processes

kill <pid>

killall <name> - will kill all instances(procs) of that 

sudo systemctl status <thing> - see current state of a process

## process priorities

if you look at the output of top there is a NI colum header
that represents the nice value..

    nice is a program found on Unix and Unix-like operating systems such as Linux. It directly maps to a kernel call of the same name. nice is used to invoke a utility or shell script with a particular CPU priority, thus giving the process more or less CPU time than other processes. A niceness of -20 is the highest priority and 19 is the lowest priority. The default niceness for processes is inherited from its parent process and is usually 0.