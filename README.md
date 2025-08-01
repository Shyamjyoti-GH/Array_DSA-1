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

To check if Array is sorted:
## Brute Force / Optimal solution TC= O(n)
    bool isSorted(vector<int>& nums){
        //your code goes here
        for(int i=0; i<nums.size()-1; i++){
            if(nums[i] > nums[i+1]) return false;
        }
        return true;
    }
Remove Duplicates  from a sorted array:
## Brute Force TC= O(n^2) SC=O(1)
    int removeDuplicates(vector<int>& nums) {
        if(nums.empty()) return 0;
        for(int i=0;i<nums.size()-1;){
            if(nums[i] == nums[i+1]){
                nums.erase(nums.begin() + i);
            }
            else i++;
        }
        return nums.size();
    }
## Average Case TC= O(n logn) SC= O(n)
    int removeDuplicates(vector<int>& nums) {
        set<int> st;
        for(int i=0; i<nums.size(); i++){
            st.insert(nums[i]);
        }
        int idx=0;
        for(auto it: st){
            nums[idx]= it;
            idx++;
        }
        return idx;
    }
## Optimal solution TC= O(n)
    int removeDuplicates(vector<int>& nums) {
        int i=nums[0];
        int idx=1;
        for(int j=1; j<nums.size(); j++){
            if(nums[j] != i){
                nums[idx]=nums[j];
                i= nums[j];
                idx++;
            } 
        }
        return idx;
    }
