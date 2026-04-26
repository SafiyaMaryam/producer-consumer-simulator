# 🔄 Producer-Consumer Problem Simulator

A fully interactive, browser-based visualization of the classic **Producer-Consumer synchronization problem** in Operating Systems, demonstrating the use of **semaphores** and **mutex locks** to safely manage a shared bounded buffer.

> 🎓 Mini Project — Operating Systems | Anna University

---

## 🌐 Live Demo

**[🚀 View Live Simulation](https://YOUR-USERNAME.github.io/producer-consumer-simulator/)**

> Replace `YOUR-USERNAME` with your GitHub username after hosting

---

## 📌 Problem Statement

The Producer-Consumer problem is a classic **inter-process synchronization** problem where:
- **Producers** generate data and place it into a shared bounded buffer
- **Consumers** remove data from the buffer and process it
- Both must operate **concurrently** without causing race conditions, buffer overflow, or buffer underflow

### The Challenge
| Problem | Cause | Solution |
|---|---|---|
| Buffer Overflow | Producer writes when buffer is full | `sem_empty` semaphore |
| Buffer Underflow | Consumer reads when buffer is empty | `sem_full` semaphore |
| Race Condition | Two threads access buffer simultaneously | `mutex` lock |

---

## ✨ Features

- 🟢 **Live Buffer Visualization** — animated slot-by-slot fill and empty
- 📊 **Real-time Semaphore Display** — `sem_empty` and `sem_full` with value bars
- 🔒 **Mutex Lock Animation** — shows which thread holds the lock
- 🧵 **Thread State Cards** — each thread shows: `IDLE → WAIT → CRITICAL → SIGNAL → DONE`
- 💡 **Algorithm Highlighting** — pseudocode line lights up as each step runs
- 📋 **Event Log** — timestamped log of every wait/signal/read/write operation
- 📈 **Live Statistics** — produced count, consumed count, occupancy %, wait events
- ⚠️ **Deadlock Detection** — alerts when all threads are blocked
- 🌙 **Dark / Light Mode** — toggle in the header
- ⚙️ **Configurable** — set number of producers, consumers, buffer size, and speed

---

## 🖼️ Screenshots

> *(Add your screenshots here after running the simulation)*

| State | Description |
|---|---|
| Normal Run | Producers and consumers operating concurrently |
| Buffer Full | `sem_empty = 0`, producers blocked |
| Buffer Empty | `sem_full = 0`, consumers blocked |
| Mutex Locked 🔒 | One thread in critical section |

---

## 🧠 Algorithm Used

### Producer Thread
```c
while(true) {
    produce_item();
    wait(sem_empty);    // wait if no empty slot
    wait(mutex);        // acquire mutual exclusion
    buffer[in] = item;  // write to buffer (critical section)
    in = (in + 1) % N;
    signal(mutex);      // release mutual exclusion
    signal(sem_full);   // signal item is available
}
```

### Consumer Thread
```c
while(true) {
    wait(sem_full);      // wait if no item available
    wait(mutex);         // acquire mutual exclusion
    item = buffer[out];  // read from buffer (critical section)
    out = (out + 1) % N;
    signal(mutex);       // release mutual exclusion
    signal(sem_empty);   // signal slot is free
    consume_item();
}
```

---

## 🚀 How to Run

### Option 1 — Direct Browser (No Setup)
```text
1. Download index.html
2. Double-click to open in any browser
3. Press Start
```

### Option 2 — Clone & Open
```bash
git clone https://github.com/YOUR-USERNAME/producer-consumer-simulator.git
cd producer-consumer-simulator
# Open index.html in your browser
```

> ✅ No installation required. No Node.js. No dependencies. Pure HTML + CSS + JS.

---

## 🎮 Usage Guide

| Control | Description |
|---|---|
| **Producers** slider | Set 1–4 producer threads |
| **Consumers** slider | Set 1–4 consumer threads |
| **Buffer Size** slider | Set buffer capacity (2–8 slots) |
| **Speed** slider | Control simulation speed (1× to 5×) |
| **Start** | Begin simulation |
| **Pause / Resume** | Pause or continue |
| **Reset** | Stop and reset everything |

### Try These Scenarios
- `4 Producers, 1 Consumer` → Buffer fills fast, producers block on `sem_empty`
- `1 Producer, 4 Consumers` → Buffer drains fast, consumers block on `sem_full`
- `2 Producers, 2 Consumers, Buffer=2` → Frequent mutex contention visible

---

## 🛠️ Tech Stack

| Technology | Usage |
|---|---|
| HTML5 | Structure and layout |
| CSS3 | Animations, theming, responsive design |
| Vanilla JavaScript | Simulation logic and state machine |
| Google Fonts | Inter + JetBrains Mono |

> No frameworks. No libraries. Single self-contained file (~40 KB).

---

## 📂 Project Structure

```text
producer-consumer-simulator/
│
└── index.html        # Complete project (HTML + CSS + JS in one file)
└── README.md         # Project documentation
```

---

## 📚 Concepts Demonstrated

- **Semaphores** — counting semaphores for buffer coordination
- **Mutex Locks** — binary semaphore for mutual exclusion
- **Critical Section** — protected buffer read/write zone
- **Bounded Buffer** — fixed-size circular shared memory
- **Thread Synchronization** — coordinating concurrent processes
- **Deadlock Detection** — identifying when all threads are blocked
- **Race Condition Prevention** — safe shared resource access

---
