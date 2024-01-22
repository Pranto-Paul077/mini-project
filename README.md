# TIC----TAC--TOE
It is a game
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
int main() {
    int n;
    cin >> n;

    vector<int> heights(n);
    for (int i = 0; i < n; i++) {
        cin >> heights[i];
    }

    int max_height = heights[0];
    int min_height = heights[0];
    int max_height_index = 0;
    int min_height_index = 0;

    for (int i = 1; i < n; i++) {
        if (heights[i] > max_height) {
            max_height = heights[i];
            max_height_index = i;
        }
        if (heights[i] <= min_height) {
            min_height = heights[i];
            min_height_index = i;
        }
    }
       int seconds = max_height_index + (n - 1 - min_height_index);
    if (max_height_index > min_height_index) {
        seconds--;
    }

    cout << seconds << endl;
 
    return 0;
}




