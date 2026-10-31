# Smart City RTOS Fault and Performance Monitoring

## 1. Project Overview
This project demonstrates a Smart City RTOS Fault and Performance Monitoring System using C programming and POSIX process management concepts.

It monitors three smart city services:
- Traffic Signal Service
- Environment Monitoring Service
- Energy Management Service

The system detects an unresponsive Energy Service, terminates the faulty process, and automatically restarts it.

## 2. Technologies Used
- Programming Language: C
- Operating System Concept: QNX RTOS
- Process Management: POSIX
- Functions: `fork()`, `kill()`, `waitpid()`, `sleep()`

## 3. System Specifications
- Monitors Traffic, Environment and Energy services.
- Displays CPU usage and IPC delay.
- Checks CPU and IPC threshold limits.
- Detects Energy Service failure.
- Terminates the unresponsive process using `SIGKILL`.
- Restarts the failed service automatically.
- Displays the recovery status.

## 4. Performance Parameters
| Parameter | Value |
|---|---:|
| CPU Limit | 80% |
| IPC Delay Limit | 100 ms |
| Traffic CPU Usage | 45% |
| Environment CPU Usage | 35% |
| Energy CPU Usage | 60% |
| Normal IPC Delay | 10–20 ms |
| Fault IPC Delay | 150 ms |

*Note: CPU usage and IPC delay values are simulated for demonstration.*

## 5. Working Principle
1. The system starts the Traffic, Environment and Energy services.
2. The monitoring process continuously checks the service status.
3. The Energy Service is intentionally made unresponsive to simulate a fault.
4. The monitor detects the failure and generates an alert.
5. The faulty Energy process is terminated using `SIGKILL`.
6. The `waitpid()` function collects the terminated process status.
7. A new Energy process is created using `fork()`.
8. The system displays the successful recovery status.

## 6. Fault Detection and Recovery
- **Fault:** Energy Service becomes unresponsive.
- **Detection:** Monitor identifies the service failure.
- **Termination:** `SIGKILL` terminates the faulty process.
- **Recovery:** A new Energy process is created.
- **Result:** Energy Service becomes active again.

## 7. How to Compile and Run

Using QNX Neutrino:
```bash
qcc smart_city.c -o smart_city
./smart_city
```

Using GCC on Linux:
```bash
gcc smart_city.c -o smart_city
./smart_city
```

## 8. Expected Output
- Traffic Signal: ACTIVE
- Environment: ACTIVE
- Energy: HANG
- Fault Detected
- Energy: KILLED
- Energy: RESTARTING
- Energy: ACTIVE
- Auto Recovery Successful

## 9. Conclusion
This project demonstrates how process monitoring, fault detection and automatic recovery can improve the reliability of Smart City services using RTOS concepts.
