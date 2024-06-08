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

