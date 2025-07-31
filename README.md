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
## 
