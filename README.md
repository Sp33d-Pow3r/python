# python
This is where I can get feedback on my python projects
I have just started coding with python

This is code for a number guessing game 
But I'm sure I can make it better somehow, any suggestions?

import random
import time
import socket

hostname = socket.gethostname()
local_ip = socket.gethostbyname(hostname)
# Defines the boolean variables for game state
last_win = False
loser = False
winner = False
factor_limited = False
multiple_limited = False
greater_limited = False
eliminated_limited = False
even_odd_limited = False
add_limited = False
multiply_limited = False
hot_cold_limited = False
prime_limited = False

dot_dot_dot = "... "
illiterate_meter = 0
#Add unlimited and limited option
#This will either give player 1 of each section or unlimited of each section

#MAKE A HOT COLD FOR THE NUMBER GUESSING GAME

#Tkinter
'''
def print_with_delay(text, delay=0.3,):
    for char in text:
        print(char, end='', flush=True)
        time.sleep(delay)
        time.sleep(1)  # Delay between character prints
    print('\n') 

'''

#When I learn to use def

print("In this game you will guess a number between 1 and 100-5000 depending on difficulty")
print("You will choose clues to help you guess the number and will have 3-10 based off difficulty\n")


limited = input("Do you want to play with one of each clue or unlimited? (limited/unlimited): \n").lower().strip()
while True:
    if limited == "limited":
        print("You will only be able to use one of each clue except for guess\n")
        limited = True
        break
    elif limited == "unlimited":
        print("You will be able to use unlimited clues\n")
        limited = False
        break
    elif limited == "butterfingers":
        dot_dot_dot = "... "
        for char in dot_dot_dot:
            print(char, end='', flush=True)
            time.sleep(1)
        print(f"dude {hostname} and {local_ip} get humbled")
        print("You getting put on limited now\n")
        limited = True
        break
    else:
        print("Didn't quite catch that, try again\n")
        time.sleep(1)
        limited = input("Do you want to play with one of each clue or unlimited? (limited/unlimited): \n").lower().strip()


difficulty = input("Choose difficulty: easy, medium, hard or impossible: \n").lower().strip()
while True:
    if difficulty == "easy":
        number_range = 100
        number = random.randint(1, number_range)
        attempts = 10
        break
    elif difficulty == "medium":
        number_range = 500
        number = random.randint(1, number_range)
        attempts = 7
        break
    elif difficulty == "hard":
        number_range = 1000
        number = random.randint(1, number_range)
        attempts = 5
        break
    elif difficulty == "impossible":
        number_range = 5000
        number = random.randint(1, number_range)
        attempts = 3
        break
    elif illiterate_meter < 10 or illiterate_meter > 10 and illiterate_meter < 20 and difficulty not in ["easy", "medium", "hard", "impossible"]:
        print("That's not a difficulty, try again\n")
        illiterate_meter += 1
        time.sleep(0.1)
        difficulty = input("Choose difficulty: easy, medium, hard or impossible: \n").lower().strip()
    elif illiterate_meter == 10 and difficulty not in ["easy", "medium", "hard", "impossible"]:
        print("Are you blind and illiterate? Dude, EASY, MEDIUM, HARD or IMPOSSIBLE\n")
        illiterate_meter += 1
        time.sleep(1)
        difficulty = input("Choose difficulty: easy, medium, hard or impossible: \n").lower().strip()
        continue
    elif illiterate_meter >= 20 and difficulty not in ["easy", "medium", "hard", "impossible"]:
        print("You are quite literally wasting power. You getting put on ultra extreme")
        difficulty = "ultra_extreme"
        attempts = 1
        number_range = 100000
        number = random.randint(1, number_range)
        time.sleep(1)
        print("Yeah good luck now hahahahhahahaha")
        break
print(f"\n\nYou have {attempts} attempts to guess the number between 1 and {number_range}\n")
print(("You have certain clues to help you guess the number\n"))
print("These are: multiple, factor, greater, eliminate, even/odd, add, multiply, hot/cold, prime and of course, guess\n")
help = input("For help type 'help' or type anything else to continue: \n").lower().strip()
if help == "help":
    print("You can use the clues to help you guess the number\n")
    print("multiple: will tell you a multiple of the number")
    print("factor: will tell you a factor of the number")
    print("greater: will ask you for a number and will tell you if the number is greater than your guess")
    print("eliminate: will eliminate 10 random numbers from the number_range")
    print("even/odd: will tell you if the number is even or odd")
    print("add: will add all the digits of the number")
    print("multiply: will multiply all the digits of the number\n")
    print("You can also type 'hot/cold' followed by a number to see how close you are to the number\n")
    print("prime: will tell you if the number is prime or not\n")
    print("You can also guess the number by typing 'guess' and then the number\n")
    print("To check your attempts, type 'attempts'\n")
    time.sleep(2)
else:
    print("Let's begin!\n")
    time.sleep(1)

searching_dot = 0
searching_repeat = random.randint(4,8)
while searching_repeat > 0:    
        while searching_dot < 4:
            print('Selecting Number'+ '.' * searching_dot, end="\r")
            searching_dot += 1
            time.sleep(0.5)
            print("\033[K", end="\r")
        searching_dot = 0
        searching_repeat -= 1

time.sleep(1)
print("Number Selected!\n")
print("""         ------------------------------------------------------------------------------
         |multiple|factor|greater|eliminate|even/odd|add|multiply|hot/cold|prime|guess|
         ------------------------------------------------------------------------------\n""")

cmd = input ("Type a command:> \n").lower().strip()

while True:    
    if attempts > 0:    
        if cmd == "multiple" and multiple_limited == False:
            print(f"A multiple of the number is: {number * random.randint(5, 90)}\n")
            multiple_limited = True if limited else False
            attempts -= 1
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "multiple" and multiple_limited == True:
            print("You have already used the multiple clue\n")
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "factor" and factor_limited == False:
            while True:
                factor = random.randint(1, number)
                if number % factor == 0 and factor < 30: #If factor > 30 it will give away too much info
                    # Ensure the factor is less than 30 for variety
                    print(f"A factor of the number is: {factor}\n")
                    attempts -= 1
                    cmd = input ("Type a command:> \n").lower().strip()
                    factor_limited = True if limited else False
                    break
                else:
                    continue
        elif factor_limited == True and cmd == "factor":
            print("You have already used the factor clue\n")
            cmd = input ("Type a command:> \n").lower().strip()             
        elif cmd == "greater" and greater_limited == False:
            greater_guess = input("Enter a number to compare:> \n")
            try:
                greater_guess = int(greater_guess)
            except ValueError:
                print("That's not a number, you nonce\n")
                time.sleep(1)
                print("You just lost a turn...\n")
                attempts -= 1
                cmd = input ("Type a command:> \n").lower().strip()
                continue
            if number > greater_guess:
                print(f'The number is greater than {greater_guess}\n')
            elif number < greater_guess:
                print(f'The number is less than {greater_guess}\n')
            elif number == greater_guess:
                print('That is definitely not the number\n')
            elif Exception:
                print("For being a smartass and not entering a number, you lose a turn\n")
                time.sleep(1)
            attempts -= 1
            greater_limited = True if limited else False
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "greater" and greater_limited == True:
            print("You have already used the greater clue\n")
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "eliminate" and eliminated_limited == False:
            eliminated_times = 10
            print("The following numbers will be eliminated from the number_range:\n")
            while eliminated_times > 0:    
                eliminated_number = random.randint(1, number_range)
                if eliminated_number == number:
                    print("Heh... was about to print the number...")
                    continue
                else:
                    print(f"{eliminated_number}\n")
                    time.sleep(0.5)
                    eliminated_times -= 1
            eliminated_limited = True if limited else False
            attempts -= 1
        elif cmd == "eliminate" and eliminated_limited == True:
            print("You have already used the eliminate clue\n")
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "even/odd" and even_odd_limited == False:
            if number % 2 == 0:
                print("\nnumber is even\n")
            else:
                print("\nnumber is odd\n")
            attempts -= 1
            even_odd_limited = True if limited else False
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "even/odd" and even_odd_limited == True:
            print("You have already used the even/odd clue\n")
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "add" and add_limited == False:
            digit_sum = sum(int(digit) for digit in str(number))
            print(f"The sum of the digits of the number is: {digit_sum}\n")
            attempts -= 1
            add_limited = True if limited else False
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "add" and add_limited == True:
            print("You have already used the add clue\n")
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "multiply" and multiply_limited == False:
            digit_product = 1
            for digit in str(number):
                digit_product *= int(digit)
            print(f"The product of the digits of the number is: {digit_product}\n")
            attempts -= 1
            multiply_limited = True if limited else False
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "multiply" and multiply_limited == True:
            print("You have already used the multiply clue\n")
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "hot/cold" and hot_cold_limited == False:
            hot_cold_guess = input("Enter a number to compare:> \n")
            try:
                hot_cold_guess = int(hot_cold_guess)
            except ValueError:
                print("That's not a number, you nonce\n")
                time.sleep(1)
                print("You just lost a turn...\n")
                attempts -= 1
                cmd = input ("Type a command:> \n").lower().strip()
                continue
            difference = abs(number - hot_cold_guess)
            if difference == 0:
                print("burning\n")
            elif difference <= 10:
                print("hot\n")
            elif difference <= 50:
                print("warm\n")
            elif difference <= 100:
                print("cold\n")
            elif difference > 100:
                print("freezing\n")
            attempts -= 1
            hot_cold_limited = True if limited else False
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "hot/cold" and hot_cold_limited == True:
            print("You have already used the hot/cold clue\n")
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "prime" and prime_limited == False:
            prime_number = 2
            while prime_number <= number:
                if number % prime_number == 0:
                    print('It is not a prime number\n')
                    break
                else:
                    prime_number += 1
            else:
                print('It is a prime number\n')
            attempts -= 1
            prime_limited = True if limited else False
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "prime" and prime_limited == True:
            print("You have already used the prime clue\n")
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "guess":
            guess = input("Enter your guess:> \n")
            if guess.isdigit():
                guess_int = int(guess)
                if guess_int == number:
                    win = "GREAT WORK!!!\n"
                    for char in win:
                        print(char, end='', flush=True)
                        time.sleep(0.3)  # Delay between character prints  
                    time.sleep(1)
                    winner = True
                    break
                elif guess_int < 1 or guess_int > number_range:
                    print(f"That's not in range >:( you just wasted a guess\n")
                    attempts -= 1
                else:
                    print("Wrong guess, try again!\n")
                    attempts -= 1
            else:
                print("That's not a number...\n")
            cmd = input ("Type a command:> \n").lower().strip()
        elif cmd == "attempts":
            print(f'You have {attempts} attempts left\n')
            time.sleep(1)
        elif cmd == "help":
            print("You can use the clues to help you guess the number\n")
            print("multiple: will tell you a multiple of the number")
            print("factor: will tell you a factor of the number")
            print("greater: will ask you for a number and will tell you if the number is greater than your guess")
            print("eliminate: will eliminate 10 random numbers from the number_range")
            print("even/odd: will tell you if the number is even or odd")
            print("add: will add all the digits of the number")
            print("multiply: will multiply all the digits of the number\n")
            print("You can also type 'hot/cold' followed by a number to see how close you are to the number\n")
            print('prime: will tell you if the number is prime or not\n')
            print("You can also guess the number by typing 'guess' and then the number\n")
            print("To check your attempts, type 'attempts'\n")
            time.sleep(2)
        else: 
            print("Thats not a command... type 'help' for help \n")
            cmd = input ("Type a command:> \n").lower().strip()
    if attempts == 0:
        final_guess = (input("You have no attempts left, please guess the number here:> \n"))
        while True:    
            try:
                final_guess = int(final_guess)
                break
            except ValueError:
                print("That's not a number, you nonce\n")
                time.sleep(1)
                final_guess = input("Please guess the NUMBER here:> \n").lower().strip()
                # continue
        for char in dot_dot_dot:
                print(char, end='', flush=True)
                time.sleep(1)  # Delay between character prints
        if final_guess == number:
            time.sleep(1)
            print("Wow on the last guess you got it right! \n")
            time.sleep(1)
            print("Thanks for playing!\n")
            last_win = True
            break
        else:
            print(f'That was not the number, the number was {number}\n')
            print(f'Maybe {final_guess} was close though...?\n')
            print("Thanks for playing!\n")
            loser = True
            break

# This offers to play again

play_again = input("Do you want to play again? (yes/no): ").lower().strip()
while True:    
    if play_again == 'yes':
        print("Then reset the program...\n")
        break
    elif play_again == 'no' and last_win == True:
        print("So after your final LUCKY guess you are too good for this game?\n")
        break
    elif play_again == 'no' and loser == True:
        print("Hmph, someone is a sore loser...\n")
        break
    elif play_again == 'no' and winner == True:
        print("You really going to end on that? Get a streak going!\n")
        break
    else:
        print("I don't speak gibberish")
        time.sleep(1)
        play_again = input("Do you want to play again? (yes/no): ").lower().strip()

print("Thanks for playing!\n")
exit()
# This is the end of the number guessing game
