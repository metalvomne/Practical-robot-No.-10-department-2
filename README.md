import matplotlib.pyplot as plt
import numpy as np

# === 1. Масиви даних (Children out of school, primary) ===
years = np.arange(2004, 2024)  # останні 20 років

# Дані взяті умовно (можна замінити реальними з World Bank)
ukraine = [45, 42, 40, 38, 35, 32, 29, 25, 22, 20, 18, 17, 16, 15, 14, 14, 13, 12, 12, 11]
usa = [300, 295, 290, 280, 270, 260, 250, 240, 235, 230, 225, 220, 215, 210, 205, 200, 195, 190, 185, 180]

# === 2. Побудова графіків двох країн ===
plt.figure(figsize=(10, 6))
plt.plot(years, ukraine, color='blue', marker='o', label='Україна')
plt.plot(years, usa, color='red', marker='s', label='США')

plt.title("Динаміка показника 'Children out of school, primary' (2004–2023)", fontsize=14, fontweight='bold')
plt.xlabel("Рік", fontsize=12)
plt.ylabel("Кількість дітей (тис.)", fontsize=12)
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()

# === 3. Побудова стовпчастих діаграм ===

# Вибір країни користувачем
country = input("Введіть назву країни (Україна або США): ").strip().lower()

if country == "україна":
    data = ukraine
    color = 'blue'
    title = "Україна"
elif country == "сша":
    data = usa
    color = 'red'
    title = "США"
else:
    print("Невірна назва країни!")
    exit()

plt.figure(figsize=(10, 6))
plt.bar(years, data, color=color, alpha=0.8)
plt.title(f"Стовпчаста діаграма показника 'Children out of school, primary' ({title})", fontsize=14, fontweight='bold')
plt.xlabel("Рік", fontsize=12)
plt.ylabel("Кількість дітей (тис.)", fontsize=12)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.tight_layout()
plt.show()
