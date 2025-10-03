# exp 1
# GENERATION OF  NETWORK WITHOUT TRAFFIC 
## Objective: Same network, but generate traffic using TCP and FTP. 
## Code: 
```
set ns [new Simulator] 

set tracefile [open out.tr w] 
set namfile [open out.nam w] 
$ns trace-all $tracefile 
$ns namtrace-all $namfile 

set n0 [$ns node] 
set n1 [$ns node] 
set n2 [$ns node] 
set n3 [$ns node] 
set n4 [$ns node] 

$ns duplex-link $n0 $n1 1Mb 10ms DropTail 
$ns duplex-link $n1 $n2 1Mb 10ms DropTail 
$ns duplex-link $n2 $n3 1Mb 10ms DropTail 
$ns duplex-link $n3 $n4 1Mb 10ms DropTail 
$ns duplex-link $n4 $n0 1Mb 10ms DropTail 

set tcp0 [new Agent/TCP] 
$ns attach-agent $n0 $tcp0 
 
set sink0 [new Agent/TCPSink] 
$ns attach-agent $n3 $sink0 

$ns connect $tcp0 $sink0 

set ftp0 [new Application/FTP] 
$ftp0 attach-agent $tcp0 

$ns at 1.0 "$ftp0 start" 
$ns at 4.5 "$ftp0 stop" 
 
proc finish {} { 
global ns tracefile namfile 
$ns flush-trace 
close $tracefile 
24 
close $namfile 
exec nam out.nam & 
exit 0 
} 
$ns at 5.0 "finish" 
$ns run
```
## output:
![WhatsApp Image 2025-10-03 at 09 35 49_d26eba08](https://github.com/user-attachments/assets/39f16479-959e-46a8-86d1-4206cd32060a)

## RESULT:
Thus, the GENERATION OF  NETWORK WITHOUT TRAFFIC  is performed using NS2.



