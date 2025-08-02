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

Left Rotate an Array by One place:
## Brute Force/ Optimal solution TC=O(n)
    void rotateArrayByOne(vector<int>& nums) {
        int temp= nums[0];
        for(int i=1; i<nums.size(); i++){
            nums[i-1]= nums[i];
        }
        nums[nums.size()-1]= temp;
    }

Left Rotate an Array by D places:
## Brute Force TC= O(n+d) SC= O(d)
    void rotateArray(vector<int>& nums, int d) {
        d= d % nums.size();
        vector<int>temp;
        for(int i=0; i<d; i++){
            temp.push_back(nums[i]);
        }
        for(int i=d; i<nums.size(); i++){
            nums[i-d]= nums[i];
        }
        int j=0;
        for(int i=nums.size()-d; i<nums.size(); i++){
            nums[i]= temp[j];
            j++;
        }    
    }
        //we can also change the last for loop directly into this
        
    for(int i=nums.size()-d; i<nums.size(); i++){
            nums[i]= temp[i-(nums.size()-d)];
        }
## Optimal solution TC= O(2n) SC= O(1)
    void rotateArray(vector<int>& nums, int d) {
        if(nums.size() == 0) return;
        d= d % nums.size();
        reverse(nums.begin(), nums.begin()+d);
        reverse(nums.begin()+d, nums.end());
        reverse(nums.begin(), nums.end());
    }
    //if asked to write reverse without using STL
    void reverse(int arr[], int start, int end){
        while(start <= end){
            int temp= arr[start];
            arr[start]= arr[end];
            arr[end]= temp;
            start++;
            end--;
        }
    }
    
Move Zeroes to End:
## Brute Force Tc= O(2n) SC= O(n)
    void moveZeroes(vector<int>& nums) {
        vector<int> temp;
        for(int i=0; i<nums.size(); i++){
            if(nums[i]) temp.push_back(nums[i]);
        }
        for(int i=0; i<temp.size(); i++){
            nums[i]= temp[i];
        }
        for(int i=temp.size(); i<nums.size(); i++){
            nums[i]=0;
        }
    }
## Optimal solution TC = O(n) SC= O(1)
    vector moveZeroes(vector<int>& nums) {
        int j=-1;
        for(int i=0; i<nums.size(); i++){
            if(nums[i] == 0) j = i;
            break;
        }
        if(j == -1) return nums;
        for(int i=j+1; i<n; i++){
            if(nums[i]) swap(nums[j], nums[i]);
            j++;
        }
    }

Linear Search:
Means search the element in the array and return the front most index where element is present if absent return -1

    int LinearSearch(vector<int>& nums, int no){
        for(int i=0; i<nums.size(); i++){
            if(nums[i] == no) return i;
        }
        return -1;
    }

Find the Union of two sorted Array:
## Brute Force TC= O(n+m) log(n+m) SC= O(n+m)
    vector<int> unionArray(vector<int>& nums1, vector<int>& nums2) {
        set<int> st;
        for(int i=0; i<nums1.size(); i++){
            st.insert(nums1[i]);
        }
        for(int i=0; i<nums2.size(); i++){
            st.insert(nums2[i]);
        }
        vector<int> unionVec;
        for(auto it: st){
            unionVec.push_back(it);
        }
        return unionVec;
    }
## Optimal solution TC= O(n+m) SC= O(n+m)
    vector<int> unionArray(vector<int>& nums1, vector<int>& nums2) {
    int n1 = nums1.size();
    int n2 = nums2.size();
    int i = 0, j = 0;
    vector<int> unionVec;

    while(i < n1 && j < n2) {
        if(nums1[i] < nums2[j]) {
            if(unionVec.empty() || unionVec.back() != nums1[i]) {
                unionVec.push_back(nums1[i]);
            }
            i++;
        }
        else if(nums1[i] > nums2[j]) {
            if(unionVec.empty() || unionVec.back() != nums2[j]) {
                unionVec.push_back(nums2[j]);
            }
            j++;
        }
        else {  
            if(unionVec.empty() || unionVec.back() != nums1[i]) {
                unionVec.push_back(nums1[i]);
            }
            i++;
            j++;
        }
    }
    //lets say one of the array got exhausted and other remains
        while(i < n1) {
            if(unionVec.empty() || unionVec.back() != nums1[i]) {
                unionVec.push_back(nums1[i]);
            }
            i++;
        }
        while(j < n2) {
            if(unionVec.empty() || unionVec.back() != nums2[j]) {
                unionVec.push_back(nums2[j]);
            }
            j++;
        }

        return unionVec;
    }

Find the Missing Number in an Array:
## Brute Force
