def read_marks_file(filename):
    marks = {}
    skipped = 0
    with open(filename, 'r') as file:
        for line in file:
            try:
                name, mark = line.strip().split(',')
                if not mark.isdigit():
                    raise ValueError
                marks[name] = int(mark)
            except:
                skipped += 1
    return marks, skipped

def print_summary(marks):
    if not marks:
        print("No valid data.")
        return
    for name, mark in marks.items():
        print(name, "→", mark)
    avg = sum(marks.values()) / len(marks)
    print("Average:", round(avg, 1))

while True:
    path = input("Enter file name: ")
    try:
        data, skipped = read_marks_file(path)
        print_summary(data)
        print("Skipped", skipped, "invalid entries.")
        break
    except FileNotFoundError:
        print("File not found. Try again.")
