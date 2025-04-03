his repository contains a C++ implementation of the 0/1 Knapsack problem using dynamic programming. The 0/1 Knapsack problem is a classic optimization problem that aims to maximize the total value of items that can be carried in a knapsack of a given capacity.

## Problem Statement

Given a set of items, each with a weight and a value, determine the maximum value that can be carried in a knapsack of a given capacity. Each item can either be included in the knapsack or excluded (hence the name 0/1).

### Input
- W: Maximum weight capacity of the knapsack.
- weights[]: Array of weights of the items.
- values[]: Array of values of the items.
- n: Number of items.

### Output
- Maximum value that can be carried in the knapsack.

## Code Explanation

The implementation uses a dynamic programming approach to solve the problem. The main steps are as follows:

1. *Initialization*: A 2D array dp is created where dp[i][w] represents the maximum value that can be attained with a weight limit w using the first i items.

2. *DP Table Construction*:
   - Iterate through each item and each weight capacity.
   - For each item, check if it can be included in the knapsack:
     - If the weight of the item is less than or equal to the current weight capacity, calculate the maximum value by either including or excluding the item.
     - If the item cannot be included, carry forward the value from the previous item.

3. *Result*: The maximum value that can be carried in the knapsack is found in dp[n][W].

## Code

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Function to solve the 0/1 Knapsack problem
int knapsack(int W, vector<int>& weights, vector<int>& values, int n) {
    // Create a 2D DP array
    vector<vector<int>> dp(n + 1, vector<int>(W + 1, 0));

    // Build the DP table
    for (int i = 1; i <= n; i++) {
        for (int w = 1; w <= W; w++) {
            // If the weight of the current item is less than or equal to the current capacity
            if (weights[i - 1] <= w) {
                // Take the maximum of including the item or excluding it
                dp[i][w] = max(dp[i - 1][w], dp[i - 1][w - weights[i - 1]] + values[i - 1]);
            } else {
                // If the item cannot be included, carry forward the value without it
                dp[i][w] = dp[i - 1][w];
            }
        }
    }

    // The maximum value that can be carried in the knapsack
    return dp[n][W];
}

int main() {
    int W = 50; // Maximum weight capacity of the knapsack
    vector<int> weights = {10, 20, 30}; // Weights of the items
    vector<int> values = {60, 100, 120}; // Values of the items
    int n = weights.size(); // Number of items

    int maxValue = knapsack(W, weights, values, n);
    cout << "Maximum value in Knapsack = " << maxValue << endl;

    return 0;
}
