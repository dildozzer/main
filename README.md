def get_coords(name):
    while True:
        try:
            x, y = map(int, input(f"Введите координаты для {name} (x y): ").split())
            if 0 <= x < 3 and 0 <= y < 3:
                return x, y
            else:
                print("Координаты должны быть в диапазоне 0–2.")
        except ValueError:
            print("Нужно ввести два целых числа через пробел.")

def print_field(field):
    for row in field:
        print(" ".join(cell if cell else "." for cell in row))
    print()

def check_win(field, sym):
    for r in range(3):
        if all(field[r][c] == sym for c in range(3)):
            return True
    for c in range(3):
        if all(field[r][c] == sym for r in range(3)):
            return True
    if all(field[i][i] == sym for i in range(3)):
        return True
    if all(field[i][2 - i] == sym for i in range(3)):
        return True
    return False

field = [["" for _ in range(3)] for _ in range(3)]
turns_made = 0
x_turn = True

while True:
    print_field(field)

    if x_turn:
        name = "крестиков"
        sym = "X"
    else:
        name = "ноликов"
        sym = "0"

    while True:
        x, y = get_coords(name)
        if field[x][y] == "":
            break
        print(f"Ошибка — клетка занята: {field[x][y]}")

    field[x][y] = sym
    turns_made += 1

    if check_win(field, sym):
        print_field(field)
        print(f"{name.capitalize()} победили!")
        break

    if turns_made >= 9:
        print_field(field)
        print("Ничья!")
        break

    x_turn = not x_turn