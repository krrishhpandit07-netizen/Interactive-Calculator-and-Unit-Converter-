
"""
PROJECT: Professional Interactive Calculator & Unit Converter
LANGUAGE: Python 3
LEVEL: Internship / Intermediate
"""

from datetime import datetime



calculation_history = []




def get_number(message):
    """Accept only valid numeric input."""

    while True:
        try:
            return float(input(message))

        except ValueError:
            print("Invalid input! Please enter a valid number.")


def get_choice(message, minimum, maximum):
    """Validate menu choices."""

    while True:
        try:
            choice = int(input(message))

            if minimum <= choice <= maximum:
                return choice

            print(f"Please enter a number between {minimum} and {maximum}.")

        except ValueError:
            print("Invalid choice! Enter a whole number.")


def save_history(operation, result):
    """Save calculations with date and time."""

    record = {
        "operation": operation,
        "result": result,
        "time": datetime.now().strftime("%d-%m-%Y %H:%M:%S")
    }

    calculation_history.append(record)




def addition(a, b):
    return a + b


def subtraction(a, b):
    return a - b


def multiplication(a, b):
    return a * b


def division(a, b):

    if b == 0:
        raise ZeroDivisionError("Cannot divide by zero.")

    return a / b


def power(a, b):
    return a ** b


def modulus(a, b):

    if b == 0:
        raise ZeroDivisionError("Cannot calculate modulus by zero.")

    return a % b


def percentage(a, b):
    """Calculate a percentage of a number."""

    return (a * b) / 100


def calculator():

    while True:

        print("\n========== ADVANCED CALCULATOR ==========")
        print("1. Addition")
        print("2. Subtraction")
        print("3. Multiplication")
        print("4. Division")
        print("5. Power")
        print("6. Modulus")
        print("7. Percentage")
        print("8. Back to Main Menu")

        choice = get_choice("Select operation: ", 1, 8)

        if choice == 8:
            break

        num1 = get_number("Enter first number: ")
        num2 = get_number("Enter second number: ")

        try:

            if choice == 1:
                result = addition(num1, num2)
                operation = f"{num1} + {num2}"

            elif choice == 2:
                result = subtraction(num1, num2)
                operation = f"{num1} - {num2}"

            elif choice == 3:
                result = multiplication(num1, num2)
                operation = f"{num1} * {num2}"

            elif choice == 4:
                result = division(num1, num2)
                operation = f"{num1} / {num2}"

            elif choice == 5:
                result = power(num1, num2)
                operation = f"{num1} ** {num2}"

            elif choice == 6:
                result = modulus(num1, num2)
                operation = f"{num1} % {num2}"

            elif choice == 7:
                result = percentage(num1, num2)
                operation = f"{num2}% of {num1}"

            if isinstance(result, complex):
                print("Complex results are not supported.")
                continue

            if isinstance(result, float) and not __import__("math").isfinite(result):
                print("Error: Result is too large.")
                continue

            print("\nResult:", result)

            save_history(operation, result)

        except (ZeroDivisionError, OverflowError, ValueError) as error:
            print("Calculation Error:", error)


def length_converter():

    print("\n========== LENGTH CONVERTER ==========")
    print("1. Kilometers to Miles")
    print("2. Miles to Kilometers")
    print("3. Meters to Kilometers")
    print("4. Kilometers to Meters")
    print("5. Centimeters to Inches")
    print("6. Inches to Centimeters")

    choice = get_choice("Select conversion: ", 1, 6)

    value = get_number("Enter value: ")

    conversions = {
        1: (value * 0.621371, "Miles"),
        2: (value / 0.621371, "Kilometers"),
        3: (value / 1000, "Kilometers"),
        4: (value * 1000, "Meters"),
        5: (value / 2.54, "Inches"),
        6: (value * 2.54, "Centimeters")
    }

    result, unit = conversions[choice]

    print(f"Converted Value: {result:.4f} {unit}")

    save_history("Length Conversion", f"{result:.4f} {unit}")


def temperature_converter():

    print("\n========== TEMPERATURE CONVERTER ==========")
    print("1. Celsius to Fahrenheit")
    print("2. Fahrenheit to Celsius")
    print("3. Celsius to Kelvin")
    print("4. Kelvin to Celsius")

    choice = get_choice("Select conversion: ", 1, 4)

    value = get_number("Enter temperature: ")

    if choice in (1, 2, 3) and value < -273.15:
        print("Error: Temperature is below absolute zero.")
        return

    if choice == 1:
        result = (value * 9/5) + 32
        unit = "Fahrenheit"

    elif choice == 2:
        result = (value - 32) * 5/9
        unit = "Celsius"

    elif choice == 3:
        result = value + 273.15
        unit = "Kelvin"

    else:
        if value < 0:
            print("Kelvin cannot be negative.")
            return

        result = value - 273.15
        unit = "Celsius"

    print(f"Converted Temperature: {result:.2f} {unit}")

    save_history("Temperature Conversion", f"{result:.2f} {unit}")




def weight_converter():

    print("\n========== WEIGHT CONVERTER ==========")
    print("1. Kilograms to Grams")
    print("2. Grams to Kilograms")
    print("3. Kilograms to Pounds")
    print("4. Pounds to Kilograms")

    choice = get_choice("Select conversion: ", 1, 4)

    value = get_number("Enter weight: ")

    if value < 0:
        print("Weight cannot be negative.")
        return

    if choice == 1:
        result = value * 1000
        unit = "Grams"

    elif choice == 2:
        result = value / 1000
        unit = "Kilograms"

    elif choice == 3:
        result = value * 2.20462
        unit = "Pounds"

    else:
        result = value / 2.20462
        unit = "Kilograms"

    print(f"Converted Weight: {result:.4f} {unit}")

    save_history("Weight Conversion", f"{result:.4f} {unit}")




def time_converter():

    print("\n========== TIME CONVERTER ==========")
    print("1. Hours to Minutes")
    print("2. Minutes to Seconds")
    print("3. Hours to Seconds")
    print("4. Days to Hours")

    choice = get_choice("Select conversion: ", 1, 4)

    value = get_number("Enter value: ")

    if value < 0:
        print("Time cannot be negative.")
        return

    if choice == 1:
        result = value * 60
        unit = "Minutes"

    elif choice == 2:
        result = value * 60
        unit = "Seconds"

    elif choice == 3:
        result = value * 3600
        unit = "Seconds"

    else:
        result = value * 24
        unit = "Hours"

    print(f"Converted Time: {result:.2f} {unit}")

    save_history("Time Conversion", f"{result:.2f} {unit}")




def show_history():

    print("\n========== CALCULATION HISTORY ==========")

    if not calculation_history:
        print("No calculations found.")
        return

    for index, record in enumerate(calculation_history, start=1):

        print(f"\nRecord {index}")
        print("Operation:", record["operation"])
        print("Result:", record["result"])
        print("Date:", record["time"])


def clear_history():

    calculation_history.clear()

    print("Calculation history cleared successfully.")




def main():

    print("\n============================================")
    print("   PROFESSIONAL CALCULATOR & UNIT CONVERTER")
    print("============================================")
    print("Developed using Python 3")

    while True:

        print("\n============== MAIN MENU ==============")
        print("1. Advanced Calculator")
        print("2. Length Converter")
        print("3. Temperature Converter")
        print("4. Weight Converter")
        print("5. Time Converter")
        print("6. View Calculation History")
        print("7. Clear Calculation History")
        print("8. Exit")
        print("=======================================")

        choice = get_choice("Enter your choice (1-8): ", 1, 8)

        if choice == 1:
            calculator()

        elif choice == 2:
            length_converter()

        elif choice == 3:
            temperature_converter()

        elif choice == 4:
            weight_converter()

        elif choice == 5:
            time_converter()

        elif choice == 6:
            show_history()

        elif choice == 7:
            clear_history()

        elif choice == 8:
            print("\nThank you for using our application!")
            print("Program closed successfully.")
            break



if __name__ == "__main__":
    main()
