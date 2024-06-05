import numpy as np
import matplotlib.pyplot as plt

# Пример данных (исторические цены акций)
historical_prices = np.array([100, 101, 102, 105, 107, 110, 115, 120])

# Параметры модели
alpha = 0.01
delta_t = 1
delta_x = 1

# Создание сетки конечных разностей
time_steps = 10
price_steps = len(historical_prices)
prices = np.zeros((time_steps, price_steps))
prices[0, :] = historical_prices

# Итерации по времени
for t in range(1, time_steps):
    for x in range(1, price_steps - 1):
        prices[t, x] = prices[t-1, x] + alpha * delta_t / (delta_x**2) * (prices[t-1, x+1] - 2 * prices[t-1, x] + prices[t-1, x-1])

# Построение графиков
plt.figure(figsize=(12, 6))
for t in range(time_steps):
    plt.plot(prices[t, :], label=f'Time {t}')
plt.xlabel('Time Steps')
plt.ylabel('Price')
plt.legend()
plt.title('Прогнозирование цены акций методом конечных разностей')
plt.show()
