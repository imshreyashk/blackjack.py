# blackjack.py
import random

def deal_card():
    cards = [2, 3, 4, 5, 6, 7, 8, 9, 10, "J", "Q", "K", "A"]
    return random.choice(cards)

def calculate_hand(hand):
    total = 0
    ace_count = 0
    for card in hand:
        if card == "J" or card == "Q" or card == "K":
            total += 10
        elif card == "A":
            ace_count += 1
            total += 11
        else:
            total += card
    while total > 21 and ace_count > 0:
        total -= 10
        ace_count -= 1
    return total

def hit(hand):
    hand.append(deal_card())

def play_blackjack():
    player_hand = []
    dealer_hand = []

    for _ in range(2):
        hit(player_hand)
        hit(dealer_hand)

    while True:
        print("Your hand:", player_hand)
        print("Your total:", calculate_hand(player_hand))
        hit_or_stay = input("Hit or Stay (h/s): ")
        if hit_or_stay.lower() == "h":
            hit(player_hand)
            if calculate_hand(player_hand) > 21:
                print("Bust! You lose.")
                return
        else:
            break

    while calculate_hand(dealer_hand) < 17:
        hit(dealer_hand)

    player_total = calculate_hand(player_hand)
    dealer_total = calculate_hand(dealer_hand)
    print("Your hand:", player_hand, "Your total:", player_total)
    print("Dealer hand:", dealer_hand, "Dealer total:", dealer_total)

    if player_total > 21:
        print("Bust! You lose.")
    elif dealer_total > 21:
        print("Dealer busts! You win.")
    elif player_total > dealer_total:
        print("You win!")
    elif dealer_total > player_total:
        print("Dealer wins.")
    else:
        print("Tie!")

play_blackjack()
