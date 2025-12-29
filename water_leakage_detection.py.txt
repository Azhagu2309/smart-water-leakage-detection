import pandas as pd
import matplotlib.pyplot as plt

data = {
    "time": [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    "water_usage_liters": [120, 125, 130, 128, 132, 300, 310, 305, 135, 140]
}

df = pd.DataFrame(data)

LEAKAGE_THRESHOLD = 200

df["Leakage"] = df["water_usage_liters"] > LEAKAGE_THRESHOLD

print("\nSMART WATER LEAKAGE DETECTION REPORT\n")

leak_found = False
for index, row in df.iterrows():
    if row["Leakage"]:
        leak_found = True
        print(f"Leakage Detected at Time {row['time']} Usage {row['water_usage_liters']} Liters")

if not leak_found:
    print("No leakage detected Water usage is normal")

plt.figure()
plt.plot(df["time"], df["water_usage_liters"], marker='o')
plt.axhline(y=LEAKAGE_THRESHOLD)
plt.xlabel("Time")
plt.ylabel("Water Usage Liters")
plt.title("Smart Water Leakage Detection")
plt.grid(True)
plt.show()
