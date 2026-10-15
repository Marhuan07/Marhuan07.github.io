# Marhuan07.github.io
import matplotlib.pyplot as plt
import statistics

# BATTERY DATA
#this below is a dictionary containing battery data, like voltage, time(minutes), and capacity
batteries = {
    "Duracell": {
        "type": "Alkaline",
        "voltage": [1.69, ],
        "time": [0, 20, 40, 60, 80],
        "capacity": "2700 mAh"
    },
    "Energizer": {
        "type": "Alkaline",
        "voltage": [1.28, ],
        "time": [0, 20, 40, 60, 80],
        "capacity": "2700 mAh"
    },
    "Rayovac": {
        "type": "Alkaline",
        "voltage": [1.59, ],
        "time": [0, 20, 40, 60, 80],
        "capacity": "2700 mAh"
    },
    "Up&Up": {
        "type": "Alkaline",
        "voltage": [1.63, ],
        "time": [0, 20, 40, 60, 80],
        "capacity": "2500 mAh"
    }
}

# CALCULATE BATTERY STATISTICS
#
def analyze_battery(name):
    battery = batteries[name]
    voltage = battery["voltage"]
    time = battery["time"]
    initial_voltage = voltage[0]
    final_voltage = voltage[-1]
    highest_voltage = max(voltage)
    lowest_voltage = min(voltage)
    average_voltage = statistics.mean(voltage)
    voltage_drop = initial_voltage - final_voltage
    percent_drop = (voltage_drop / initial_voltage) * 100
    lowest_index = voltage.index(lowest_voltage)
    lowest_time = time[lowest_index]
    print("\n--------------------------------")
    print(name, "Battery Analysis")
    print("--------------------------------")
    print("Battery type:", battery["type"])
    print("Battery capacity:", battery["capacity"])
    print("Initial voltage:", round(initial_voltage, 3), "V")
    print("Final voltage:", round(final_voltage, 3), "V")
    print("Highest voltage:", round(highest_voltage, 3), "V")
    print("Lowest voltage:", round(lowest_voltage, 3), "V")
    print("Average voltage:", round(average_voltage, 3), "V")
    print("Voltage drop:", round(voltage_drop, 3), "V")
    print("Percent voltage drop:", round(percent_drop, 2), "%")
    print("Lowest voltage occurred at:", lowest_time, "minutes")

# PLOT ONE BATTERY

def plot_battery(name):
    battery = batteries[name]
    time = battery["time"]
    voltage = battery["voltage"]
    initial_voltage = voltage[0]
    final_voltage = voltage[-1]
    plt.figure()
    plt.plot(time, voltage, marker="o")

    # Important markers

    plt.scatter(time[0], initial_voltage, label="Initial Voltage")
    plt.scatter(time[-1], final_voltage, label="Final Voltage")
    plt.xlabel("Time (minutes)")
    plt.ylabel("Voltage (V)")
    plt.title(name + " Battery Voltage Over Time")
    plt.legend()
    plt.grid()
    plt.show()

# COMPARE ALL BATTERIES

def compare_batteries():
    plt.figure()
    for name in batteries:
        time = batteries[name]["time"]
        voltage = batteries[name]["voltage"]
        plt.plot(time, voltage, marker="o", label=name)
    plt.xlabel("Time (minutes)")
    plt.ylabel("Voltage (V)")
    plt.title("Battery Voltage Comparison")
    plt.legend()
    plt.grid()
    plt.show()

# FIND THE BEST BATTERY

def find_best_battery():
    best_battery = None
    smallest_drop = None
    for name in batteries:
        voltage = batteries[name]["voltage"]
        voltage_drop = voltage[0] - voltage[-1]
        if smallest_drop is None or voltage_drop < smallest_drop:
            smallest_drop = voltage_drop
            best_battery = name
    print("\n================================")
    print("BEST BATTERY")
    print("================================")
    print("The battery with the smallest voltage drop is:",
          best_battery)
    print("Voltage drop:",
          round(smallest_drop, 3), "V")

# MAIN PROGRAM

while True:
    print("\n================================")
    print("BATTERY ANALYSIS PROGRAM")
    print("================================")
    print("1. Analyze a battery")
    print("2. Plot a battery")
    print("3. Compare all batteries")
    print("4. Find the best battery")
    print("5. Exit")
    choice = input("Enter your choice: ")
    if choice == "1":
        print("\nAvailable batteries:")
        for name in batteries:
            print("-", name)
        battery_choice = input("Enter battery name: ")
        if battery_choice in batteries:
            analyze_battery(battery_choice)
        else:
            print("Invalid battery.")
    elif choice == "2":
        print("\nAvailable batteries:")
        for name in batteries:
            print("-", name)
        battery_choice = input("Enter battery name: ")
        if battery_choice in batteries:
            plot_battery(battery_choice)
        else:
            print("Invalid battery.")
    elif choice == "3":
        compare_batteries()
    elif choice == "4":
        find_best_battery()
    elif choice == "5":
        print("Goodbye!")
        break
    else:
        print("Invalid choice.")
