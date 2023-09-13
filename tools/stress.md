### How to do stress test?
First install `stress`:
```
apt install stress
```
This command for cpu: (4 is the number of cores)
```
stress --cpu 4
```
```
stress-ng --vm 1 --vm-bytes 90% -t 1h
```
