-def is_leap_year(year):
    # Check if the year is a leap year
    if year % 4 == 0:
        if year % 100 == 0:
            if year % 400 == 0:
                return True
            else:
                return False
        else:
            return True
    else:
        return False


def get_month_days(year, month):
    # Get the number of days in a given month
    if month in [1, 3, 5, 7, 8, 10, 12]:
        return 31
    elif month == 2:
        if is_leap_year(year):
            return 29
        else:
            return 28
    else:
        return 30


def get_starting_day(year, month):
    # Calculate the starting day of the month
    # Zeller's Congruence algorithm is used to find the day of the week
    if month < 3:
        month += 12
        year -= 1
    q = 1
    K = year % 100
    J = year // 100
    h = (q + 13*(month + 1)//5 + K + K//4 + J//4 + 5*J) % 7
    # Zeller's algorithm returns 0 = Saturday, 1 = Sunday, ..., 6 = Friday
    # Adjusting to return 0 = Sunday, 1 = Monday, ..., 6 = Saturday
    return (h + 5) % 7


def print_calendar(year, month):
    # Print the calendar for a given year and month
    month_names = ['January', 'February', 'March', 'April', 'May', 'June', 'July',
                   'August', 'September', 'October', 'November', 'December']
    
    # Print the month and year
    print(f'{month_names[month-1]} {year}')
    
    # Print the days of the week
    print('Sun Mon Tue Wed Thu Fri Sat')
    
    # Get the starting day of the month
    starting_day = get_starting_day(year, month)
    
    # Print the empty spaces for the starting day
    print('    ' * starting_day, end='')
    
    # Print the days of the month
    for day in range(1, get_month_days(year, month) + 1):
        print(f'{day:2d}  ', end='')
        
        # Move to the next line after Saturday
        if (day + starting_day) % 7 == 0:
            print()
    
    # Move to the next line after printing the calendar
    print()


# Taking input from the user
year = int(input("Enter the year: "))
month = int(input("Enter the month number: "))

# Displaying the calendar
print_calendar(year, month)
