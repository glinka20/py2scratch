from collections import Counter
import itertools

def count_pairs(text, mode='all'):
    """
    Подсчет пар в строке с разными режимами.
    
    Параметры:
        text (str): исходная строка
        mode (str): режим подсчета
            - 'all': все возможные упорядоченные пары
            - 'adjacent': только соседние пары
            - 'unique': пары из уникальных символов
            - 'unordered': неупорядоченные пары
    """
    if mode == 'all':
        # Все возможные упорядоченные пары
        n = len(text)
        return n * (n - 1)
    
    elif mode == 'adjacent':
        # Только соседние пары
        if len(text) < 2:
            return 0
        pairs = [text[i:i+2] for i in range(len(text)-1)]
        return len(pairs)
    
    elif mode == 'unique':
        # Пары из уникальных символов (без порядка)
        unique_chars = set(text)
        n = len(unique_chars)
        return n * (n - 1) // 2
    
    elif mode == 'unordered':
        # Все возможные неупорядоченные пары
        n = len(text)
        return n * (n - 1) // 2
    
    else:
        raise ValueError("Неизвестный режим. Используйте: 'all', 'adjacent', 'unique', 'unordered'")

# Основная программа
def main():
    print("ПОДСЧЕТ ПАР В СТРОКЕ")
    print("-" * 30)
    
    # Ввод данных
    text = input("Введите строку: ").strip()
    
    if not text:
        print("Строка пустая!")
        return
    
    print(f"\nИсходная строка: '{text}'")
    print(f"Длина строки: {len(text)}")
    
    # Разные варианты подсчета
    print("\nРезультаты подсчета:")
    print(f"1. Все возможные упорядоченные пары: {count_pairs(text, 'all')}")
    print(f"2. Соседние пары в строке: {count_pairs(text, 'adjacent')}")
    print(f"3. Пары из уникальных символов: {count_pairs(text, 'unique')}")
    print(f"4. Все возможные неупорядоченные пары: {count_pairs(text, 'unordered')}")
    
    # Детализация соседних пар
    if len(text) >= 2:
        print("\nДетализация соседних пар:")
        pairs = [text[i:i+2] for i in range(len(text)-1)]
        pair_counter = Counter(pairs)
        for pair, count in sorted(pair_counter.items()):
            print(f"  '{pair}': {count} раз(а)")

if __name__ == "__main__":
    main()
