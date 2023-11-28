# Progression-outcomes-as-defined-by-the-University-regulations
from graphics import GraphWin, Rectangle, Point, Text

def determine_progress(pass_, defer, fail):
    try:
        total = pass_ + defer + fail
        if total != 120:
            return "Total incorrect"
        else:
            if pass_ == 120:
                return "Progress"
            elif pass_ == 100 and (defer == 20 or fail == 20):
                return "Progress (module trailer)"
            elif fail >= 80:
                return "Exclude"
            else:
                return "Do not progress – module retriever"

    except ValueError:
        return "Integer required"

# Initialize counters for each category
results = {
    "Progress": 0,
    "Progress (module trailer)": 0,
    "Exclude": 0,
    "Do not progress – module retriever": 0
}

# Initialize an empty list to store input data sets
data_sets = []

while True:
    try:
        pass_ = int(input("Please enter your credits at pass: "))
        if pass_ not in range(0, 130, 20):
            print("Out of range")
            continue

        defer = int(input("Please enter your credits at defer: "))
        if defer not in range(0, 130, 20):
            print("Out of range")
            continue

        fail = int(input("Please enter your credits at fail: "))
        if fail not in range(0, 130, 20):
            print("Out of range")
            continue

        result = determine_progress(pass_, defer, fail)
        print(result)

        # Increment the respective category count
        results[result] += 1

        # Append the input data as a tuple (pass_, defer, fail) to the list
        data_sets.append((pass_, defer, fail))

        choice = input("Would you like to enter another set of data? Enter 'y' for yes or 'q' to quit: ")
        if choice.lower() == 'q':
            break

    except ValueError:
        print("Integer required for credits.")

# Save progression data to a text file (Part 2)
with open('progression_data.txt', 'w') as file:
    for data in data_sets:
        file.write(f"{data[0]}, {data[1]}, {data[2]}\n")

# Display Histogram (Part 1)
win = GraphWin("Histogram Results", 400, 300)
# (Code for histogram)

# Display stored progression data from the text file (Part 3)
print("\nPart 3:")
with open('progression_data.txt', 'r') as file:
    for line in file:
        pass_, defer, fail = map(int, line.strip().split(', '))
        print(f"{'Progress' if pass_ == 120 else 'Progress (module trailer)' if pass_ == 100 and (defer == 20 or fail == 20) else 'Exclude' if fail >= 80 else 'Do not progress – module retriever'} - {pass_}, {defer}, {fail}")

# (Code for the histogram display)

win.getMouse()
win.close()
