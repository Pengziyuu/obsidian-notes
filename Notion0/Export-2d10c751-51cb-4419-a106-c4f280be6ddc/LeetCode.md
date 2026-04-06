# 題型

- **雙指標 (Two Pointers):**
    
    - 常用於陣列或鏈結串列中尋找特定元素或配對。
    
    - 例如：兩數之和、三數之和、反轉字串等。
    

- **排序 (Sorting):**
    
    - `sort(v.begin(), v.end())`：由小到大排序。
    
    - `sort(v.begin(), v.end(), greater<T>())` 或
        
        `sort(v.rbegin(), v.rend())`：由大到小排序。
        
    

- **貪婪演算法 (Greedy Algorithm):**
    
    - 每一步都選擇當前看起來最好的選擇，最終得到全域最佳解。
    
    - 例如：分發餅乾、無重疊區間、買賣股票的最佳時機等。
    

- **二分搜尋 (Binary Search):**
    
    - 適用於已排序的資料，能以 O(log n) 的時間複雜度快速尋找目標。
    
    - 例如：x 的平方根、尋找旋轉排序陣列中的最小值等。
    

- **分治法 (Divide and Conquer):**
    
    - 將大問題拆解成小問題，再將小問題的解合併成大問題的解。
    
    - 例如：Pow(x, n)、不同的二元搜尋樹等。
    

- **搜尋 (Search):**
    
    - **深度優先搜尋 (DFS):** 常用遞迴或堆疊實現，適合尋找所有解、路徑等。
    
    - **廣度優先搜尋 (BFS):** 常用佇列實現，適合尋找最短路徑、層序遍歷等。
    

- **動態規劃 (Dynamic Programming):**
    
    - 將問題拆解成子問題，並將子問題的解儲存起來，避免重複計算。
    
    - 例如：爬樓梯、打家劫舍、最長遞增子序列等。
    

---

# 解題流程

- 徹底理解題目
    
    - **理解約束條件 (Constraints)**：
        
        - `nums.length` 的範圍是多少？這會影響演算法的時間複雜度。
        
        - 如果 `n` 高達 $10^5$，$O(n^2)$ 的演算法通常會超時 (TLE - Time Limit Exceeded)，需要思考 $O(n log n)$ 或 $O(n)$ 的解法。
        
        - 陣列/字串中的元素值範圍是什麼？是正數、負數還是包含 0？這會影響是否需要使用 `long long` 來避免整數溢位 (integer overflow)。
        
        - 題目是否有特殊限制？例如「空間複雜度必須是 O(1)」。
        
    
    - **思考邊界情況 (Edge Cases)**：
        
        - 輸入為空（例如：空的陣列、空的字串）。
        
        - 輸入只有一個元素。
        
        - 輸入包含重複的元素。
        
        - 數值達到最大或最小值。
        
    

- 設計演算法與資料結構
    
    - **暴力解 (Brute Force)**：
        
        - 首先思考最直觀、最簡單的解法，即使它效率不高。
        
        - 有助於更好地理解問題，並確保沒有想錯方向。
        
    
    - **優化解法 (Optimization)**：
        
        - 分析暴力解的時間複雜度和空間複雜度。
        
        - 思考瓶頸在哪裡？是重複計算？還是查找效率太低？
        
        - 根據問題類型，聯想相關的資料結構和演算法：
            
            - **陣列/字串相關**：雙指標 (Two Pointers)、滑動視窗 (Sliding Window)、前綴和 (Prefix Sum)。
            
            - **查找/計數相關**：哈希表 (C++ 中的 `unordered_map`, `unordered_set`)，通常能將查找時間從 `O(n)` 降到 `O(1)`。
            
            - **排序相關**：如果題目不要求維持原順序，排序 (Sorting) 往往是優化的第一步。
            
            - **樹/圖相關**：深度優先搜尋 (DFS)、廣度優先搜尋 (BFS)、遞迴。
            
            - **最優化/路徑問題**：動態規劃 (Dynamic Programming)、貪婪演算法 (Greedy)。
            
            - **需要快速找最大/最小值**：堆 (Heap, C++ 中的 `priority_queue`)。
            
        
    

---

# **C++ 標準模板庫 (STL, Standard Template Library)**

STL 主要由以下四大核心元件組成。

- ==**容器 (Containers)**==：用來儲存和管理資料的物件。

- ==**演算法 (Algorithms)**==：處理資料的函式，例如排序、搜尋、轉換等。

- ==**迭代器 (Iterators)**==：提供統一的介面，用來存取容器中的元素，其角色類似於指向元素的「泛型指標」。

- ==**函式物件 (Functors)**==：行為類似函式的物件，可作為演算法的策略或判斷式。

---

==容器 (Containers)== - 「該用什麼來裝資料？」

- 序列容器 (Sequence Containers) - 在意元素的排列順序
    
    - `vector` - 動態陣列 (Dynamic Array)
        
        1. **宣告與初始化** (建立 DP 表、計數陣列)
        
        1. **尾部新增/移除** (動態建立結果、模擬堆疊)
        
        1. **隨機存取與修改** (O(1)，最常用的操作)
        
        1. **走訪** (遍歷讀取或更新)
        
        1. **取得大小 & 判斷是否為空** (迴圈邊界、終止條件)
        
        1. **排序 (核心)** (解決大量問題的前置步驟)
        
        1. **二分搜尋 (核心)** (在已排序中高效查找)
        
        1. **反轉** (字串、陣列反轉題目)
        
        1. **數值計算** (求總和、最大/最小值)
        
        1. **清空** (處理多筆測資時重置狀態)
        
        ```C++
        int main() {
            // 1. 宣告與初始化
            int n = 5;
            vector<int> dp(n + 1, 0); // 大小為 n+1，所有元素初始化為 0
            vector<int> v = {40, 10, 50, 20, 30}; // 從列表初始化
        
            // 2. 尾部新增/移除
            vector<int> result;
            result.push_back(100); // [100]
            result.push_back(200); // [100, 200]
            result.pop_back();     // [100]
        
            // 3. 隨機存取與修改 (O(1) 時間複雜度)
            cout << v[0] << endl; // 輸出 40
            v[1] = 15; // [40, 15, 50, 20, 30]
        
            // 4. 走訪 (遍歷)
            // a) 索引走訪 (需要用到索引時)
            for (int i = 0; i < v.size(); ++i) {
                // ...
            }
            // b) Range-based for (更簡潔，不需要索引時)
            for (int& val : v) {
                // ...
            }
        
            // 5. 取得大小 & 判斷是否為空
            cout << v.size() << endl;
            if (!result.empty()) {
                // ...
            }
        
            // 6. 排序
            // 預設升序 15 20 30 40 50
            sort(v.begin(), v.end()); 
        
            // 降序排序 (使用 lambda) 50 40 30 20 15
            sort(v.begin(), v.end(), [](int a, int b) {
                return a > b;
            });
        
            // 7. 二分搜尋 - 必須在已排序的 vector 上使用
            // 重新排序回升序以利查找
            sort(v.begin(), v.end()); // v: [15, 20, 30, 40, 50]
            // 查找 >= 35 的第一個元素
            auto it = lower_bound(v.begin(), v.end(), 35);
            if (it != v.end()) {
                cout << *it << endl; // 輸出 40
                cout  << distance(v.begin(), it) << endl; // 輸出 3
            }
            // 檢查 30 是否存在
            bool found = binary_search(v.begin(), v.end(), 30);
            cout << (found ? "是" : "否") << endl;
        
            // 8. 反轉 50 40 30 20 15
            reverse(v.begin(), v.end());
        
            // 9. 數值計算
            int sum = accumulate(v.begin(), v.end(), 0);
            cout << sum << endl; // 輸出 155
        
            // 找最大/最小值
            // * 注意： max_element 回傳的是 iterator，需要用 * 取值
            int max_val = *max_element(v.begin(), v.end());
            int min_val = *min_element(v.begin(), v.end());
        
            // 10. 清空
            v.clear();
            cout << v.size() << endl; // 輸出 0
        
            return 0;
        }
        ```
        
    
    - `deque` - 雙向佇列 (Double-Ended Queue)
        
        - 何時使用 `deque`？以下場景時，`deque` 是比 `vector` 更好的選擇：
            
            - **實現佇列 (Queue)**: 在廣度優先搜尋 (BFS) 中，你需要一個先進先出 (FIFO) 的結構。`deque` 的 `push_back()` 和 `pop_front()` 都是 O(1)，完美符合需求。
            
            - **滑動窗口問題 (Sliding Window)**: 像是 "滑動窗口最大值" 這類題目，需要維護一個窗口，並在窗口移動時，高效地從兩端新增或移除元素。這時 `deque` 是實現「單調佇列 (Monotonic Queue)」的標準工具。
            
            - **需要在頭部頻繁插入**: 如果演算法需要在容器的頭部大量插入元素，`deque` 的 O(1) `push_front()` 遠勝於 `vector` 的 O(N) `insert()`。
            
        
        1. **宣告與初始化** (建立佇列或雙端佇列)
        
        1. **雙向新增/移除 (核心)** (高效實現佇列、單調佇列)
        
        1. **隨機存取與修改** (O(1)，但比 vector 稍慢)
        
        1. **走訪** (遍歷讀取或更新)
        
        1. **取得大小 & 判斷是否為空** (迴圈邊界、終止條件)
        
        1. **排序** (可排序，但不常用)
        
        1. **反轉** (可反轉)
        
        1. **清空** (處理多筆測資時重置狀態)
        
        ```C++
        int main() {
            // 1. 宣告與初始化
            deque<int> dq1; // 空 deque
            deque<int> dq = {40, 10, 50, 20, 30};
        
            // 2. 雙向新增/移除
            dq.push_back(100);    // [40, 10, 50, 20, 30, 100]
            dq.push_front(99);    // [99, 40, 10, 50, 20, 30, 100]
        
            dq.pop_back();        // [99, 40, 10, 50, 20, 30]
            dq.pop_front();       // [40, 10, 50, 20, 30]
        
            // 3. 隨機存取與修改 (通常是 O(1))
            //雖然是 O(1)，但其常數時間比 vector 大，因為內部結構更複雜
            cout << dq[0] << endl; // 輸出 40
            dq[1] = 15; // [40, 15, 50, 20, 30]
        
            // 4. 走訪 (遍歷)
            // a) 索引走訪
            for (int i = 0; i < dq.size(); ++i) {
                // ...
            }
            // b) Range-based for
            for (int& val : dq) {
                // ...
            }
        
            // 5. 取得大小 & 判斷是否為空
            cout << dq.size() << endl;
            if (!dq.empty()) {
                // ...
            }
        
            // 6. 排序
            // 但若排序是主要需求，通常會優先選擇 vector
            sort(dq.begin(), dq.end()); // 排序後: 15 20 30 40 50
        
            // 7. 反轉
            reverse(dq.begin(), dq.end()); // 反轉後: 50 40 30 20 15
        
            // 9. 數值計算
            int sum = accumulate(dq.begin(), dq.end(), 0);
            cout << sum << endl; // 輸出 155
        
            int max_val = *max_element(dq.begin(), dq.end());
            int min_val = *min_element(dq.begin(), dq.end());
        
            // 10. 清空
            dq.clear();
            cout << dq.size() << endl; // 輸出 0
        
            return 0;
        }
        ```
        
    
    - `list` - 雙向鏈結串列 (Double Link List)
        
        - 何時使用 `list`？以下特定場景，`list` 是絕佳選擇：
            
            - **LRU 快取 (LRU Cache)**: LeetCode 經典題目。`list` 用來維護資料的存取順序，當一個資料被存取，可以透過 `splice` 操作在 O(1) 時間內將其移動到頭部表示「最近使用」。搭配 `unordered_map` 儲存鍵與 `list` 迭代器的映射，即可實現一個高效的 LRU 快取。
            
            - **需要頻繁在中間插入/刪除**: 如果題目情境真的需要大量在序列中間進行新增或移除，`list` 的 O(1) 效能遠勝 `vector` 和 `deque` 的 O(N)。例如模擬一個文字編輯器的游標移動和文字輸入/刪除。
            
            - **要求迭代器穩定性**: 在 `list` 中，除非刪除元素本身，否則指向其他元素的迭代器永遠不會失效。在 `vector`/`deque` 中，插入/刪除操作可能會導致所有迭代器失效。
            
        
        1. **宣告與初始化**
        
        1. **雙向新增/移除** (高效實現佇列、堆疊)
        
        1. **任意位置插入/刪除 (核心)** (使用 iterator 的 O(1) 操作)
        
        1. **元素轉移 (splice)** (O(1) 合併或移動元素，LRU 快取常用)
        
        1. **走訪 (遍歷)** (只能用 iterator 或 range-based for)
        
        1. **取得大小 & 判斷是否為空**
        
        1. **排序** (使用成員函式 `.sort()`)
        
        1. **清空**
        
        ```C++
        int main() {
            // 1. 宣告與初始化
            list<int> li = {40, 10, 50, 20, 30};
        
            // 2. 雙向新增/移除 (皆為 O(1))
            li.push_back(100);    // {40, 10, 50, 20, 30, 100}
            li.push_front(99);    // {99, 40, 10, 50, 20, 30, 100}
        
            li.pop_back();        // {99, 40, 10, 50, 20, 30}
            li.pop_front();       // {40, 10, 50, 20, 30}
        
            // 3. 任意位置插入/刪除 (核心優勢，O(1))
            // 首先需要一個指向目標位置的 iterator
            auto it = li.begin();
            advance(it, 2); // it 指向第 3 個元素 (50)
        
            li.insert(it, 999); // 在 it 前插入 -> {40, 10, 999, 50, 20, 30}
            
            it = li.erase(it);  // 刪除 it 指向的元素 (50)，it 會自動指向下一個元素 (20)
                                // li -> {40, 10, 999, 20, 30}
            
            // 4. 元素轉移 (splice) (O(1))
            // 可將另一個 list 的元素「剪下貼上」過來，效率極高
            list<int> other_li = {1, 2, 3};
            // 將 other_li 的所有元素移動到 li 的開頭
            li.splice(li.begin(), other_li); 
            // li -> {1, 2, 3, 40, 10, 999, 20, 30}
            // other_li -> {} (變空了)
        
            // 5. 走訪 (遍歷)
            // a) Range-based for (推薦)
            for (int& val : li) {
                // ...
            }
            // b) Iterator
            for (auto iter = li.begin(); iter != li.end(); ++iter) {
                // ...
            }
            // 注意：list 不支援隨機存取，所以不能用索引走訪
            // for (int i = 0; i < li.size(); ++i) { /* 編譯錯誤 */ }
        
            // 6. 取得大小 & 判斷是否為空
            cout << li.size() << endl;
            if (!li.empty()) {
                // ...
            }
        
            // 7. 排序 (使用成員函式 .sort())
            // sort(li.begin(), li.end()); // 編譯錯誤，因為 sort 需要隨機存取
            li.sort(); // 升序排序
            li.sort([](int a, int b) { return a > b; }); // 降序排序
        
            // 8. 清空
            li.clear();
            cout << li.size() << endl; // 輸出 0
        
            return 0;
        }
        ```
        
    

- 無序關聯容器 (Unordered Associative Containers) - 元素無序，最快的查找速度
    
    - `unordered_set` - 唯一鍵的快速集合，基於雜湊表的容器
        
        - 何時使用 `unordered_set`？
            
            - **黃金法則：當只需要快速「判斷一個元素是否存在（是否見過）」，而完全不關心元素的順序時。**
            
            - **高效去重與存在性檢查**: 幾乎所有需要「判斷重複」、「紀錄訪問過的狀態以避免死循環」的題目。
            
            - **集合運算**: 計算兩個陣列的交集 (Intersection) 或聯集 (Union)。可以先把一個陣列的元素全放入 `unordered_set`，然後遍歷第二個陣列，在 O(1) 的時間內檢查每個元素是否存在於 set 中。
            
        
        1. **宣告與初始化**
        
        1. **新增元素** (平均 O(1)，自動去重)
        
        1. **刪除元素** (平均 O(1))
        
        1. **查找元素 (核心)** (平均 O(1)，最快的存在性檢查)
        
        1. **走訪** (遍歷順序不固定)
        
        1. **取得大小 & 判斷是否為空**
        
        1. **清空**
        
        ```C++
        int main() {
            // 1. 宣告與初始化
            // 從 vector 初始化 (會自動移除重複項，但順序不保證)
            vector<int> nums = {40, 10, 50, 20, 30, 10};
            unordered_set<int> us(nums.begin(), nums.end()); 
            // 內容可能是 {10, 20, 50, 40, 30} 或其他任意順序
        
            // 2. 新增元素 (insert) - 平均 O(1)
            // 如果元素已存在則不會插入
            us.insert(60); 
            us.insert(10); // 插入失敗，因為 10 已存在
        
            // 3. 刪除元素 (erase) - 平均 O(1)
            us.erase(40); 
            
            // 4. 查找元素 (核心，平均 O(1)，速度極快)
            // a) 使用 count()，回傳 0 或 1，語法最簡單
            if (us.count(30)) {
                // 存在
            }
            
            // b) 使用 find()，回傳 iterator。若找不到則回傳 us.end()
            auto it = us.find(20);
            if (it != us.end()) {
                // 存在
            }
        
            // 5. 走訪 (遍歷順序不固定！)
            // 遍歷的順序是雜亂的，且每次執行、不同編譯器下可能都不同
            cout << "unordered_set 的內容: ";
            for (int val : us) {
                cout << val << " ";
            }
        
            // 6. 取得大小 & 判斷是否為空
            cout << "unordered_set 的大小: " << us.size() << endl;
            if (!us.empty()) {
                // ...
            }
            
            // 7. 清空
            us.clear();
            cout << "清空後的大小: " << us.size() << endl; // 輸出 0
        
            return 0;
        }
        ```
        
    
    - `unordered_map` - 唯一鍵的快速鍵值對，基於雜湊表的鍵值對容器
        
        - 何時使用 `unordered_map`？**只要需要「鍵值對映射」或「頻率計數」。**
            
            - **最高效的頻率計數**: 任何需要統計元素出現次數的。
            
            - **建立快速查找的映射**: 將數值映射到其索引，以便在 O(1) 時間內查找目標配對。
            
            - **DP 記憶化 (Memoization)**: 在動態規劃中，`unordered_map` 是實現記憶化搜尋最高效的工具之一，用來儲存已計算過的子問題狀態及其結果，`unordered_map<State, Result>`。
            
        
        1. **宣告與初始化**
        
        1. **新增 & 修改元素 (核心)** (平均 O(1)，`[]` 運算子最常用)
        
        1. **查找元素 (核心)** (平均 O(1)，最快的 Key-Value 查找)
        
        1. **刪除元素** (平均 O(1))
        
        1. **走訪** (遍歷順序不固定)
        
        1. **取得大小 & 判斷是否為空**
        
        1. **清空**
        
        ```C++
        int main() {
            // 1. 宣告與初始化
            unordered_map<string, int> um;
        
            // 2. 新增 & 修改元素 (核心，平均 O(1))
            // a) 使用 [] 運算子
            um["two_sum"] = 1;      // 新增 {"two_sum", 1}
            um["dp"] = 5;           // 新增 {"dp", 5}
            um["two_sum"] = 2;      // 修改 {"two_sum", 2}
        
            // 3. 查找元素 (核心，平均 O(1))
            // a) 使用 count()，回傳 0 或 1，判斷 key 是否存在
            if (um.count("dp")) {
        				// ...
            }
            
            // b) 使用 find()，回傳 iterator。若找不到則回傳 um.end()
            auto it = um.find("two_sum");
            if (it != um.end()) {
                // it->first 是 key, it->second 是 value
            }
        
            // 4. 刪除元素 - 平均 O(1)
            um.erase("dp");
        
            // 5. 走訪 (遍歷順序不固定！)
            // 遍歷的順序是雜亂的，且每次執行、不同編譯器下可能都不同
            for (const auto& [key, value] : um) {
                cout << key << value << endl;
            }
            
            // 6. 取得大小 & 判斷是否為空
            cout << um.size() << endl;
            if (!um.empty()) {
                // ...
            }
            
            // 7. 清空
            um.clear();
            cout << um.size() << endl; // 輸出 0
        
            return 0;
        }
        ```
        
    
    - `unordered_multiset`
        
        - 何時使用 `unordered_multiset`？**一個高速的「元素袋子 (Bag)」**，只關心袋子裡有**哪些東西**以及**各有幾個**，而不關心它們的排列順序。
            
            - **判斷字母異位詞 (Anagrams)**: 這是 `unordered_multiset` 的經典應用。要判斷兩個字串 `s` 和 `t` 是否為 anagram，可以將 `s` 的所有字元放入 `unordered_multiset`，然後遍歷 `t` 的所有字元，逐一從 set 中刪除。如果最後 set 為空，則兩者是 anagram。
            
            - **模擬「資源池」**: 當你需要檢查是否能用手頭的一組資源（可重複）來構成某個目標時。例如 "Ransom Note" 問題，可以用 `unordered_multiset` 儲存雜誌中的所有字元，然後遍歷贖金信中的字元，看是否能從 set 中逐一找到並移除。
            
            - **需要計數但** `**map**` **過於繁瑣的場景**: 有時候你只需要知道元素的個數，而不需要對個數本身做複雜操作。`unordered_multiset` 的 `insert`/`erase`/`count` 介面比 `unordered_map<T, int>` 的 `map[key]++` / `map[key]--` 在概念上更直接。
            
        
        ```C++
        // 同 unordered_set 
        ```
        
    
    - `unordered_multimap`
        
        - 何時使用 `unordered_multimap`？
            
            - **需要最高效能的「一對多」映射**: 當需要一個「一對多」的對應關係，且 Key 不需要排序，同時又追求極致的插入和刪除效能時，`unordered_multimap` 在理論上是最佳選擇。例如，用來表示圖的鄰接串列 `unordered_multimap<int, int> adj`，插入一條邊的操作非常快。
            
        
        ```C++
        // 同unordered_map 
        ```
        
    

- 有序關聯容器 (Associative Containers) - 元素自帶排序，用於快速查找
    
    - `set` - 唯一鍵的集合，基於紅黑樹的容器
        
        - 何時使用 `set`？
            
            - **去重並排序**: 這是最直接的用途。當題目需要處理不重複的元素，且這些元素需要保持有序時。
            
            - **快速判斷元素是否存在**: `set` 的 O(logN) 查找速度非常快。在需要頻繁檢查一個元素是否「已經見過」的場景中很有用（例如：尋找數組中的重複項、判斷鏈結串列是否有環）。
            
            - **需要動態維護有序集合**: 當你需要一個資料集合，它在演算法執行過程中會不斷有元素的增刪，但你又需要隨時能從中找到最大/最小值，或者找到某個元素的「下一個更大/小的元素」時，`set` 就非常強大。例如，在滑動窗口問題中維護窗口內的有序元素。
            
        
        1. **宣告與初始化** (預設升序，可自訂排序)
        
        1. **新增元素** (O(logN)，自動排序去重)
        
        1. **刪除元素** (O(logN))
        
        1. **查找元素 (核心)** (O(logN)，高效判斷元素是否存在)
        
        1. **邊界查找 (核心)** (`lower_bound`/`upper_bound`，查找上下界)
        
        1. **走訪** (遍歷的結果是排序的)
        
        1. **取得大小 & 判斷是否為空**
        
        1. **清空**
        
        ```C++
        int main() {
            // 1. 宣告與初始化
            // a) 預設升序 set
            set<int> s;
            // b) 從 vector 初始化 (會自動排序並移除重複項)
            vector<int> nums = {40, 10, 50, 20, 30, 10};
            set<int> s_from_vec(nums.begin(), nums.end()); // 內容: {10, 20, 30, 40, 50}
        
            // c) 降序 set
            set<int, greater<int>> descending_s;
        
            // 2. 新增元素 (insert) - O(log N)
            // 會自動維持排序，且若元素已存在則不會插入
            s.insert(40); // {40}
            s.insert(10); // {10, 40}
            s.insert(50); // {10, 40, 50}
            s.insert(10); // 插入失敗，s 內容不變: {10, 40, 50}
        
            // 3. 刪除元素 (erase) - O(log N)
            s.erase(40); // 刪除值為 40 的元素 -> {10, 50}
            // 也可以用 iterator 刪除
            auto it_to_erase = s.find(50);
            if (it_to_erase != s.end()) {
                s.erase(it_to_erase); // -> {10}
            }
            
            // 4. 查找元素 (核心) - O(log N)
            // a) 使用 count()，回傳 0 或 1，語法最簡單
            if (s_from_vec.count(30)) {
                // 存在
            }
            // b) 使用 find()，回傳 iterator。若找不到則回傳 s.end()
            auto it = s_from_vec.find(20);
            if (it != s_from_vec.end()) {
                cout << *it << endl; // 輸出 20
            }
        
            // 5. 邊界查找 (核心) - O(log N)
            // s_from_vec: {10, 20, 30, 40, 50}
            // lower_bound: 找第一個 "大於等於" 目標值的 iterator
            auto lb = s_from_vec.lower_bound(25); // *lb is 30
            // upper_bound: 找第一個 "嚴格大於" 目標值的 iterator
            auto ub = s_from_vec.upper_bound(30); // *ub is 40
        
            // 6. 走訪 (遍歷結果永遠是排序的)
            for (int val : s_from_vec) {
                // 輸出: 10 20 30 40 50
            }
            // 注意：set 不支援隨機存取，不能用 s[i]
        
            // 7. 取得大小 & 判斷是否為空
            cout << s_from_vec.size() << endl;
            if (!s.empty()) {
                // ...
            }
            
            // 8. 清空
            s.clear();
            cout << s.size() << endl; // 輸出 0
        
            return 0;
        }
        ```
        
    
    - `map` - 唯一鍵的鍵值，基於紅黑樹的鍵值對容器
        
        - 何時使用 `map`？需要「映射關係」的場景。
            
            - **頻率計數**: 這是 `map` 最經典的用途，用來統計陣列、字串中每個元素出現的次數。
            
            - **建立映射關係**: 需要將一種資料對應到另一種時。
            
            - **DP 狀態壓縮/記憶化**: 在動態規劃中，如果狀態不是一個簡單的整數（可能是一個字串、`pair` 或 `vector`），無法用陣列當作 `dp` 表，這時就可以用 `map` 來儲存已計算過的狀態結果，即 `map<State, Result>`。
            
            - **需要根據 Key 排序的場景**: 如果問題需要在維護鍵值對的同時，還要能快速找到「大於/小於某個 key」的元素，`map` 的 `lower_bound` 和有序性就派上用場了。
            
        
        1. **宣告與初始化** (依 Key 排序)
        
        1. **新增 & 修改元素 (核心)** (使用 `[]` 或 `insert`)
        
        1. **查找元素 (核心)** (O(logN)，判斷 Key 是否存在)
        
        1. **刪除元素** (O(logN))
        
        1. **走訪** (遍歷結果依 Key 排序)
        
        1. **邊界查找** (`lower_bound`/`upper_bound`，依 Key 查找)
        
        1. **取得大小 & 判斷是否為空**
        
        1. **清空**
        
        ```C++
        int main() {
            // 1. 宣告與初始化
            // Key 是 int, Value 是 string
            map<int, string> m;
        
            // 2. 新增 & 修改元素 (核心)
            // a) 使用 [] 運算子 (最常用)
            // 如果 key 不存在，會自動建立並賦值；如果存在，則會覆蓋
            m[101] = "Alice"; // 新增 {101, "Alice"}
            m[102] = "Bob";   // 新增 {102, "Bob"}
            m[101] = "Anna";  // 修改 {101, "Anna"}
        
            // b) 使用 insert()
            // 如果 key 已存在，insert 不會做任何事
            m.insert({103, "Charlie"}); // 新增 {103, "Charlie"}
            m.insert({102, "Bill"});    // 新增失敗，因為 key 102 已存在
        
            // 3. 查找元素 (核心) - O(log N)
            // a) 使用 count()，回傳 0 或 1，判斷 key 是否存在的最佳方式
            if (m.count(102)) {
                // key 102 存在
            }
            // b) 使用 find()，回傳 iterator。若找不到則回傳 m.end()
            auto it = m.find(101);
            if (it != m.end()) {
                // it->first 是 key, it->second 是 value
            }
        
            // 4. 刪除元素 - O(log N)
            m.erase(103); // 刪除 key 為 103 的元素
        
            // 5. 走訪 (遍歷結果永遠根據 Key 排序)
            // C++17 結構化綁定語法 (推薦)
            for (const auto& [key, value] : m) {
                cout << key << value << endl;
            }
        
            // 6. 邊界查找 (依 Key 查找) - O(log N)
            // m: {101: "Anna", 102: "Bob"}
            // lower_bound: 找第一個 Key "大於等於" 目標值的 iterator
            auto lb = m.lower_bound(102); // 指向 {102, "Bob"}
            cout << lb->first << endl;
            
            // 7. 取得大小 & 判斷是否為空
            cout << m.size() << endl;
            if (!m.empty()) {
                // ...
            }
            
            // 8. 清空
            m.clear();
            cout << m.size() << endl; // 輸出 0
        
            return 0;
        }
        ```
        
    
    - `multiset` - 允許多鍵的集合
        
        - 何時使用 `multiset`？
            
            - **需要動態維護一個「可重複的有序集合」**: 這是 `multiset` 的核心用途。當需要一個資料集合，它允許重複，又需要頻繁地增刪元素，同時還要能隨時快速地找到最大/最小值或中位數時，`multiset` 就非常合適。
            
            - **滑動窗口中位數 / 第 K 大元素**: 這是 `multiset` 最經典的應用場景。例如，維護一個固定大小為 K 的 `multiset` 來代表當前的滑動窗口。由於 `multiset` 自動排序，窗口內的最大/最小值 (`ms.rbegin()` / `ms.begin()`) 唾手可得。對於中位數問題，可以透過 `next` 配合 `begin()` 和 `size()` 在 O(logK) 時間內找到中位數。
            
            - **替代優先佇列 (Priority Queue)**: `priority_queue` 只能存取頂端元素，而 `multiset` 不但能存取頂端 (最大/最小值)，還能刪除任意一個元素，這在某些複雜問題中提供了更高的靈活性。
            
        
        ```C++
        // 同 set
        ```
        
    
    - `multimap` - 允許多鍵的鍵值對
        
        - 何時使用 `multimap`？處理「一對多」的有序映射關係問題。
            
            1. **分組問題**: 當你需要根據某個屬性（Key）對一組物件（Value）進行分組，且分組後還要保持屬性的有序性時。例如，將員工按薪水（Key）分組，一個薪水等級可能對應多個員工（Value）。
            
            1. **需要排序的鄰接串列**: 在圖論中，如果需要一個鄰接串列來表示圖，同時希望每個節點的所有鄰居節點都是有序的，可以使用 `multimap<int, int>`。
            
            1. **事件排程**: 當多個事件可能發生在同一個時間點時，可以使用 `multimap<timestamp, event_details>`。`multimap` 會自動根據時間戳排序，並能儲存同一時間點的多個事件。
            
        
        ```C++
        // 同 map
        ```
        
    

- 容器配接器 (Container Adaptors) - 提供特定介面的容器
    
    - `stack` - 堆疊
        
        - 何時使用 `stack`？
            
            - **括號匹配**: 遇到左括號就 `push`，遇到右括號就檢查 `top()` 是否匹配，匹配則 `pop`。
            
            - **單調棧 (Monotonic Stack)**: 一種高階技巧，用於解決「尋找下一個更大/更小的元素」這類問題。透過維護一個單調遞增或遞減的堆疊，可以高效地找到每個元素右邊（或左邊）第一個比它大/小的元素。
            
            - **模擬遞迴 / DFS (深度優先搜尋)**: 遞迴的本質就是一個函式呼叫堆疊。所有遞迴實現的 DFS 都可以改用一個顯式的 `stack` 來達成迭代寫法，避免遞迴深度過大導致堆疊溢位。
            
            - **表達式求值 / 路徑簡化**: 在處理逆波蘭表達式 (Reverse Polish Notation) 或簡化檔案路徑 (例如 "/a/./b/../c") 時，`stack` 可以很自然地處理運算子和運算元的後進先出關係，或路徑的進入與返回。
            
        
        1. **宣告與初始化**
        
        1. **壓入元素 (**`**push**`**)** (將元素放到堆疊頂部)
        
        1. **訪問頂部元素 (**`**top**`**)** (取得頂部元素，但不移除)
        
        1. **彈出元素 (**`**pop**`**)** (移除頂部元素，**注意：不回傳值**)
        
        1. **判斷是否為空 (**`**empty**`**)** (堆疊操作的常用迴圈條件)
        
        1. **取得大小 (**`**size**`**)** (取得堆疊中的元素數量)
        
        ```C++
        int main() {
            // 1. 宣告與初始化
            // 底層預設使用 deque<int>
            stack<int> s;
        
            // 也可以指定底層容器，例如 vector
            // stack<int, vector<int>> s_with_vector;
        
            // 2. 壓入元素 (push) - O(1)
            s.push(10); // stack: [10]
            s.push(20); // stack: [10, 20]
            s.push(30); // stack: [10, 20, 30] <- 30 在頂部
        
            // 3. 訪問頂部元素 (top) - O(1)
            cout << s.top() << endl; // 輸出 30
        
            // 4. 彈出元素 (pop) - O(1)
            // pop() 是一個 void 函式，只移除元素，不回傳
            s.pop(); // stack: [10, 20]
        
            // 5. 判斷是否為空 (empty)
            if (!s.empty()) {
        				// 非空
            }
        
            // 6. 取得大小 (size)
            cout << s.size() << endl; // 輸出 2
        
            return 0;
        }
        ```
        
    
    - `queue` - 佇列
        
        - 何時使用 `queue`？在圖論和樹的相關問題中。
            
            - **廣度優先搜尋 (BFS - Breadth-First Search)**: 這是 `queue` **最核心、最重要**的應用。BFS 演算法的本質就是透過一個 `queue` 來逐層探索圖或樹的節點，常用於尋找無權圖中的最短路徑。
            
            - **樹的層序遍歷 (Level-Order Traversal)**: 這是 BFS 在樹上的具體應用。`queue` 可以完美地儲存每一層的節點，處理完當前層後，下一層的所有節點也剛好被依序放入了 `queue` 中。`q.size()` 在此場景中常用來確定每一層的節點數量。
            
            - **模擬佇列系統**: 任何需要模擬「先進先出」流程的題目，例如作業系統中的任務排程、現實生活中的排隊買票等。
            
        
        1. **宣告與初始化**
        
        1. **放入元素至尾端 (**`**push**`**)** (Enqueue)
        
        1. **訪問頭部元素 (**`**front**`**)** (取得隊伍最前端的元素)
        
        1. **彈出頭部元素 (**`**pop**`**)** (讓隊伍最前端的元素出列，**不回傳值**)
        
        1. **訪問尾端元素 (**`**back**`**)** (取得隊伍最後一個元素)
        
        1. **判斷是否為空 (**`**empty**`**)** (BFS 演算法的核心迴圈條件)
        
        1. **取得大小 (**`**size**`**)** (常用於樹的層序遍歷)
        
        ```C++
        int main() {
            // 1. 宣告與初始化
            // 底層預設使用 deque<int>
            queue<int> q;
        
            // 2. 放入元素至尾端 (push) - O(1)
            q.push(10); // queue: [10]
            q.push(20); // queue: [10, 20]
            q.push(30); // queue: [10, 20, 30]
        
            // 3. 訪問頭部元素 (front) - O(1)
            cout << q.front() << endl; // 輸出 10
        
            // 4. 訪問尾端元素 (back) - O(1)
            cout << q.back() << endl; // 輸出 30
        
            // 5. 彈出頭部元素 (pop) - O(1)
            // pop() 是一個 void 函式，只移除元素，不回傳
            q.pop(); // queue: [20, 30]
            cout << q.front() << endl; // 輸出 20
        
            // 6. 判斷是否為空 (empty)
            if (!q.empty()) {
        				// 非空
            }
        
            // 7. 取得大小 (size)
            // 在層序遍歷中，用來確定目前層級有多少個節點
            cout << q.size() << endl; // 輸出 2
            
            return 0;
        }
        ```
        
    
    - `priority_queue` - 優先佇列
        
        - 何時使用 `priority_queue`？解決「動態取得極值」問題。當問題符合「在一個不斷變化的集合中，總是需要找到並處理最大（或最小）的那個元素」時。
            
            - **Top K 問題**: 「在 N 個元素中找到第 K 大的元素」。可以維護一個大小為 K 的**最小堆**：遍歷所有元素，如果堆的大小小於 K 就直接放入；否則，如果當前元素比堆頂（目前 K 個中的最小值）還大，就彈出堆頂，放入當前元素。遍歷結束後，堆頂就是第 K 大的元素。
            
            - **合併 K 個排序好的列表 (Merge K Sorted Lists)**: 用一個最小堆來存放 K 個列表的頭部元素，每次從堆中取出最小的那個，然後將該元素所在列表的下一個元素放入堆中，重複此過程直到堆為空。
            
            - **Dijkstra 演算法**: 在尋找圖中加權最短路徑時，`priority_queue` (最小堆) 被用來儲存 `{距離, 節點}`，並總是從中選出目前已知距離最短的節點進行下一步的探索。
            
            - **資料流中位數 (Median from Data Stream)**: 使用一個最大堆（儲存較小的一半數字）和一個最小堆（儲存較大的一半數字），並保持兩者大小平衡，即可在 O(logN) 時間內新增元素並在 O(1) 時間內取得中位數。
            
        
        1. **宣告與初始化 (核心)** (最大堆 vs. 最小堆)
        
        1. **壓入元素 (**`**push**`**)** (O(logN))
        
        1. **訪問頂部元素 (**`**top**`**)** (O(1))
        
        1. **彈出頂部元素 (**`**pop**`**)** (O(logN))
        
        1. **判斷是否為空 (**`**empty**`**)**
        
        1. **取得大小 (**`**size**`**)**
        
        ```C++
        int main() {
            // 1. 宣告與初始化 (核心)
            
            // a) 最大堆 (Max-Heap) - 預設行為
            // 頂部永遠是最大的元素
            priority_queue<int> max_pq;
            max_pq.push(10);
            max_pq.push(50);
            max_pq.push(20);
            cout << max_pq.top() << endl; // 輸出 50
        
            // b) 最小堆 (Min-Heap)
            // 語法：priority_queue<Type, Container, Comparator>
            // 頂部永遠是最小的元素
            priority_queue<int, vector<int>, greater<int>> min_pq;
            min_pq.push(10);
            min_pq.push(50);
            min_pq.push(20);
            cout << min_pq.top() << endl; // 輸出 10
        
            // c) 儲存 pair (常用於 Dijkstra 等演算法)
            // 預設會先比較 pair.first，再比較 pair.second
            priority_queue<pair<int, char>> pair_pq;
            pair_pq.push({10, 'A'});
            pair_pq.push({20, 'B'});
            pair_pq.push({10, 'C'}); // {10, 'C'} 比 {10, 'A'} 大
            cout << pair_pq.top().first << ", " << pair_pq.top().second << endl; // 輸出 {20, B}
        
            // 2. 壓入元素 (push) - O(log N)
            // 已在上方展示
        
            // 3. 訪問頂部元素 (top) - O(1)
            // 已在上方展示
        
            // 4. 彈出頂部元素 (pop) - O(log N)
            max_pq.pop(); // 移除 50
            cout << max_pq.top() << endl; // 輸出 20
            
            // 5. 判斷是否為空 (empty)
            if (!max_pq.empty()) {
        			 // 非空
            }
        
            // 6. 取得大小 (size)
            cout << max_pq.size() << endl; // 輸出 2
        
            return 0;
        }
        ```
        
    

---

==演算法 (Algorithms)== - 「想對這批資料做什麼處理？」

- 排序與相關操作 (Sorting and related operations)
    
    - `sort`: 對序列進行排序 (預設為升序)。
        
        ```C++
        int main() {
            vector<int> v = {5, 2, 8, 1, 9, 4};
            
            sort(v.begin(), v.end()); // 升序排序
        
            cout << "升序排序後: ";
            for (int n : v) {
                cout << n << " ";
            }
            cout << endl;
        
            // 降序排序
            sort(v.begin(), v.end(), greater<int>());
            
            cout << "降序排序後: ";
            for (int n : v) {
                cout << n << " ";
            }
            cout << endl;
            return 0;
        }
        ```
        
    
    - `lower_bound`: 在**已排序**的序列中，找到第一個**不小於 (>=)** 給定值的元素。
        
        - 回傳一個指向該元素的迭代器。
        
        ```C++
        int main() {
            vector<int> v = {10, 20, 30, 30, 30, 40, 50};
            
            // 尋找第一個不小於 30 的元素
            auto it = lower_bound(v.begin(), v.end(), 30);
            cout << "第一個不小於 30 的元素在索引: " << distance(v.begin(), it) << endl; // 輸出: 2
        
            // 尋找第一個不小於 35 的元素
            auto it2 = lower_bound(v.begin(), v.end(), 35);
            cout << "第一個不小於 35 的元素 (" << *it2 << ") 在索引: " << distance(v.begin(), it2) << endl; // 輸出: 40 在索引 5
            return 0;
        }
        ```
        
    
    - `upper_bound`: 在**已排序**的序列中，找到第一個**大於 (>)**給定值的元素。
        
        - 回傳一個指向該元素的迭代器。
        
        - `lower_bound` 和 `upper_bound` 搭配使用可以找到某個值在序列中的所有出現範圍。
        
        ```C++
        int main() {
            vector<int> v = {10, 20, 30, 30, 30, 40, 50};
        
            // 尋找第一個大於 30 的元素
            auto it = upper_bound(v.begin(), v.end(), 30);
            cout << "第一個大於 30 的元素 (" << *it << ") 在索引: " << distance(v.begin(), it) << endl; // 輸出: 40 在索引 5
        
            // 計算 30 的數量
            auto lb = lower_bound(v.begin(), v.end(), 30);
            auto ub = upper_bound(v.begin(), v.end(), 30);
            cout << "元素 30 的數量為: " << distance(lb, ub) << endl; // 輸出: 3
            return 0;
        }
        ```
        
    
    - `binary_search`: 在**已排序**的序列中進行二分搜尋。
        
        - 回傳 `true` 或 `false`。
        
        ```C++
        int main() {
            vector<int> v = {10, 20, 30, 40, 50}; // 必須先排序
            
            if (binary_search(v.begin(), v.end(), 30)) {
                cout << "找到元素 30。" << endl;
            } else {
                cout << "找不到元素 30。" << endl;
            }
            
            if (binary_search(v.begin(), v.end(), 35)) {
                cout << "找到元素 35。" << endl;
            } else {
                cout << "找不到元素 35。" << endl;
            }
            return 0;
        }
        ```
        
    
    - `**nth_element**`: 尋找第 n 小的元素。
        
        - 用於解決 "Top K" 或「第 K 大/小元素」問題。以平均 O(N) 的時間複雜度將第 n 個元素放到它排序後應在的位置，比 `sort` 整個陣列（O(N log N)）更有效率。
        
        ```C++
        int main() {
            vector<int> v = {3, 2, 1, 5, 6, 4};
            int k = 2; // 尋找第 2 大的元素
        
            // 第 k 大的元素，等同於第 (v.size() - k) 小的元素 (0-indexed)
            // 我們要找的元素會被放到 v.begin() + (v.size() - k) 這個位置
            auto kth_it = v.begin() + v.size() - k;
            nth_element(v.begin(), kth_it, v.end());
        
            // 執行後，*kth_it 就是第 k 大的元素。
            // 小於它的元素都在它左邊，大於等於它的元素都在它右邊（但不保證左右兩邊有序）。
            cout << "第 " << k << " 大的元素是: " << *kth_it << endl; // 輸出 5
        
            // 找中位數
            vector<int> v2 = {3, 2, 1, 5, 6, 4, 7};
            auto median_it = v2.begin() + v2.size() / 2;
            nth_element(v2.begin(), median_it, v2.end());
            cout << "中位數是: " << *median_it << endl; // 輸出 4
            return 0;
        }
        ```
        
    
    - `stable_sort`: `sort` 的穩定版本 (相等元素的相對順序不變)。
        
        如果兩個元素相等，它們在排序後的相對位置和排序前保持一致。
        
        ```C++
        struct Item {
            int key;
            string value;
        };
        
        int main() {
            vector<Item> v = {{3, "C"}, {1, "A"}, {2, "B1"}, {2, "B2"}};
        
            // 只根據 key 排序。因為是 stable_sort，key 為 2 的 "B1" 和 "B2" 的相對順序不變
            stable_sort(v.begin(), v.end(), [](const Item& a, const Item& b) {
                return a.key < b.key;
            });
        
            cout << "穩定排序後: ";
            for (const auto& item : v) {
                cout << "{" << item.key << ", " << item.value << "} ";
            }
            cout << endl; // 輸出: {1, A} {2, B1} {2, B2} {3, C}
            return 0;
        }
        ```
        
    
    - `partial_sort`: 只排序序列的前 N 個元素。
        
        - 將序列中最小的 N 個元素放到序列的前 N 個位置，並對它們進行排序。其餘元素的位置不確定。
        
        - 主要用於「前 K 個最小/最大元素」的問題。但更常見的解法是用 `priority_queue` (最小/最大堆)，效率更高，思路也更通用。
        
        ```C++
        int main() {
            vector<int> v = {5, 2, 8, 1, 9, 4, 7, 3, 6};
            
            // 將最小的 3 個元素排序後放在序列開頭
            partial_sort(v.begin(), v.begin() + 3, v.end());
        
            cout << "部分排序後的內容: ";
            for (int n : v) {
                cout << n << " "; // 輸出可能是: 1 2 3 ... (後面元素順序不保證)
            }
            cout << endl;
            return 0;
        }
        ```
        
    

- 修改序列操作 (Modifying sequence operations) - 改變元素或順序
    
    - `swap`: 交換兩個變數的值。
        
        任何排序演算法、陣列原地修改題目（例如雙指針法）的基礎操作。
        
        ```C++
        void reverse_array(vector<int>& arr) {
            int left = 0;
            int right = arr.size() - 1;
            while (left < right) {
                swap(arr[left], arr[right]);
                left++;
                right--;
            }
        }
        
        int main() {
            vector<int> v = {1, 2, 3, 4, 5};
            reverse_array(v);
        
            cout << "使用 swap 反轉陣列後: ";
            for (int n : v) {
                cout << n << " ";
            }
            cout << endl;
            return 0;
        }
        ```
        
    
    - `reverse`: 反轉序列的順序。
        
        ```C++
        int main() {
            vector<int> v = {1, 2, 3, 4, 5};
            
            reverse(v.begin(), v.end());
        
            cout << "反轉後的內容: ";
            for (int n : v) {
                cout << n << " ";
            }
            cout << endl;
            return 0;
        }
        ```
        
    
    - `next_permutation`: 產生下一個字典序排列。
        
        - 只要給定一個初始序列（通常是排序後的），就可以在 `do-while` 迴圈中輕鬆遍歷所有不重複的排列。
        
        ```C++
        int main() {
            vector<int> nums = {1, 2, 3};
        
            // 必須先對序列排序，才能保證從最小的排列開始
            sort(nums.begin(), nums.end());
        
            cout << "元素 {1, 2, 3} 的所有排列:" << endl;
            do {
                for (int n : nums) {
                    cout << n << " ";
                }
                cout << endl;
            } while (next_permutation(nums.begin(), nums.end()));
            
            return 0;
        }
        ```
        
    
    - `unique`: 移除連續的重複元素。
        
        - 和 `remove` 類似，它也只會移動元素，需要搭配 `erase` 來真正縮小容器。
        
        ```C++
        int main() {
            vector<int> v = {1, 1, 2, 2, 2, 3, 1, 1, 4};
            // 注意：unique 只會移除 "連續" 的重複項
            
            auto new_end = unique(v.begin(), v.end());
            // 此時 v 的內容可能是 {1, 2, 3, 1, 4, ?, ?, ?, ?}
            
            v.erase(new_end, v.end());
        
            cout << "unique 之後的內容: ";
            for (int n : v) {
                cout << n << " ";
            }
            cout << endl;
            return 0;
        }
        ```
        
    
    - `rotate`: 將序列中的元素向左旋轉。
        
        - 將指定的元素變成新的第一個元素。
        
        ```C++
        int main() {
            vector<int> v = {10, 20, 30, 40, 50};
            
            // 將 v.begin() + 2 (也就是 30) 作為新的第一個元素
            rotate(v.begin(), v.begin() + 2, v.end());
        
            cout << "旋轉後的內容: "; // 輸出: 30 40 50 10 20
            for (int n : v) {
                cout << n << " ";
            }
            cout << endl;
            return 0;
        }
        ```
        
    
    - `remove`: "移除" 序列中等於某個值的元素 (實際上是將不被移除的元素前移，並返回新的邏輯結尾)。
        
        - `remove` 並不會真的從容器中刪除元素，而是將所有 _不被移除_ 的元素移動到序列的前端，並回傳一個指向新的 "邏輯結尾" 的迭代器。通常會搭配容器的 `erase` 方法一起使用，來真正刪除元素。
        
        ```C++
        int main() {
            vector<int> v = {10, 20, 30, 20, 40, 50};
            
            // 將所有不等於 20 的元素往前移動
            auto new_end = remove(v.begin(), v.end(), 20);
        
            // 此時 v 的內容可能是 {10, 30, 40, 50, ?, ?}，? 代表未定義
            cout << "remove 之後，erase 之前: ";
            for(auto it = v.begin(); it != new_end; ++it) {
                cout << *it << " ";
            }
            cout << endl;
        
            // 真正刪除從 new_end 到結尾的元素
            v.erase(new_end, v.end());
        
            cout << "最終內容: ";
            for (int n : v) {
                cout << n << " ";
            }
            cout << endl;
            return 0;
        }
        ```
        
    
    - `fill`: 用一個指定的值填滿整個序列。
        
        ```C++
        int main() {
            vector<int> v(5); // 包含 5 個預設值的 vector
        
            fill(v.begin(), v.end(), 7); // 用 7 填滿整個 vector
        
            cout << "填滿後的內容: ";
            for (int n : v) {
                cout << n << " ";
            }
            cout << endl;
            return 0;
        }
        ```
        
    
    - `copy`: 複製一個序列到另一個位置。
        
        ```C++
        int main() {
            vector<int> source = {1, 2, 3, 4, 5};
            vector<int> destination(source.size()); // 目標容器需要有足夠的空間
        
            copy(source.begin(), source.end(), destination.begin());
        
            cout << "目標容器的內容: ";
            for (int n : destination) {
                cout << n << " ";
            }
            cout << endl;
            return 0;
        }
        ```
        
    
    - `replace`: 將序列中所有等於某個值的元素替換為新值。
        
        ```C++
        int main() {
            vector<int> v = {10, 20, 30, 20, 40, 20};
            
            replace(v.begin(), v.end(), 20, 99); // 將所有 20 替換為 99
        
            cout << "替換後的內容: ";
            for (int n : v) {
                cout << n << " ";
            }
            cout << endl;
            return 0;
        }
        ```
        
    
    - `transform`: 對序列中的每個元素應用一個操作，並將結果儲存到目標序列。
        
        ```C++
        int main() {
            vector<int> v1 = {1, 2, 3, 4, 5};
            vector<int> v2(v1.size());
        
            // 將 v1 的每個元素乘以 2，並存入 v2
            transform(v1.begin(), v1.end(), v2.begin(), [](int n){ return n * 2; });
        
            cout << "v2 的內容: ";
            for (int n : v2) {
                cout << n << " ";
            }
            cout << endl;
            return 0;
        }
        ```
        
    
    - `move`: 移動一個序列的元素。
        
        - 通常比 `copy` 更有效率，因為它避免了不必要的物件複製（特別是對於複雜物件）。來源物件在移動後會處於一個有效的、但未指定的狀態。
        
        ```C++
        int main() {
            vector<string> source = {"apple", "banana", "cherry"};
            vector<string> destination(source.size());
        
            move(source.begin(), source.end(), destination.begin());
        
            cout << "目標容器: ";
            for (const auto& s : destination) {
                cout << s << " ";
            }
            cout << "\n來源容器 (移動後): "; // 內容未定義，不應再使用
            for (const auto& s : source) {
                cout << "'" << s << "' ";
            }
            cout << endl;
            return 0;
        }
        ```
        
    

- 非修改序列操作 (Non-modifying sequence operations) - 查找與計數
    
    - `min`, `max`, `minmax`: 找出最小/最大值。
        
        ```C++
        int main() {
            int a = 10, b = 20;
            cout << "a 和 b 中較小的是: " << min(a, b) << endl; // 輸出 10
        
            // C++11 起支援 initializer_list，可比較多個值
            int min_val = min({5, 2, 8, 1, 9});
            cout << "幾個數字中最小的是: " << min_val << endl; // 輸出 1
        
            // minmax 回傳一個 pair，包含最小值和最大值
            auto p = minmax({5, 2, 8, 1, 9});
            cout << "最小值是: " << p.first << ", 最大值是: " << p.second << endl; // 輸出 1, 9
            return 0;
        }
        ```
        
    
    - `min_element`, `max_element`: 尋找序列中的最小/最大元素。
        
        ```C++
        int main() {
            vector<int> v = {5, 2, 8, 1, 9, 4};
        
            // 回傳指向最小元素的迭代器
            auto min_it = min_element(v.begin(), v.end());
            // 回傳指向最大元素的迭代器
            auto max_it = max_element(v.begin(), v.end());
        
            cout << "最小值 " << *min_it << " 在索引 " << distance(v.begin(), min_it) << endl;
            cout << "最大值 " << *max_it << " 在索引 " << distance(v.begin(), max_it) << endl;
            return 0;
        }
        ```
        
    
    - `count`: 計算序列中等於某個值的元素數量。
        
        ```C++
        int main() {
            vector<int> v = {10, 20, 30, 20, 40, 20};
            int value_to_count = 20;
        
            int num_items = count(v.begin(), v.end(), value_to_count);
            cout << "元素 " << value_to_count << " 出現了 " << num_items << " 次。" << endl;
            return 0;
        }
        ```
        
    
    - `count_if`: 計算序列中符合某個條件的元素數量。
        
        ```C++
        int main() {
            vector<int> v = {1, 2, 3, 4, 5, 6, 7, 8};
        
            // 使用 Lambda 表示式來計算大於 4 的元素數量
            int num_items = count_if(v.begin(), v.end(), [](int i){ return i > 4; });
            cout << "大於 4 的元素有 " << num_items << " 個。" << endl;
            return 0;
        }
        ```
        
    
    - `find`: 尋找序列中第一個等於某個值的元素。
        
        - 回傳一個指向第一個符合條件的元素的迭代器，如果找不到則回傳序列的 `end()` 迭代器。
        
        ```C++
        int main() {
            vector<int> v = {10, 20, 30, 40, 50};
            int value_to_find = 30;
        
            auto it = find(v.begin(), v.end(), value_to_find);
        
            if (it != v.end()) {
                cout << "找到元素 " << *it << " 在索引 " << distance(v.begin(), it) << endl;
            } else {
                cout << "找不到元素 " << value_to_find << endl;
            }
            return 0;
        }
        ```
        
    
    - `find_if`: 尋找序列中第一個符合某個條件 (predicate) 的元素。
        
        - Predicate 是一個回傳布林值的函式或 Lambda。
        
        ```C++
        // Predicate: 檢查數字是否為偶數
        bool is_even(int n) {
            return n % 2 == 0;
        }
        
        int main() {
            vector<int> v = {1, 3, 5, 8, 10, 12};
        
            auto it = find_if(v.begin(), v.end(), is_even);
        
            if (it != v.end()) {
                cout << "第一個偶數是: " << *it << endl;
            } else {
                cout << "找不到偶數" << endl;
            }
            return 0;
        }
        ```
        
    
    - `search`: 在一個序列中尋找另一個子序列。
        
        - 回傳一個指向子序列在原序列中起始位置的迭代器。
        
        ```C++
        int main() {
            vector<int> main_seq = {1, 2, 3, 4, 5, 6, 7, 8};
            vector<int> sub_seq = {4, 5, 6};
        
            auto it = search(main_seq.begin(), main_seq.end(), sub_seq.begin(), sub_seq.end());
        
            if (it != main_seq.end()) {
                cout << "找到子序列，起始位置在索引 " << distance(main_seq.begin(), it) << endl;
            } else {
                cout << "找不到子序列" << endl;
            }
            return 0;
        }
        ```
        
    
    - `for_each`: 對序列中的每個元素執行一個函式。
        
        ```C++
        void print_element(int n) {
            cout << n << " ";
        }
        
        int main() {
            vector<int> v = {1, 2, 3, 4, 5};
            cout << "序列中的元素: ";
            for_each(v.begin(), v.end(), print_element);
            cout << endl;
            return 0;
        }
        ```
        
    

- 數值操作 (Numeric operations)
    
    - `accumulate`: 計算序列元素的總和 (或透過自訂操作累積)。
        
        ```C++
        int main() {
            vector<int> v = {1, 2, 3, 4, 5};
            
            // 計算總和，初始值為 0
            int sum = accumulate(v.begin(), v.end(), 0);
            cout << "總和: " << sum << endl;
        
            // 計算乘積，初始值為 1
            int product = accumulate(v.begin(), v.end(), 1, multiplies<int>());
            cout << "乘積: " << product << endl;
            return 0;
        }
        ```
        
    
    - `abs`: 計算絕對值。
        
        ```C++
        int main() {
            int diff = -10;
            cout << "-10 的絕對值是: " << abs(diff) << endl;
        
            double val = -3.14;
            cout << "-3.14 的絕對值是: " << abs(val) << endl;
            return 0;
        }
        ```
        
    
    - `gcd`, `lcm`: 最大公因數與最小公倍數。
        
        ```C++
        int main() {
            int a = 54;
            int b = 24;
        
            // Greatest Common Divisor (最大公因數)
            int common_divisor = gcd(a, b);
            cout << a << " 和 " << b << " 的最大公因數是: " << common_divisor << endl; // 輸出 6
        
            // Least Common Multiple (最小公倍數)
            int common_multiple = lcm(a, b);
            cout << a << " 和 " << b << " 的最小公倍數是: " << common_multiple << endl; // 輸出 216
            return 0;
        }
        ```
        
    
    - `iota`: 用連續遞增的值填充序列。
        
        - 非常適合用來產生測試用的序列。
        
        ```C++
        int main() {
            vector<int> v(5);
            
            // 從 10 開始，用 10, 11, 12, ... 填充序列
            iota(v.begin(), v.end(), 10);
        
            cout << "iota 填充結果: ";
            for (int n : v) {
                cout << n << " "; // 輸出: 10 11 12 13 14
            }
            cout << endl;
            return 0;
        }
        ```
        
    
    - `partial_sum`: 計算序列的部分和。
        
        - 結果序列的第 i 個元素是原序列前 i 個元素的總和。
        
        ```C++
        int main() {
            vector<int> v = {1, 2, 3, 4, 5};
            vector<int> result(v.size());
        
            partial_sum(v.begin(), v.end(), result.begin());
        
            cout << "部分和: ";
            for (int n : result) {
                cout << n << " "; // 輸出: 1 3 6 10 15
            }
            cout << endl;
            return 0;
        }
        ```
        
    
    - `inner_product`: 計算兩個序列的內積。
        
        - $result=init+a_1∗b_1+a_2∗b_2+…$
        
        ```C++
        int main() {
            vector<int> v1 = {1, 2, 3};
            vector<int> v2 = {4, 5, 6};
            
            // 初始值為 0，計算 1*4 + 2*5 + 3*6
            int result = inner_product(v1.begin(), v1.end(), v2.begin(), 0);
            
            cout << "內積: " << result << endl; // 輸出: 4 + 10 + 18 = 32
            return 0;
        }
        ```
        
    

- 合併與集合操作 (Merge and set operations) - 適用於已排序序列
    
    - `merge`: 合併兩個已排序的序列。
        
        ```C++
        int main() {
            vector<int> v1 = {1, 3, 5, 7};
            vector<int> v2 = {2, 4, 6, 8};
            vector<int> dest(v1.size() + v2.size());
        
            merge(v1.begin(), v1.end(), v2.begin(), v2.end(), dest.begin());
        
            cout << "合併後的序列: ";
            for (int n : dest) {
                cout << n << " ";
            }
            cout << endl;
            return 0;
        }
        ```
        
    
    - `set_intersection`: 計算兩個集合的交集。
        
        ```C++
        int main() {
            vector<int> v1 = {1, 2, 3, 4, 5};
            vector<int> v2 = {3, 4, 5, 6, 7};
            vector<int> intersection_res;
        
            set_intersection(v1.begin(), v1.end(), 
                                  v2.begin(), v2.end(), 
                                  back_inserter(intersection_res)); // 使用 back_inserter 自動擴展容器
        
            cout << "交集: ";
            for (int n : intersection_res) {
                cout << n << " "; // 輸出: 3 4 5
            }
            cout << endl;
            return 0;
        }
        ```
        
    
    - `set_union`: 計算兩個集合的聯集。
        
        ```C++
        int main() {
            vector<int> v1 = {1, 2, 3};
            vector<int> v2 = {3, 4, 5};
            vector<int> union_res;
        
            set_union(v1.begin(), v1.end(), 
                           v2.begin(), v2.end(), 
                           back_inserter(union_res));
        
            cout << "聯集: ";
            for (int n : union_res) {
                cout << n << " "; // 輸出: 1 2 3 4 5
            }
            cout << endl;
            return 0;
        }
        ```
        
    
    - `set_difference`: 計算兩個集合的差集。
        
        - 結果包含所有在第一個序列中，但不在第二個序列中的元素。
        
        ```C++
        int main() {
            vector<int> v1 = {1, 2, 3, 4, 5};
            vector<int> v2 = {3, 4, 5, 6, 7};
            vector<int> diff_res;
        
            set_difference(v1.begin(), v1.end(), 
                                v2.begin(), v2.end(), 
                                back_inserter(diff_res));
        
            cout << "差集 (v1 - v2): ";
            for (int n : diff_res) {
                cout << n << " "; // 輸出: 1 2
            }
            cout << endl;
            return 0;
        }
        ```
        
    

- 演算法操作對象
    
    |   |   |   |   |   |
    |---|---|---|---|---|
    |演算法類別|演算法名稱 (Algorithm Name)|主要操作對象 (Primary Target Object)|常見容器範例 (Common Container Examples)|重要條件/限制 (Important Conditions/Restrictions)|
    |排序與相關操作|sort, stable_sort|一個迭代器範圍 [first, last)|vector, deque, C-style array|需要「隨機存取迭代器」  <br>(Random Access Iterator)，因此不適用於 list。|
    ||nth_element|一個迭代器範圍 [first, last)|vector, deque, C-style array|需要「隨機存取迭代器」。|
    ||binary_search|一個迭代器範圍 [first, last) 及一個值|vector, deque, list, C-style array|操作的序列必須已排序。|
    ||lower_bound, upper_bound|一個迭代器範圍 [first, last) 及一個值|vector, deque, list, C-style array|操作的序列必須已排序。|
    |修改序列操作|swap|兩個可修改的物件參考|任何類型的變數 (int, string, vector...)|物件必須是可交換的。|
    ||reverse|一個迭代器範圍 [first, last)|vector, string, deque, list|需要「雙向迭代器」 (Bidirectional Iterator)。|
    ||next_permutation|一個迭代器範圍 [first, last)|vector, string|需要「雙向迭代器」。為了遍歷所有排列，初始序列最好是排序過的。|
    ||unique|一個迭代器範圍 [first, last)|vector, deque, list|只移除連續的重複元素，通常先對序列排序。|
    ||rotate|一個迭代器範圍 [first, middle, last)|vector, string, deque, list|需要「前向迭代器」(Forward Iterator) 以上。|
    ||remove|一個迭代器範圍 [first, last) 及一個值|vector, deque, list|需要「前向迭代器」。|
    |非修改序列操作|max, min|兩個值，或一個 initializer_list|int, double, string 等可比較型別|物件必須支援 < 比較運算。|
    ||max_element, min_element|一個迭代器範圍 [first, last)|所有標準容器|需要「前向迭代器」。|
    ||find, count|一個迭代器範圍 [first, last) 及一個值|所有標準容器|需要「輸入迭代器」(Input Iterator) 以上。|
    |數值操作|accumulate|一個迭代器範圍 [first, last) 及一個初始值|vector<int>, list<double> 等數值容器|序列中的元素型別需要支援 + 運算（或自訂的二元操作）。|
    ||abs|一個數值|int, long, float, double|N/A|
    ||gcd, lcm|兩個整數值|int, long, long long|僅適用於整數型別。|
    ||iota|一個迭代器範圍 [first, last) 及一個初始值|vector, array|序列中的元素型別需要支援 ++ (遞增) 運算。|
    |合併與集合操作|merge|兩個輸入迭代器範圍，一個輸出迭代器|所有標準容器|兩個輸入序列都必須已排序。|
    

---

==迭代器 (Iterators)== ==-== 「==串起演算法與容器的萬用指標==」

- 迭代器類型
    
    |   |   |   |   |   |
    |---|---|---|---|---|
    |能力層級|迭代器類型|核心能力 (白話文)|關鍵新增操作|典型容器/用途|
    |Level 1|Input / Output|單次使用的「唯讀」或「唯寫」探測器，只能前進。|*it (讀/寫)  <br>++it|cin (讀取)  <br>cout (寫入)|
    |Level 2|Forward|可重複使用的探測器，但只能前進。|(可多次讀取同一個元素)|unordered_map  <br>forward_list|
    |Level 3|Bidirectional|可雙向移動的探測器 (可前進也可後退)。|--it|list  <br>set  <br>map|
    |Level 4|Random Access|全能型探測器，可隨意跳躍。|it + n  <br>it - n  <br>it[n]|vector  <br>deque  <br>array|
    
    - `Forward` = Input + 可重複讀取。
    
    - `Bidirectional` = Forward + 可後退 (`-`)。
    
    - `Random Access` = Bidirectional + 可跳躍 (`+`, , `[]`)。
    
    - **關鍵應用**：`std::sort` 演算法需要能夠隨意比較和交換元素，因此它**要求**容器必須提供 **Random Access Iterator**。這就是為什麼 `std::list` 不能直接使用 `std::sort` 的原因。
    

- 最重要的四個迭代器操作：
    
    - `**container.begin()**`
        
        - **指向**：容器的**第一個元素**。
        
        - **用途**：作為走訪的起點。
        
    
    - `**container.end()**`
        
        - **指向**：**「最後一個元素的下一個位置」**。
        
        - **重點**：它是一個**哨兵**或**標記**，本身**不儲存任何元素**。
        
        - **區間概念**：`begin()` 和 `end()` 構成了一個「左閉右開」的區間 `[begin, end)`，這是 C++ STL 中最常見的表示法。
        
    
    - `**container.rbegin()**` (reverse begin)
        
        - **指向**：**反向視角**的**第一個元素** (也就是正向的最後一個元素)。
        
        - **用途**：從後往前走訪的起點。
        
    
    - `**container.rend()**` (reverse end)
        
        - **指向**：**反向視角**的「最後一個元素的下一個位置」(也就是正向 `begin()` 前的位置)。
        
        - **用途**：從後往前走訪的終點標記。
        
    
    ```C++
    std::vector<int> v = {10, 20, 30};
    
    // 正向遍歷
    for (auto it = v.begin(); it != v.end(); ++it) {
    // 輸出: 10 20 30
    }
    
    // 反向遍歷
    for (auto it = v.rbegin(); it != v.rend(); ++it) {
    // 輸出: 30 20 10
    }
    ```
    

---

==函式物件 (Functors / Function Objects))== - 「演算法需要一個判斷標準或操作策略」

- **函式物件 (Functors) 是什麼？**
    
    - **核心定義**：一個「行為像函式的物件」。
    
    - **實作方式**：在一個 `class` 或 `struct` 中，對 `()` 運算子進行多載 (overload `operator()`)。這使得該類別的物件可以像函式一樣被呼叫。
    
    - **最大優勢**：與一般函式不同，**Functor 可以擁有「狀態」(state)**。因為它本質上是一個物件，所以它可以包含成員變數，在多次呼叫之間儲存和利用資訊。
    

- C++ 內建的函式物件
    
    - **算術類 (Arithmetic Functors)**
        
        - `plus<T>`：執行 `a + b`。
        
        - `minus<T>`：執行 `a - b`。
        
        - `multiplies<T>`：執行 `a * b`。
        
        - `divides<T>`：執行 `a / b`。
        
    
    - 比較類 (Comparison Functors)
        
        - `greater<T>`：判斷 `a > b`。
        
        - `less<T>`：判斷 `a < b`。
        
        - `equal_to<T>`：判斷 `a == b`。
        
        - `not_equal_to<T>`：判斷 `a != b`。
        
        - `greater_equal<T>`：判斷 `a >= b`。
        
        - `less_equal<T>`：判斷 `a <= b`。
        
    
    - **邏輯類 (Logical Functors)**
        
        - `logical_and<T>`：執行 `a && b`。
        
        - `logical_or<T>`：執行 `a || b`。
        
        - `logical_not<T>`：執行 `!a`。
        
    
      
    

---

# C++ 專屬技巧 todo

- **迭代器 (Iterators)**：熟練使用 `for (auto& element : container)` 迴圈，簡潔且不易出錯。

- **型別推斷 (Type Inference)**：多用 `auto` 來簡化複雜的型別宣告。

- **Lambda 函式**：在需要自訂比較函式的演算法（如 `sort`）中非常方便。
    
    ### 1. Lambda 的基本組成
    
    一個完整的 Lambda 長這樣：`[ 捕獲列表 ] ( 參數列表 ) -> 回傳型別 { 函數本體 };`
    
    - `**[]**` **捕獲列表 (Capture Clause)**：讓 Lambda 可以存取外部變數。
    
    - `**()**` **參數列表 (Parameters)**：跟一般函數一樣，傳入需要的參數。
    
    - `**> type**` **回傳型別**：通常可以省略，編譯器會自動推導（除非邏輯太複雜）。
    
    - `**{}**` **函數本體**：具體的邏輯程式碼。
    
    ---
    
    ### 2. 捕獲列表的各種玩法
    
    這是 Lambda 最強大的地方。決定了 Lambda 如何「看」到外部的變數：
    
    - `[]`：不捕獲任何外部變數。
    
    - `[x]`：以 **值傳遞 (by value)** 捕獲變數 `x`（唯讀複本）。
    
    - `[&x]`：以 **引用傳遞 (by reference)** 捕獲 `x`（可以修改原變數）。
    
    - `[=]`：以 **值傳遞** 捕獲當前作用域的所有變數。
    
    - `[&]`：以 **引用傳遞** 捕獲當前作用域的所有變數。
    
    ---
    

- **I/O 優化** (通常在競賽中更需要，LeetCode 較少卡 I/O)：C++

- **位元運算 (Bit Manipulation):**
    
    - 用位移操作代替乘除法 (例如 `x << 1` 代替 `x * 2`)。
    
    - 用 `x & 1` 判斷奇偶數。
    

---

# 變數命名

|變數名稱|常見用途|範例|
|---|---|---|
|基本整數與迴圈 (Integers & Loops)|||
|`i, j, k`|迴圈計數器。|`for (int i = 0; i < n; ++i)`|
|`n, m`|數量或大小。|`int n; cin >> n; vector<int> arr(n);`|
|`x, y, z`|通用的整數值或座標。|`int x, y; cin >> x >> y;`|
|`a, b, c`|通用的整數值。|`int gcd(int a, int b) { ... }`|
|`cnt, count`|計數器。|`int cnt = 0; for(int x : arr) if(x > 0) cnt++;`|
|`ans, res`|最終答案。|`long long ans = 0; ... cout << ans << endl;`|
|`sum`|總和。|`long long sum = 0; for(int x : nums) sum += x;`|
|`idx, index`|索引值 (Index)。|`int idx = -1;`|
|`l, r`|左右指針 (Left / Right)。|`int l = 0, r = n - 1;`|
|`start, end`|區間的起點和終點。|`int start = 0, end = n - 1;`|
|`mid`|中間值。|`int mid = l + (r - l) / 2;`|
|陣列與資料結構 (Arrays & Data Structures)|||
|`arr, a`|陣列 (Array)。|`vector<int> arr(n);`|
|`nums`|數字陣列 (Numbers)。|`vector<int> nums;`|
|`v`|向量 (Vector)。|`vector<int> v;`|
|`s`|字串 (String) 或 集合 (Set)。|`string s; 或 set<int> s;`|
|`q`|佇列 (Queue)。|`queue<int> q;`|
|`stk`|堆疊 (Stack)。|`stack<int> stk;`|
|`pq`|優先佇列 (Priority Queue)。|`priority_queue<int> pq;`|
|`mp, map`|映射 (Map)。|`map<string, int> mp;`|
|圖論 (Graph Theory)|||
|`V, n`|頂點數量 (Vertices)。|`int V, E; cin >> V >> E;`|
|`E, m`|邊的數量 (Edges)。|`for(int i=0; i<m; ++i){...}`|
|`adj`|鄰接串列 (Adjacency List)。|`adj[u].push_back(v);`|
|`g, graph`|圖。|`vector<int> g[MAXN];`|
|`u, v, w`|頂點和權重。|`cin >> u >> v >> w;`|
|`s, t`|起點和終點 (Source / Target)。|`int s = 0, t = n - 1;`|
|`dist, d`|距離 (Distance)。|`vector<int> dist(n, -1);`|
|`vis, visited`|是否訪問過。|`vector<bool> visited(n, false);`|
|`parent, p`|父節點。|`vector<int> parent(n);`|
|動態規劃 (Dynamic Programming)|||
|`dp`|DP 陣列/表格。|`vector<vector<int>> dp(n, vector<int>(m, 0));`|
|`memo`|記憶化搜尋的陣列 (Memoization)。|`int memo[1001]; memset(memo, -1, sizeof(memo));`|
|網格/矩陣 (Grid / Matrix)|||
|`R, H, n`|行數 (Rows / Height)。|`int R, C; cin >> R >> C;`|
|`C, W, m`|欄數 (Columns / Width)。|`vector<vector<int>> grid(R, vector<int>(C));`|
|`grid, mat`|二維網格或矩陣。|`grid[i][j]`|
|`dx, dy`|方向陣列。|`int dx[] = {0, 0, 1, -1}; int dy[] = {1, -1, 0, 0};`|
|常數 (Constants)|||
|`MOD`|模數 (Modulo)。|`const int MOD = 1e9 + 7;`|
|`INF`|無窮大 (Infinity)。|`const int INF = 0x3f3f3f3f;`|
|`PI`|圓周率。|`const double PI = acos(-1.0);`|

  

---