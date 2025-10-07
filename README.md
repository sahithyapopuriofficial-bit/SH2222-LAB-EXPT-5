# Experiment 5: Simulation of Single Server Queue (M/M/1 Model) 

**Question:**

Write a Python program to simulate a single server queueing system (M/M/1) 
with infinite capacity, where customers arrive randomly at a service counter (e.g., a bank or 
ticket counter). 

**AIM:**

To implement and simulate a single server infinite capacity queue (M/M/1) using Python 
and study customer waiting time, service time, and system utilization.  

**SOFTWARE REQUIRED:** Python and numpy library  

**Algorithm:**

<img width="695" height="253" alt="{56559156-AA7F-4644-BEAE-8EAC9527E21F}" src="https://github.com/user-attachments/assets/45d861d6-5db0-4a10-9118-6c780726a19d" />

**Mathematical Expression:**

<img width="767" height="383" alt="image" src="https://github.com/user-attachments/assets/1eb4d6ce-7159-412c-ba80-181927be6f63" />

**PROGRAM:**
```
import numpy as np 
# Inputs 
lam = float(input("Enter arrival rate (λ): ")) 
mu = float(input("Enter service rate (μ): ")) 
n = int(input("Enter number of customers: ")) 
# Generate inter-arrival and service times 
inter_arrival_times = np.random.exponential(1/lam, n) 
service_times = np.random.exponential(1/mu, n) 
# Initialize arrays 
arrival_times = np.cumsum(inter_arrival_times) 
service_start_times = np.zeros(n) 
departure_times = np.zeros(n) 
waiting_times = np.zeros(n) 
# First customer 
service_start_times[0] = arrival_times[0] 
departure_times[0] = service_start_times[0] + service_times[0] 
waiting_times[0] = service_start_times[0] - arrival_times[0] 
# Next customers 
for i in range(1, n): 
    service_start_times[i] = max(arrival_times[i], departure_times[i-1]) 
    departure_times[i] = service_start_times[i] + service_times[i] 
    waiting_times[i] = service_start_times[i] - arrival_times[i] 
# Display results 
print("\n--- Single Server Queue Simulation ---") 
print("Cust\tArrive\tService\tStart\tDepart\tWaiting") 
for i in range(n): 
    print(f"{i+1}\t{arrival_times[i]:.2f}\t{service_times[i]:.2f}\t" 
          f"{service_start_times[i]:.2f}\t{departure_times[i]:.2f}\t{waiting_times[i]:.2f}") 
print("\nAverage waiting time in queue: ", round(np.mean(waiting_times), 2))
```
**OUTPUT:**

<img width="476" height="327" alt="image" src="https://github.com/user-attachments/assets/de89230b-1149-4ccf-b16d-f743f4ee993a" />

**RESULT:**

The program successfully simulates a single server infinite capacity queueing model 
(M/M/1). 
