def makeChange():
    """
    This function calculates all the ways to represent a value in cents using
    coins of 25, 10, 5, and 1 cent, using dynamic programming.

    How it works:
    - Gets the user input for the value in cents.
    - Creates a DP table where dp[i] contains all combinations to form the value i.
    - Iterates over each coin type and updates dp[i] based on previously solved subproblems.
    - Prints the found combinations and returns the result.
    """
    
    n = int(input("Enter the amount in cents: "))

    # Define the coin values
    coins = [25, 10, 5, 1]

    # Initialize the DP table with empty sets to store combinations
    dp = [set() for _ in range(n + 1)]
    dp[0].add((0, 0, 0, 0))

    # Update the combinations in dp for each coin
    for coin_idx, coin in enumerate(coins):
        for i in range(coin, n + 1):
            for comb in dp[i - coin]:
                # Update the combination by adding 1 coin of the current type
                new_comb = list(comb)
                new_comb[coin_idx] += 1
                dp[i].add(tuple(new_comb))

    # Convert the set of combinations into a list of lists
    result = [list(comb) for comb in dp[n]]
    print(f"The possible combinations to make {n} cents are:")
    for comb in sorted(result):
        print(comb)
    return result

makeChange()
