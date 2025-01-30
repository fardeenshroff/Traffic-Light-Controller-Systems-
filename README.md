# 🚦 Traffic Light Controller Systems 

## 📌 Project Overview  

The **Traffic Light Controller** is a **hardware-based system** designed using **Hardware Description Languages (HDL)** to manage traffic flow efficiently. This project ensures **optimized vehicle movement, pedestrian safety, and minimal congestion** by implementing a **finite state machine (FSM)**.  

The system is implemented using **Verilog/VHDL** and tested using simulation tools such as **ModelSim/Xilinx ISim**.  

---

## 📋 Table of Contents  

- [Project Overview](#-project-overview)  
- [Features](#-features)  
- [System Design](#-system-design)  
- [Implementation](#-implementation)  
- [Testing](#-testing)  
- [Results](#-results)  
- [Analysis](#-analysis)  
- [Future Enhancements](#-future-enhancements)  
- [License](#-license)  
- [Contribution](#-contribution)  
- [Contact](#-contact)  

---

## 🛠️ Features  

✔ **Time-based signal transitions** for optimized traffic flow.  
✔ **FSM-based design** for better state management.  
✔ **Clock divider** for timing regulation.  
✔ **Synchronized pedestrian crossing signals**.  
✔ **Simulation-based testing** to verify system accuracy.  
✔ **Scalable architecture** for multiple intersections.  

---

## 🏗️ System Design  

### **1️⃣ State Diagram**  

The traffic light follows a **finite state machine (FSM)** approach:  

- **State 0:** 🚦 **Main Road: Red | Side Road: Green**  
- **State 1:** 🚦 **Main Road: Green | Side Road: Red**  
- **State 2:** 🚦 **Both Roads: Yellow (Transition)**  

Each state has a **fixed duration**, managed by a **clock divider**.  

---

### **2️⃣ Hardware Implementation**  

The design consists of the following **HDL modules**:  

- **Clock Divider:** Generates a slower clock signal for timing control.  
- **State Machine:** Controls the transitions between **RED, GREEN, and YELLOW** states.  
- **Output Logic:** Activates the appropriate **LED signals** based on the FSM state.  

---

## 📝 Implementation  

### **1️⃣ Project Structure**

📂 Traffic_Light_Controller │── 📜 README.md                # Project documentation │── 📂 src                      # Source files │   ├── traffic_light.v         # Main HDL module │   ├── state_machine.v         # FSM implementation │   ├── clock_divider.v         # Clock divider for signal timing │── 📂 testbench                # Testbench files │   ├── traffic_light_tb.v      # Testbench for verification │── 📂 results                   # Simulation results │   ├── waveform.png            # Output waveforms │── 📜 LICENSE                   # License file (optional) │── 📜 report.pdf                # Project report (optional)

---

### **2️⃣ HDL Code - Traffic Light Controller (Verilog)**  

```verilog
module traffic_light(
    input clk, rst,
    output reg [2:0] main_signal,  // {Red, Yellow, Green}
    output reg [2:0] sec_signal    // {Red, Yellow, Green}
);
    reg [1:0] state; // 0: Red, 1: Green, 2: Yellow

    always @(posedge clk or posedge rst) begin
        if (rst) 
            state <= 0;
        else 
            case (state)
                0: state <= 1; // Red → Green
                1: state <= 2; // Green → Yellow
                2: state <= 0; // Yellow → Red
            endcase
    end

    always @(*) begin
        case (state)
            0: begin main_signal = 3'b100; sec_signal = 3'b001; end  // Main Red, Sec Green
            1: begin main_signal = 3'b001; sec_signal = 3'b100; end  // Main Green, Sec Red
            2: begin main_signal = 3'b010; sec_signal = 3'b010; end  // Both Yellow
        endcase
    end
endmodule


---

✅ Testing

1️⃣ Testbench Code (Verilog)

module traffic_light_tb();
    reg clk, rst;
    wire [2:0] main_signal, sec_signal;

    // Instantiate Traffic Light Controller
    traffic_light uut (.clk(clk), .rst(rst), .main_signal(main_signal), .sec_signal(sec_signal));

    initial begin
        $dumpfile("traffic_light.vcd");
        $dumpvars(0, traffic_light_tb);
        
        clk = 0;
        rst = 1; #5;
        rst = 0;
        
        #100; // Run simulation
        $finish;
    end

    always #5 clk = ~clk; // Generate clock signal
endmodule


---

📊 Results

1️⃣ Simulation Waveforms

The project was tested using ModelSim/Xilinx ISim, and the results confirm:

✅ Correct state transitions (Red → Green → Yellow → Red).
✅ Pedestrian light synchronization.
✅ Stable clock-driven changes ensuring smooth operation.

Output Screenshot:




---

🔎 Analysis

✔ Efficiency: The FSM-based approach ensures smooth and predictable traffic management.
✔ Scalability: The design can be extended for multiple intersections.
✔ Reliability: The HDL-based implementation ensures hardware-level efficiency and real-world applicability.


---

🚀 Future Enhancements

🔹 Sensor-Based Traffic Control: Real-time detection of traffic conditions using IR sensors.
🔹 Emergency Vehicle Override: Automatic priority handling for ambulances and fire trucks.
🔹 IoT Integration: Cloud-based monitoring and real-time traffic optimization.


---

📜 License

This project is released under the MIT License, allowing modifications and contributions while crediting the original work.


---

🤝 Contribution

Want to improve this project? Follow these steps:

1️⃣ Fork the repository.
2️⃣ Create a new branch (feature-xyz).
3️⃣ Commit your changes.
4️⃣ Submit a pull request (PR).


---

📧 Contact

For any queries or improvements, feel free to reach out:

📩 Email: fshroff1@hawk.iit.edu
🌍 GitHub: www.github.com/fardeenshroff

---
