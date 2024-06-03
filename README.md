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

