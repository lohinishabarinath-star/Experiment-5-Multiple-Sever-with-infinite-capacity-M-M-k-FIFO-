# Experiment-5-Multiple-Sever-with-infinite-capacity-(M/M/k)-(oo/FIFO)
# Aim
 	To find 
  
a)	Average number of materials in the system 

b)	Average number of materials in the conveyor

c)	Waiting time of each material in the system 

d)	Waiting time of each material in the conveyor

If the arrival of materials follow poisson process with mean interval time 10 seconds, service time of two lather machine follow exponential distribution with mean sevice time 1 second and average service time of robot is 7 seconds.

# Software required: Visual Components and Python
# Theory: 
Queueing shows up everywhere: cafeterias, libraries, banks—anywhere arrivals need service and may face delay. Waiting can’t be removed entirely, but it can be controlled. Adding more servers reduces delays, though it may increase idle time.
In an M/M/∞ system, there are infinitely many servers, so every arrival begins service immediately and no one waits. Arrivals follow a Poisson rate λ, and each server provides exponential service with rate μ.
If there are k customers in the system, then k servers are busy. Each works independently, so the total service-completion rate is the minimum of k exponential clocks, giving an overall departure rate of kμ.
This lets us treat the M/M/∞ model as a simple Markov chain and find the distribution of the number of customers in service.
# Algorithm
<img width="806" height="297" alt="image" src="https://github.com/user-attachments/assets/e08285b0-8d2d-4b63-8e52-4bf2d065b0ff" />

# Program
Register number: 25015038
Name: LOHINI S
Slot: 3P1-1
```
import math

# Input for mean inter-arrival time
arr_time_input = ''
while not arr_time_input.strip():
    arr_time_input = input("Enter the mean inter arrival time of objects from feeder (in secs): ")
    if not arr_time_input.strip():
        print("Input cannot be empty. Please enter a value.")

arr_time = float(arr_time_input)

# Other inputs
ser_time = float(input("Enter the mean service time of lathe machine (in secs): "))
robot_time = float(input("Enter the additional time taken for the robot (in secs): "))
c = int(input("Number of service centres: "))

# Rates
lam = 1 / arr_time
mu = 1 / (ser_time + robot_time)

print("------------------------------------------------")
print("Multiple Server with Infinite Capacity Queue - (M/M/c):(∞/FIFO)")
print("------------------------------------------------")

print(f"The mean arrival rate per second: {lam:.2f}")
print(f"The mean service rate per second: {mu:.2f}")

rho = lam / (c * mu)

# Calculating P0
summation = 0
for i in range(c):
    summation += (lam / mu) ** i / math.factorial(i)

summation += ((lam / mu) ** c / math.factorial(c)) * (1 / (1 - rho))
P0 = 1 / summation

# If rho < 1 → stable system
if rho < 1:
    Lq = (P0 * (lam / mu) ** c * rho) / (math.factorial(c) * (1 - rho) ** 2)
    Ls = Lq + lam / mu
    Ws = Ls / lam
    Wq = Lq / lam

    print(f"Average number of objects in the system (Ls): {Ls:.2f}")
    print(f"Average number of objects in the queue (Lq): {Lq:.2f}")
    print(f"Average waiting time in the system (Ws): {Ws:.2f} secs")
    print(f"Average waiting time in the queue (Wq): {Wq:.2f} secs")
    print(f"Probability that the system is busy (ρ): {rho:.2f}")
    print(f"Probability that the system is empty (P0): {P0:.2f}")

else:
    print("Warning! Objects overflow will happen in the conveyor")

print("------------------------------------------------")
```

# Output
```
Enter the mean inter arrival time of objects from feeder (in secs): 10
Enter the mean service time of lathe machine (in secs): 12
Enter the additional time taken for the robot (in secs): 3
Number of service centres: 2
------------------------------------------------
Multiple Server with Infinite Capacity Queue - (M/M/c):(∞/FIFO)
------------------------------------------------
The mean arrival rate per second: 0.10
The mean service rate per second: 0.07
Average number of objects in the system (Ls): 3.43
Average number of objects in the queue (Lq): 1.93
Average waiting time in the system (Ws): 34.29 secs
Average waiting time in the queue (Wq): 19.29 secs
Probability that the system is busy (ρ): 0.75
Probability that the system is empty (P0): 0.14
------------------------------------------------
```

# Result
       The average number of material in the system and in the conveyor and waiting are  successfully found.

