# staking-rewards
def staking_rewards(initial_amount, apr, days, compound=False, comp_period=365):
    """
    Рассчитывает доходность стейкинга.
    
    :param initial_amount: Начальная сумма стейкинга (в токенах)
    :param apr: Годовая процентная ставка (в %)
    :param days: Количество дней стейкинга
    :param compound: Если True, считает сложный процент (компаундинг)
    :param comp_period: Количество дней в году (по умолчанию 365)
    :return: Итоговая сумма + чистая прибыль
    """
    rate = apr / 100  # Преобразуем процент в десятичную дробь
    
    if compound:
        # Формула сложных процентов: A = P * (1 + r/n)^(nt)
        final_amount = initial_amount * (1 + rate / comp_period) ** days
    else:
        # Простые проценты: A = P + P * (r * t)
        final_amount = initial_amount + (initial_amount * rate * days / 365)
    
    profit = final_amount - initial_amount
    return final_amount, profit

# Ввод данных от пользователя
initial = float(input("Введите сумму депозита (в токенах): "))
apr = float(input("Введите годовую процентную ставку (APR) в %: "))
days = int(input("Введите количество дней стейкинга: "))
compound_choice = input("Использовать сложный процент? (y/n): ").strip().lower()

# Вычисление доходности
final_balance, profit = staking_rewards(initial, apr, days, compound=(compound_choice == 'y'))

# Вывод результатов
print(f"\n🔹 Итоговая сумма: {final_balance:.6f} токенов")
print(f"💰 Чистая прибыль: {profit:.6f} токенов")
nice
