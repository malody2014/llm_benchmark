
# 大模型测评记录 - 编程部分

## 简介
1. 本评测是个人性质，使用滚动更新的私有题库进行长期跟踪评测。
2. 入选编程测试的模型至少要具备32K上下文和8K的输出能力。模型必须提供API。
3. 在语言选择上，主要考察5种语言：TypeScript，Java，Golang，Python，C#和C++。涵盖了前端，后端，客户端，数据分析和游戏客户端开发等场景。
4. 在问题设置上，题目都来自笔者私有项目的改造，或自行设计的场景，无任何互联网开源代码。
5. 所有问题均不涉及第三方SDK，行业逻辑等。

---

## 评测方法
1. 模型优先使用官方推荐的温度值(下文有备注)，如果没有推荐，则使用默认温度0.1。推理模型限制思考长度30K，输出长度10K，无法分别设置的模型，设置总输出为40K。非推理模型设置输出长度10K。模型支持的MaxToken达不到上限，就按模型上限。其他参数按模型默认。
2. 每道题有至少1个得分点/用例，回答每正确一点即得1分。最终得分是得分除以得分点总数，再乘以10。（即每道题满分10分）
3. 每题限定了输入和输出格式，大模型输出代码直接用于编译和运行，如果是依赖问题，笔者负责解决，但编译失败记0分，运行异常记0分。
4.人工检查所有代码，对于靠默认输出，兜底值混分的情况，即使答案正确，也不计分。

### 运行环境
* Python: 3.9.6
* TypeScript: node v22.14.0,  tsc  5.8.2
* Golang: 1.20.7
* Java: 1.8.0_201
* C#: dotnet5.0
* C++: Apple clang version 16.0.0 (clang-1600.0.26.6) 限定C++17以内的语言特性
---
### 题目大纲
```
1、魔方旋转，输出魔方指定面的颜色 (6种语言)
2、特殊正则表达式的解析函数，输出匹配结果 (6种语言)
3、迷宫寻路，给出迷宫寻路的规则，输出路径 (6种语言)
4、售票系统，模拟简化版12306售票系统，输出指定用户的购票结果 (6种语言)
7、来自第1题，抽掉全部注释和一半代码，不做任何提示，要求补全 (Python、TypeScript)
9、解析器实现，类Markdown解析，给类Markdown原文和标准的Html翻译版本，要求推导出解析过程，输入超长上下文 (C#、 Golang)
10、三视图投影，给空间三视图投影数据，求空间物体的所有可能体积。需要合理设计数据结构，正确穷举空间结构，并正确计算体积（TypeScript、Java、C++）
11、拼图问题，求完成指定形状所需的拼图块及其摆放位置（C#、Golang）
12、函数计算器，求输入各类函数的交点。目前仅限最高三次函数。（Python、Java、C++）
```
---
## 最新成绩（Updated 25-07-29）
| **模型**                       | **原始分数** | **原始中位** | **运行异常** | **语法错误** | **0分率** | **总异常** | **极限分数** | **中位分数** | **中位差距** | **平均耗时(秒)** | **平均代码行** | **成本(元)** |
|------------------------------|----------|----------|----------|----------|---------|---------|----------|----------|----------|-------------|-----------|-----------|
| **OpenAI o4 mini(high)**     | 279.916  | 240.29   | 1.11%    | 3.33%    | 6.67%   | 11.11%  | 77.75    | 66.75    | 14.16%   | 106         | 145       | ¥11.81    |
| **Claude Sonnet 4(Think)**   | 272.421  | 241.13   | 1.11%    | 5.56%    | 3.33%   | 10.00%  | 75.67    | 66.98    | 11.49%   | 163         | 149       | ¥34.77    |
| **Qwen3-Coder-480B-A35B** _**3_ | 262.27 | 187.34 | 5.56%     | 4.44%     | 10.00% | 20.00% | 72.85     | 52.04   | 28.57%   | 46           | 200 | ¥1.91 |
| **Gemini 2.5 Pro**           | 260.073  | 208.98   | 2.22%    | 7.78%    | 8.89%   | 18.89%  | 72.24    | 58.05    | 19.65%   | 92          | 186       | ¥25.49    |
| **DeepSeek R1 0528**  _**1_       | 249.684  | 177.28   | 3.33%    | 5.56%    | 13.33%  | 22.22%  | 69.36    | 49.25    | 29.00%   | 629         | 173       | ¥6.35     |
| **Claude Sonnet 4**          | 245.745  | 219.69   | 3.33%    | 4.44%    | 7.78%   | 15.55%  | 68.26    | 61.02    | 10.60%   | 30          | 183       | ¥6.50     |
| **GPT4.1 mini**              | 231.80   | 183.15   | 2.22%    | 7.78%    | 3.33%   | 13.33%  | 64.39    | 50.87    | 20.99%   | 34          | 228       | ¥0.72     |
| **Qwen3-235B-A22B-Instruct-2507** | 227.65 | 152.77| 4.44%   | 16.67%   | 13.33%   | 34.44%  | 63.24   | 42.44     | 32.89%   | 112         | 221       | ¥0.36 |
| **Qwen3-235B-A22B(Think)**   | 219.208  | 179.39   | 2.22%    | 6.67%    | 20.00%  | 28.89%  | 60.89    | 49.83    | 18.17%   | 315         | 164       | ¥8.69     |
| **Doubao-Seed-1.6(Think)**   | 213.143  | 157.55   | 3.33%    | 14.44%   | 11.11%  | 28.88%  | 59.21    | 43.76    | 26.08%   | 310         | 171       | ¥3.62     |
| **Doubao-Seed-1.6-thinking** | 209.598  | 146.06   | 1.11%    | 18.89%   | 15.56%  | 35.56%  | 58.22    | 40.57    | 30.32%   | 446         | 181       | ¥4.28     |
| **Grok4**                    |	209.279	|198.45 	 |0.00%	    |5.56%	   |12.22%	 |17.78%	 |58.13 	  |55.12 	   |5.18%	    |255	        |138	      |¥61.38     |
| **Gemini 2.5 flash(Think)**  | 208.31   | 162.15   | 1.11%    | 11.11%   | 18.89%  | 31.11%  | 57.86    | 45.04    | 22.16%   | 72          | 193       | ¥1.78     |
| **GLM-4.5**                 | 204.791 | 138.66 | 5.56% | 3.33% | 16.67% | 25.56% | 56.89 | 38.52 | 32.29% | ¥0.40 |
| **DeepSeek V3 0324**         | 196.986  | 136.93   | 10.00%   | 4.44%    | 13.33%  | 27.77%  | 54.72    | 38.04    | 30.49%   | 139         | 174       | ¥0.86     |
| **OpenAI GPT-4o 0326**       | 181.5    | 136.15   | 22.22%   | 4.44%    | 7.78%   | 34.44%  | 50.42    | 37.82    | 24.99%   | 11          | 141       | ¥4.47     |
| **kimi-k2-0711-preview** _**2_|	178.24 	|97.71 	   |5.56%	    |7.78%	   |18.89%	 |32.23%	 |49.51 	  |27.14 	   |45.18%	  |114	        |161	      |¥0.83      |
| **Grok3 Beta**               | 174.097  | 102.06   | 13.33%   | 5.56%    | 14.44%  | 33.33%  | 48.36    | 28.35    | 41.38%   | 17          | 139       | ¥4.40     |
| **Grok3 mini**               | 168.649  | 142.50   | 1.11%    | 7.78%    | 37.78%  | 46.67%  | 46.85    | 39.58    | 15.50%   | 123         | 115       | ¥1.29     |
| **Doubao-Seed-1.6**          | 160.991  | 125.95   | 3.33%    | 12.22%   | 17.78%  | 33.33%  | 44.72    | 34.99    | 21.77%   | 22          | 182       | ¥0.44     |
| **Qwen3-235B-A22B**          | 153.57   | 125.85   | 7.78%    | 18.89%   | 7.78%   | 34.45%  | 42.66    | 34.96    | 18.05%   | 28          | 180       | ¥0.37     |
| **Kimi-Dev-72B**             | 101.35   | 54.65    | 8.89%    | 23.33%   | 27.78%  | 60.00%  | 28.15    | 15.18    | 46.08%   | 170         | 116       | -         |

* _**1 官方API不支持调节温度_
* _**2 使用推荐温度0.6_
* _**3 使用推荐温度0.7_
---

## 更新机制
* 新模型测试后，总榜实时更新
* 每月5号做一次成绩归档
* 每个模型的详细评测首发在知乎个人号: [知乎主页](https://www.zhihu.com/people/toyama)，和微信公众号：**大模型观测员**

![qrcode_for_gh_ced94128890d_258](https://github.com/user-attachments/assets/c624c1db-7821-4f45-98da-5fac0bc34f4d)



