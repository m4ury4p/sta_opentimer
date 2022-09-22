# sta_opentimer:
### Using Opentimer for timing analysis:


### Technical terms:

Arrival Time: The time which signal tp <b>takes</b> to go from start point to end point is called arrival time.<br>
Require time: The <b>expected time</b> for signal to arrive at end point. is called require time.<br>

## Slack:

The difference between arrival time and require time is called slack.<br>
Slack = RAT - AAT<br>
When we use maximum require time, the slack is called maximum slack.<br>
When we use miniimum require time, the slack is called minimum slack.<br>



### Static timing Analysis using Opentimer:

## We will be using a tool named opentimer to analyse timing:<br>

To install this tool, write following commands in terminal:
```
$ git clone https://github.com/OpenTimer/OpenTimer.git
$ cd OpenTimer
$ mkdir build
$ cd build
$ cmake ../
$ make 
$ make test

```
If the test run is successfull, we can start the analysis.
