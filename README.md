# Advanced Programming Sem 6 
#include <iostream>
#include <vector>
#include <unordered_map>
#include <unordered_set>
#include <algorithm>
using namespace std;

// 1. Remove Duplicates from a Sorted Array
int removeDuplicates(vector<int>& nums) {
    if (nums.empty()) return 0;
    int sz = 1;
    for (int i = 1; i < nums.size(); i++) {
        if (nums[i] != nums[sz - 1]) {
            nums[sz++] = nums[i];
        }
    }
    return sz;
}

// 2. Implementing Insertion Sort
void insertionSort(vector<int>& arr) {
    for (int i = 1; i < arr.size(); i++) {
        int key = arr[i], j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

// 3. Contains Duplicate
bool containsDuplicate(vector<int>& nums) {
    unordered_set<int> seen;
    for (int num : nums) {
        if (!seen.insert(num).second) return true;
    }
    return false;
}

// 4. Two Sum
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> map;
    for (int i = 0; i < nums.size(); i++) {
        int complement = target - nums[i];
        if (map.count(complement)) {
            return {map[complement], i};
        }
        map[nums[i]] = i;
    }
    return {};
}

// 5. Jump Game
bool canJump(vector<int>& nums) {
    int maxReach = 0;
    for (int i = 0; i < nums.size(); i++) {
        if (i > maxReach) return false;
        maxReach = max(maxReach, nums[i] + i);
    }
    return true;
}

// 6. Majority Element
int majorityElement(vector<int>& nums) {
    unordered_map<int, int> map;
    int count = nums.size() / 2;
    for (int num : nums) {
        if (++map[num] > count) return num;
    }
    return -1;
}

// 7. Valid Palindrome
bool isPalindrome(string s) {
    string cleaned;
    for (char c : s) {
        if (isalnum(c)) cleaned += tolower(c);
    }
    return equal(cleaned.begin(), cleaned.end(), cleaned.rbegin());
}

// 8. Jump Game 2
int jump(vector<int>& nums) {
    int near = 0, far = 0, jumps = 0;
    while (far < nums.size() - 1) {
        int farthest = 0;
        for (int i = near; i <= far; i++) {
            farthest = max(farthest, i + nums[i]);
        }
        near = far + 1;
        far = farthest;
        jumps++;
    }
    return jumps;
}

// 9. 3Sum
vector<vector<int>> threeSum(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    vector<vector<int>> res;
    for (int i = 0; i < nums.size(); i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue;
        int j = i + 1, k = nums.size() - 1;
        while (j < k) {
            int total = nums[i] + nums[j] + nums[k];
            if (total > 0) {
                k--;
            } else if (total < 0) {
                j++;
            } else {
                res.push_back({nums[i], nums[j], nums[k]});
                while (j < k && nums[j] == nums[j + 1]) j++;
                j++;
            }
        }
    }
    return res;
}

// 10. Set Matrix Zeroes
void setZeroes(vector<vector<int>>& matrix) {
    int m = matrix.size(), n = matrix[0].size();
    vector<bool> row(m, false), col(n, false);
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (matrix[i][j] == 0) {
                row[i] = col[j] = true;
            }
        }
    }
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (row[i] || col[j]) matrix[i][j] = 0;
        }
    }
}

// 11. Longest Substring Without Repeating Characters
int lengthOfLongestSubstring(string s) {
    unordered_set<char> charSet;
    int left = 0, maxLength = 0;
    for (int right = 0; right < s.size(); right++) {
        while (charSet.count(s[right])) {
            charSet.erase(s[left++]);
        }
        charSet.insert(s[right]);
        maxLength = max(maxLength, right - left + 1);
    }
    return maxLength;
}

// 12. Find the Duplicate Number
int findDuplicate(vector<int>& nums) {
    unordered_set<int> seen;
    for (int num : nums) {
        if (!seen.insert(num).second) return num;
    }
    return -1;
}
