# Array_DSA-1

Finding Largest element of an Array:
## Brute Force TC= O(n logn)
    int largestElement(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        return nums[nums.size()-1];
    }
## Optimal solution TC= O(n)
    int largestElement(vector<int>& nums) {
        int largest= nums[0];
        for(int i=1; i<nums.size(); i++){
            if(largest < nums[i]) largest= nums[i];
        }
        return largest;
    }

Second Largest element in an Array without sorting:
## Brute Force TC= O(n)
    int secondLargestElement(vector<int>& nums) {
        int largest = nums[0];
        
        // First pass: find largest
        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] > largest)
                largest = nums[i];
        }
        
        int second = INT_MIN;
        // Second pass: find second largest
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] < largest && nums[i] > second)
                second = nums[i];
        }
        
        return (second == INT_MIN) ? 0 : second;
    }
## Optimal solution TC= O(n)
    int secondLargestElement(vector<int>& nums) {
        int first = INT_MIN, second = INT_MIN;
        for (int num : nums) {
            if (num > first) {
                second = first;
                first = num;
            } else if (num > second && num < first) {
                second = num;
            }
            return (second == INT_MIN) ? -1 : second;
        }
    }

## To check if Array is sorted
