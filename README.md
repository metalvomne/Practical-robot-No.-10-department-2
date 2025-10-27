import json
import matplotlib.pyplot as plt

# === 1. Зчитування даних з JSON ===
data_file = "employees.json"

with open(data_file, "r", encoding="utf-8") as f:
    employees = json.load(f)

# === 2. Підрахунок кількості працівників за посадами ===
positions_count = {}
for emp in employees:
    pos = emp["position"]
    positions_count[pos] = positions_count.get(pos, 0) + 1

# === 3. Підготовка даних для графіка ===
labels = list(positions_count.keys())
sizes = list(positions_count.values())

# === 4. Побудова кругової діаграми ===
colors = plt.cm.Set3.colors  # набір різних кольорів
plt.figure(figsize=(7, 7))
plt.pie(
    sizes,
    labels=labels,
    autopct='%1.1f%%',   # відсотки з одним десятковим знаком
    startangle=90,       # початок від вертикалі
    colors=colors[:len(labels)],  # унікальні кольори
    shadow=True
)

plt.title("Розподіл працівників за посадами", fontsize=14, fontweight="bold")
plt.tight_layout()
plt.show()
