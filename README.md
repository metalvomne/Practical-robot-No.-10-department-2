import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

# === 1. Зчитування даних з файлу ===
try:
    df = pd.read_csv("gdp-per-capita-growth.csv")
    print("Файл 'gdp-per-capita-growth.csv' успішно відкрито.")
except FileNotFoundError:
    print("Помилка: файл 'gdp-per-capita-growth.csv' не знайдено!")
    exit()
except Exception as e:
    print(f"Помилка при відкритті файлу: {e}")
    exit()

# === 2. Перевіримо структуру ===
# У файлі Our World in Data зазвичай є колонки: Entity, Code, Year, GDP per capita growth (annual %)
if not {"Entity", "Year", "GDP per capita growth (annual %)"} <= set(df.columns):
    print("Помилка: у файлі немає потрібних колонок!")
    exit()

# === 3. Вибір країн ===
country1 = "Ukraine"
country2 = "United States"

ukr = df[df["Entity"] == country1]
usa = df[df["Entity"] == country2]

# === 4. Фільтруємо дані за 2000–2019 роки ===
ukr = ukr[(ukr["Year"] >= 2000) & (ukr["Year"] <= 2019)]
usa = usa[(usa["Year"] >= 2000) & (usa["Year"] <= 2019)]

# === 5. Побудова лінійного графіка ===
plt.figure(figsize=(10, 6))
plt.plot(ukr["Year"], ukr["GDP per capita growth (annual %)"], marker='o', color='blue', label="Україна")
plt.plot(usa["Year"], usa["GDP per capita growth (annual %)"], marker='s', color='red', label="США")

plt.title("GDP per capita growth (annual %) — 2000–2019", fontsize=14, fontweight="bold")
plt.xlabel("Рік", fontsize=12)
plt.ylabel("Зростання ВВП на душу населення, %", fontsize=12)
plt.legend()
plt.grid(True)

# --- вісь X — цілі числа ---
plt.xticks(ticks=np.arange(2000, 2020, 1))

plt.tight_layout()
plt.show()

# === 6. Побудова стовпчастої діаграми для вибраної країни ===
country = input("Введіть назву країни (Ukraine або United States): ").strip()

if country.lower() == "ukraine":
    data_to_plot = ukr
    color = "blue"
    title = "Україна"
elif country.lower() in ["united states", "usa"]:
    data_to_plot = usa
    color = "red"
    title = "США"
else:
    print("Такої країни немає у наборі даних!")
    exit()

plt.figure(figsize=(10, 6))
plt.bar(data_to_plot["Year"], data_to_plot["GDP per capita growth (annual %)"], color=color)
plt.title(f"Динаміка зростання ВВП на душу населення — {title} (2000–2019)", fontsize=14)
plt.xlabel("Рік", fontsize=12)
plt.ylabel("Зростання ВВП на душу населення, %", fontsize=12)
plt.grid(axis='y', linestyle='--', alpha=0.7)

# --- вісь X — цілі числа ---
plt.xticks(ticks=np.arange(2000, 2020, 1))

plt.tight_layout()
plt.show()
