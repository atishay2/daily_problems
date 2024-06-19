# daily_problems
Leetcode_challenges


![2597  The Number of Beautiful Subsets](https://github.com/atishay2/daily_problems/assets/52835993/76e66250-c0ef-40c7-baf7-3c9e4d852181)

Solution: 

backtracking 

class Solution:
    
    def beautifulSubsets(self, nums: List[int], k: int) -> int:
        self.res = 0

        def backtrack(index, nums, k, visit):   
            for x in range(index, len(nums)):               
                if (nums[x]-k) in visit:               
                    continue
                self.res += 1
                visit[nums[x]] += 1
                backtrack(x+1, nums, k,visit)
                visit[nums[x]] -= 1
                if visit[nums[x]] == 0:
                    del visit[nums[x]]
        nums.sort()
        backtrack(0, nums, k, Counter())
        return self.res

LC : 994 Rotting Oranges
![image](https://github.com/atishay2/daily_problems/assets/52835993/7d2a423b-1534-49e2-a172-cc7fee6069a8)
![image](https://github.com/atishay2/daily_problems/assets/52835993/541043a6-98f6-4d8e-bd98-9defbc14531e)

    class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        q = collections.deque() ; fresh = 0
        ROW = len(grid) ; COL = len(grid[0])
        for x in range(ROW):
            for y in range(COL):
                if grid[x][y] == 1:
                    fresh += 1
                if grid[x][y] == 2:
                    q.append((x,y))
        count = 0 ; visit = set()
        while q and fresh > 0:
            qLen = len(q)

            for _ in range(qLen):
                cur_x, cur_y = q.popleft()

                for a, b in [(0,1),(0,-1), (1,0), (-1,0)]:
                    m, n = cur_x+a, cur_y+b

                    if 0 <= m < ROW and 0 <= n < COL and (m,n) not in visit and grid[m][n] == 1:
                        fresh -= 1
                        q.append((m,n))
                        visit.add((m,n))
            count += 1
        
        return count if fresh == 0 else -1

LC : 2486 Append Characters to String to Make Subsequence
![image](https://github.com/atishay2/daily_problems/assets/52835993/0e9757a8-c026-461f-b96a-20516685d9e3)
![image](https://github.com/atishay2/daily_problems/assets/52835993/d56956ca-9c5b-4658-a905-46fc1b4860a3)

    class Solution:
        def appendCharacters(self, s: str, t: str) -> int:
            r = 0
            for x in range(len(s)):
                
                if r < len(t) and s[x] == t[r] :
                    r += 1
            return len(t)-r

LC : 344. Reverse String

![image](https://github.com/atishay2/daily_problems/assets/52835993/f1222e26-494d-4f7a-821a-1aa2daeed6e0)

    class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        l, r = 0, len(s)-1

        while l <= r:
            s[l], s[r] = s[r], s[l]
            l += 1; r -= 1 
        return s

LC : 3110 Score of a String

![image](https://github.com/atishay2/daily_problems/assets/52835993/8c130ea3-53c7-49ad-b057-159899e782cc)

    class Solution:
        def scoreOfString(self, s: str) -> int:
        
            res = 0 
            for x in range(len(s)-1):
                res += abs(ord(s[x])-ord(s[x+1]))
            return res

LC : 1002 Find Common Characters

![image](https://github.com/atishay2/daily_problems/assets/52835993/7d2a7bc8-227a-4da6-90ec-a4488cb94909)


    class Solution:
        def commonChars(self, words: List[str]) -> List[str]:
            count = Counter(words[0])
            for word in words:
                cur_dic = Counter(word)
    
                for c in count:
                    count[c] = min(count[c], cur_dic[c])
    
            res = []
    
            for key in count:
    
                for x in range(count[key]):
                    res.append(key)
            return res

LC : 846 Hand of Straights

![image](https://github.com/atishay2/daily_problems/assets/52835993/dce179bb-cb44-4239-b16a-105e850c87a0)

    class Solution:
        def isNStraightHand(self, hand: List[int], groupSize: int) -> bool:
            if len(hand)%groupSize != 0:
                return False
            count = Counter(hand)
    
            heap = (list(count.keys()))
            heapq.heapify(heap)
            
            while heap:
                first = heap[0]
    
                for i in range(first, first+groupSize):
                    
                    if i not in heap:
                        return False
                    count[i] -= 1
                    if count[i] == 0 :
                        if i != heap[0]:
                            return False
                        
                        heapq.heappop(heap)
            return True

LC : 3174. Clear Digits

![image](https://github.com/atishay2/daily_problems/assets/52835993/c117c815-a98c-4f8a-a203-e43f5c13aafc)


    class Solution:
        def clearDigits(self, s: str) -> str:
            
            stack = []
            ans = list(s)
    
            for x in range(len(s)):
                if stack and ans[x].isdigit():
                    stack.pop()
                else:
                    stack.append(ans[x])
            return "".join(stack)

LC : 3175. Find The First Player to win K Games in a Row

![image](https://github.com/atishay2/daily_problems/assets/52835993/f1ac5907-769e-4451-aad1-918553c50dbf)

![image](https://github.com/atishay2/daily_problems/assets/52835993/3caa1e8d-d6a1-49d9-8b6e-bc2f77603257)

    class Solution:
        def findWinningPlayer(self, skills: List[int], k: int) -> int:
            freq = {skills[i] : [i, k] for i in range(len(skills))}
            if k >= len(skills)-1: return skills.index(max(skills))
            que = collections.deque(skills)
    
            flag = True
            first = que.popleft()
            while flag:
                sec = que.popleft()
                first = max(first,sec)
                sec = min(first,sec)
                que.append(sec)
                freq[first][1] -= 1
                if freq[first][1] == 0:
                    flag = False
            return freq[first][0]

LC : 974. Subarray Sums Divisible by K

![image](https://github.com/atishay2/daily_problems/assets/52835993/b1ea6bff-432d-4d33-b04e-016ecbbbb5ed)

    class Solution:
        def subarraysDivByK(self, nums: List[int], k: int) -> int:
            
            freq = {0 : [-1]}
    
            cum = 0 ; count = 0
    
            for i, num in enumerate(nums):
                cum += num 
                rem = cum % k 
                if rem in freq :
                    count += len(freq[rem])
                    freq[rem].append(i)
                else:
                    freq[rem] = [i]
            return count

LC : 3179. Find the N-th Value After K Seconds

![image](https://github.com/atishay2/daily_problems/assets/52835993/fa1bef4b-da2d-4067-88c9-44a0124140dc)

![image](https://github.com/atishay2/daily_problems/assets/52835993/174e3e38-a245-4efc-97c3-b57fbbd57c61)

![image](https://github.com/atishay2/daily_problems/assets/52835993/3e0b6720-18d0-47a4-99ba-5955df63f50d)

    class Solution:
        def valueAfterKSeconds(self, n: int, k: int) -> int:
            grid = [[0 for _ in range(n)] for _ in range(k+1)]
    
          
    
            for x in range(k+1):
                for y in range(n):
                    if x == 0 or y == 0:
                        
                        grid[x][y] = 1
                    if x > 0 and y > 0:
                        grid[x][y] = grid[x-1][y]+grid[x][y-1]
            return grid[-1][-1] % (10**9+7)

LC : 3178. Find the Child Who Has the Ball After K Seconds

![image](https://github.com/atishay2/daily_problems/assets/52835993/f52b1adb-e15c-4926-8489-dcbb9557faf1)
![image](https://github.com/atishay2/daily_problems/assets/52835993/d889ef66-a252-422c-83ad-de54d340910a)
![image](https://github.com/atishay2/daily_problems/assets/52835993/c3980067-7447-40f4-a18f-52ae9ebd90dc)

    
    class Solution:
        def numberOfChild(self, n: int, k: int) -> int:
            Qu = k//(n-1)
            rem = k%(n-1)
            par = Qu%2
    
            if par == 0:
                return rem
            else:
                return n-rem-1

LC : 1122. Relative Sort Array

![image](https://github.com/atishay2/daily_problems/assets/52835993/b919a271-6f8f-4251-89ac-8739503dd138)

    class Solution:
        def relativeSortArray(self, arr1: List[int], arr2: List[int]) -> List[int]:
            res = []
            freq = Counter(arr1)
    
            for x in arr2:
                if x in freq :
                    for y in range(freq[x]):
                        res.append(x)
                        freq[x] -= 1
            
            res2 = []
            for key, val in freq.items():
                if val != 0:
                    while val != 0:
                        res2.append(key)
                        val -= 1
            res2.sort()
            return res+res2

LC : 75. Sort Colors
![image](https://github.com/atishay2/daily_problems/assets/52835993/f612e86d-7603-4f23-930c-0aadd962dfb8)

DUTCH NATIONAL FLAG PROBLEM : throw the 0s at the left, increment the pointer, throw the 2s at the end of the array (right), decrement the pointer.

    class Solution:
        def sortColors(self, nums: List[int]) -> None:
            """
            Do not return anything, modify nums in-place instead.
            """
            left, right = 0, len(nums)-1
            i = 0 
    
            while i <= right:
                if nums[i] == 0:
                    nums[i], nums[left] = nums[left], nums[i]
                    left += 1
                
                elif nums[i] == 2:
                    nums[i], nums[right] = nums[right], nums[i]
                    right -= 1
                    i -= 1
                i += 1
            return nums


LC : 875. Koko Eating Bananas

![image](https://github.com/atishay2/daily_problems/assets/52835993/aa8ba695-3e45-4d4c-8048-f14e99c430c7)
    
    class Solution:
        def minEatingSpeed(self, piles: List[int], h: int) -> int:
            
            def speed_check(speed):
                hrs = 0 
                for x in piles:
                    hrs += ceil(x/speed)
                return hrs <= h
    
            low = 1 ; high = max(piles)
            while low < high:
                
                mid = (low+high)//2
                
                if speed_check(mid):
                    high = mid
                else:
                    low = mid+1
            return low

LC : 945. Minimum Increment to Make Array Unique

![image](https://github.com/atishay2/daily_problems/assets/52835993/1b6f122d-3af1-41d3-a4fa-9750e596dd8f)

    class Solution:
        def minIncrementForUnique(self, nums: List[int]) -> int:
            freq = Counter(nums)
            count = 0 
            nums.sort()
            
            for x in range(len(nums)+max(nums)):       
                if freq[x] > 1:
                    extra = freq[x]-1
                    freq[x+1] = freq.get(x+1, 0)+extra
                    count += extra
            return count

LC : 502. IPO

![image](https://github.com/atishay2/daily_problems/assets/52835993/795d1cfc-37c7-4a9f-a1f1-238743ecab82)
![image](https://github.com/atishay2/daily_problems/assets/52835993/c37f4b46-0640-497b-9de4-86e33c12596c)

    class Solution:
        def findMaximizedCapital(self, k: int, w: int, profits: List[int], capital: List[int]) -> int: 
            res = []
            for x in range(len(profits)):
                res.append((capital[x], profits[x]))
            
            res.sort()
            i = 0 
            maxCap = []
    
            while k > 0:        
                while i < len(res) and res[i][0] <= w :
                    heapq.heappush(maxCap, -res[i][1])
                    i += 1
                if not maxCap:
                    break
                w -= heapq.heappop(maxCap)
                k -= 1
            return w

LC : 3184. Count Pairs That Form a Complete Day I

![image](https://github.com/atishay2/daily_problems/assets/52835993/ac8ee00e-88e9-4047-a015-bec7c2f0f974)

![image](https://github.com/atishay2/daily_problems/assets/52835993/1299c85e-4fa2-46e4-b3f3-25757bc3eda5)

    class Solution:
        def countCompleteDayPairs(self, hours: List[int]) -> int:
            freq = {}
            count = 0 
            for x in range(len(hours)):
                cur = hours[x]%24
                if (-cur%24) in freq:
                    count += freq[-cur%24]
    
                freq[cur] = freq.get(cur, 0)+1
    
            return count 

lc : 3185 Count Pairs That Form a Complete Day II

![image](https://github.com/atishay2/daily_problems/assets/52835993/53327fcc-805f-4fe4-aaf4-a8932694c1a1)

    class Solution:
        def countCompleteDayPairs(self, hours: List[int]) -> int:
            freq = {}
            count = 0 
            for x in range(len(hours)):
                cur = hours[x]%24
                if (-cur%24) in freq:
                    count += freq[-cur%24]
    
                freq[cur] = freq.get(cur, 0)+1
    
            return count 

LC : 3186. Maximum Total Damage With Spell Casting                         (R E V I S E )

![image](https://github.com/atishay2/daily_problems/assets/52835993/e859330c-025b-4be6-ae31-c4811475abc6)

![image](https://github.com/atishay2/daily_problems/assets/52835993/c6c4e530-83bf-423a-92a7-bebffd9a9164)

    class Solution:
        def maximumTotalDamage(self, power: List[int]) -> int:
    
            count = Counter(power)
            dp = [0]*(3+len(count.keys()))
            arr = sorted(list(count.keys()))
            for x in range(len(arr)):
                
                dmg = count[arr[x]]*arr[x]
                if x > 1 and arr[x]-arr[x-2] <= 2:
                    dp[x+3] = max(dmg+dp[x], dp[x+2])
                elif x > 0 and arr[x]-arr[x-1] <= 2:
                    dp[x+3] = max(dmg+dp[x+1], dp[x+2])
                else:
                    dp[x+3] += dmg + dp[x+2]
                
            return dp[-1]
LC : 330. Patching Array (sum of 2 to the powers from 0 to n)

![image](https://github.com/atishay2/daily_problems/assets/52835993/7d125006-6690-4318-87b8-321a152fdca4)

    
    class Solution:
        def minPatches(self, nums: List[int], n: int) -> int:
            count, miss, i = 0,1,0
    
            while miss <= n :
                if i < len(nums) and nums[i] <= miss:
                    miss += nums[i]
                    i += 1
                else:
                    miss *= 2
                    count += 1
            return count
LC : 633. Sum of Square Numbers

![image](https://github.com/atishay2/daily_problems/assets/52835993/9c84f53c-0b79-48d2-b2a7-cd72b54af573)

OUTPUT LIMIT EXCEEDED (perform the prime factor decomposition of number, if one of the prime factor has (prime % 4 == 3) a remanided 3 when modular divided by 4 and its correcsponding exponent is ODD, the number cannot be sum of two squares otherwise it is (Number Theory sum of two squares theorem)).

    class Solution:
        def judgeSquareSum(self, c: int) -> bool:
            def is_prime(num):
                i = 2 ; res = set(); exp = 0
                cur = num
                while i <= cur and num  >= 1:
                    
                    if (num % i != 0):
                        if exp > 0 : 
                            res.add((i, exp))
                        exp = 0
                        if (num == 1) : break
                        i += 1
                        
                    else :
                        exp += 1
                        num = num//i
                    
                return res
            
            primes = list(is_prime(c))
            
            for pr, ex in primes:
                if (pr%4 == 3) and (ex%2 == 1):
                    return False
            return True

CORRECT SOLUTION 

    class Solution:
        def judgeSquareSum(self, c: int) -> bool:
            left = 0 ; right = int(math.sqrt(c))
                    while left <= right:
                        deco = (left**2) + (right**2)
                        if deco == c:
                            return True 
                        elif deco > c : right -= 1
                        else : left += 1
                    return False

LC : 1482. Minimum Number of Days to Make m Bouquets

![image](https://github.com/atishay2/daily_problems/assets/52835993/404decde-1c80-40e1-b8a0-0745014f826b)
![image](https://github.com/atishay2/daily_problems/assets/52835993/9f148909-83be-4116-be69-1cbd5a787201)

    
    class Solution:
        def minDays(self, bloomDay: List[int], m: int, k: int) -> int:
            if m*k > len(bloomDay): return -1
            start = 0 ; end = max(bloomDay)
    
            def is_possible(cur):
                count = 0 ; bouq = 0 
                for x in bloomDay:
                    if x <= cur: 
                        count += 1
                        if count == k:
                            bouq += 1
                            count = 0
                            if bouq == m : return True
                    else: count = 0
                return False
            while start < end :
                
                mid = (start+end)//2
                
                if is_possible(mid):
                    end = mid
                else : start = mid + 1
            return start
