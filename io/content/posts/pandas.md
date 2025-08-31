---
date: '2025-08-31T17:34:00+08:00'
title: 'Pandas'

---

Example

```python
import pandas as pd
import matplotlib.pyplot as plt

# Load the data from the CSV file
df = pd.read_csv('charge_log.csv')

# Inspect the data
print(df.head())
print(df.info())

# Convert 'time' column from HH:MM:SS format to seconds
def time_to_seconds(time_str):
    h, m, s = map(int, time_str.split(':'))
    return h * 3600 + m * 60 + s

df['time_in_seconds'] = df['time'].apply(time_to_seconds)

# Create the plot
plt.figure(figsize=(12, 8))

# Get unique current types
cur_types = df['cur_type'].unique()

# Plot a line for each current type
for cur_type in cur_types:
    df_cur_type = df[df['cur_type'] == cur_type]
    plt.plot(df_cur_type['time_in_seconds'], df_cur_type['current'], label=cur_type)

# Set labels and title
plt.xlabel('时间 (s)')
plt.ylabel('电流')
plt.title('充电参数表')
plt.legend(title='电流类型')
plt.grid(True)
plt.tight_layout()

# Save the plot
plt.savefig('charge_log_plot.png')

print("Plot saved as charge_log_plot.png")
```

