# fuzzer
The project primarily involves fuzzing various components of OpenDaylight; the end goal being finding as many bugs or exploitable vulnerabilities as possible in the way that OpenDaylight presently implements its interfaces and protocols. 

This project uncovers high-impact, exploitable vulnerabilities in OpenDaylight components such as:
1. Memory corruption
2. Denial of service
3. Integer handling problems
4. Improper handling of exceptions
5. Privilege escalations or erroneous trust boundaries
6. Injection and Inclusion involving untrusted input text formats
7. Improper validation of inputs
8. Resource exhaustion (disk, CPU, memory)
9. Implementation logic errors depending on the protocol design of components and layers.

Consists of the following three components:

1. Generating fuzz inputs
Studying and identifying input interfaces for the OpenDaylight controller and further generating fuzz inputs. These fuzz inputs shall be generated using a number of different fuzzing strategies (discussed below in detail).
The output of this generator will be a series of test inputs that will be subsequently fed to the controller.
There are two possible interfaces to the controller:
a) Southbound interfaces and protocol plugins including openflow plugin, ovsdb plugin, other standard protocols like ONF, IETF etc and other vendor specific interfaces
b) Northbound REST APIs
Under the scope of this internship tenure, it may be necessary to identify and target a subset of these interfaces that can serve as the best fuzzing candidates.

2. Executing fuzzed inputs
Launching front-end responsible for looping over the generated fuzz inputs, each time spawning a new instance of the controller as a child process.
This main process, or the parent, shall trace the child process(OpenDaylight controller) and be able to receive all signals that are destined for the child process.
This front-end will have to be integrated to work with Mininet - the dataplane simulator and Robot Framework - the test automation framework.

3. Error monitoring and detection engine
Dynamically monitoring each instance of the controller for unhandled exceptions, crash or any other interesting signals. This component shall log all the event results (registers, memory and execution state) for later review and debugging since it’d be necessary to identify the kinds of faults, their reproducibility and how severe they are to qualify as security vulnerabilities.
