import random

deck = ['A♠', 'K♠', 'Q♠', 'J♠', '10♠', '9♠', '8♠', '7♠', '6♠', '5♠', '4♠', '3♠', '2♠',
        'A♥', 'K♥', 'Q♥', 'J♥', '10♥', '9♥', '8♥', '7♥', '6♥', '5♥', '4♥', '3♥', '2♥',
        'A♦', 'K♦', 'Q♦', 'J♦', '10♦', '9♦', '8♦', '7♦', '6♦', '5♦', '4♦', '3♦', '2♦',
        'A♣', 'K♣', 'Q♣', 'J♣', '10♣', '9♣', '8♣', '7♣', '6♣', '5♣', '4♣', '3♣', '2♣']
og_deck = deck[:]  # Copy of the deck for resetting

deck_values = [11, 10, 10, 10, 10, 9, 8, 7, 6, 5, 4, 3, 2] * 4  # Each card's numeric value

def blackJack(name, deposit):  # Main function that is originally called
    global deck, deck_values
    deck = og_deck[:]  # Reset the deck
    deck_values = [11, 10, 10, 10, 10, 9, 8, 7, 6, 5, 4, 3, 2] * 4  # Reset deck values

    if deposit <= 0:  # Prevents the user from playing without money
        print("Sorry, looks like you run out of money!")
        return

    print(f"\nYour current total is: ${deposit}")
    bet = int(input("How much would you like to bet (In whole dollars)? "))

    if bet > deposit:  # To make sure the user has enough money
        print("Try betting a smaller value than your total!")
        return blackJack(name, deposit)

    print(f"{name} bet ${bet}, let's deal the cards.")

    player_card_1_value = random.randrange(len(deck))
    player_card_1 = deck.pop(player_card_1_value)
    player_card_1_val = deck_values.pop(player_card_1_value)

    player_card_2_value = random.randrange(len(deck))
    player_card_2 = deck.pop(player_card_2_value)
    player_card_2_val = deck_values.pop(player_card_2_value)

    # Ensure two unique cards are drawn
    if player_card_1 == player_card_2:
        player_card_2_value = random.randrange(len(deck))
        player_card_2 = deck.pop(player_card_2_value)
        player_card_2_val = deck_values.pop(player_card_2_value)

    player_card_total = player_card_1_val + player_card_2_val

    dealer_card_1_value = random.randrange(len(deck))
    dealer_card_1 = deck[dealer_card_1_value]

    print("\nHere are your two cards:")
    print(f"{player_card_1}  {player_card_2}")
    print("\nHere are the dealer's cards (Only 1 is visible to the player)")
    print(f"{dealer_card_1}  ⍰\n")

    if player_card_total == 21:
        deposit += bet
        print(f"You got BLACKJACK! You won ${bet}. Your new total is ${deposit}")
        return play_again(name, deposit)
    else:
        hit_or_stay(name, deposit, bet, player_card_total, dealer_card_1_value, dealer_card_1)

def hit_or_stay(name, deposit, bet, player_card_total, dealer_card_1_value, dealer_card_1):
    global deck, deck_values
    hit_stay = input(f"Your numeric total is {player_card_total}, would you like to 'Hit' or 'Stay'? ").capitalize()

    if hit_stay == 'Hit':
        hit_card_value = random.randrange(len(deck))
        hit_card = deck.pop(hit_card_value)
        hit_card_val = deck_values.pop(hit_card_value)

        player_card_total += hit_card_val
        
        print(f"\nHIT! You drew {hit_card}")
        
        if player_card_total < 21:
            hit_or_stay(name, deposit, bet, player_card_total, dealer_card_1_value, dealer_card_1)
        elif player_card_total == 21:
            deposit += bet
            print(f"You got BLACKJACK! You won ${bet}. Your new total is ${deposit}")
            return play_again(name, deposit)
        else:
            deposit -= bet
            print(f"You BUST! Your numeric value is {player_card_total}. You lost ${bet}. Your new total is ${deposit}")
            return play_again(name, deposit)
    else:
        print(f"You choose to stay. Your numeric total is {player_card_total}.")
        dealers_turn(name, deposit, bet, player_card_total, dealer_card_1_value, dealer_card_1)

def dealers_turn(name, deposit, bet, player_card_total, dealer_card_1_value, dealer_card_1):
    global deck, deck_values
    print("\nThe dealer will now reveal their other card.")

    dealer_card_2_value = random.randrange(len(deck))
    dealer_card_2 = deck.pop(dealer_card_2_value)
    dealer_card_2_val = deck_values.pop(dealer_card_2_value)

    dealer_card_total = deck_values[dealer_card_1_value] + dealer_card_2_val

    print(f"{dealer_card_1}  {dealer_card_2}")

    while dealer_card_total < 16:
        print("The dealer has to hit!")
        dealer_hit_card_value = random.randrange(len(deck))
        dealer_hit_card = deck.pop(dealer_hit_card_value)
        dealer_hit_card_val = deck_values.pop(dealer_hit_card_value)
        dealer_card_total += dealer_hit_card_val
        print(f"Dealer drew {dealer_hit_card}")

    results(name, deposit, bet, player_card_total, dealer_card_total)

def results(name, deposit, bet, player_card_total, dealer_card_total):
    if dealer_card_total > 21:
        deposit += bet
        print(f"The dealer BUSTED! Their numeric value is {dealer_card_total}. You won ${bet}. Your new total is ${deposit}")
    elif dealer_card_total > player_card_total:
        deposit -= bet
        print(f"The dealer wins with {dealer_card_total} over your {player_card_total}. You lost ${bet}. Your new total is ${deposit}")
    elif dealer_card_total < player_card_total:
        deposit += bet
        print(f"You won with {player_card_total} over the dealer's {dealer_card_total}! You won ${bet}. Your new total is ${deposit}")
    else:
        print(f"It's a push! You both scored {player_card_total}. Your total remains ${deposit}")
    
    play_again(name, deposit)

def play_again(name, deposit):
    choice = input("Do you want to play again? ('Yes' or 'No') ").capitalize()
    if choice == 'Yes':
        blackJack(name, deposit)
    else:
        print(f"\n{name}, your total is ${deposit}. Thank you for playing! ")

# Start the game
user_name = input("Please enter your name: ")
user_deposit = int(input(f"Welcome {user_name}! How much money would you like to deposit? (In whole dollars) $"))
blackJack(user_name, user_deposit)
