★ PART 1 — CLEANING CREW COORDINATION (PEHLA PROJECT)
“2 Robots ek 2D grid ko efficiently clean karte hain”
1️⃣ GRID KYA HAI?

Grid = ek 2D rectangular area (jaise graph paper).

Har cell ek block hota hai.

Kuch cells dirty ho sakte hain (cleaning required).

Agents (robots) kisi ek position se shuru hote hain.

Example:

20 rows × 28 cols grid


Iska matlab 20×28 = 560 cells.

2️⃣ DIRTY CELLS — random dirt placement

Hum grid me randomly kuch cells ko dirty mark karte hain.

DIRT_PERCENT = 18%
Total cells = 560
Dirty = 560 × 0.18 ≈ 100 cells

3️⃣ ROBOTS — DO AGENTS

2 robots placed at:

(2,2) → Agent 0
(17,25) → Agent 1


Yeh start positions hoti hain.

4️⃣ CORE PROBLEM

DONO robots ek hi jagah dubara na jayein
→ matlab non-overlapping cleaning
→ matlab division of work is required.

5️⃣ VORONOI PARTITION / NEAREST-ROBOT ASSIGNMENT

This is the heart of coordination.

⚡ Concept:

Jis robot ke start point ke sabse kareeb jo cell hote hain, woh usi robot ka kaam.

Matlab har dirty cell ke liye:

distance to Agent 0
distance to Agent 1


Jiski distance kam → assign to that agent.

Use kiya gaya distance = Manhattan Distance

Manhattan Distance (simple):
|x1 - x2| + |y1 - y2|


Why Manhattan?

Grid me diagonal movement allowed nahi hota

Isliye horizontal + vertical moves ka simple sum

Yeh step ensure karta hai ki
→ Robot dono ek hi dirt cell clean karne nahi jayenge
→ Kaam fair aur neat divide hota hai

6️⃣ ROUTE PLANNING — “Kaise ek robot apne assigned dirt ko clean kare?”
Step 1 — Greedy Nearest Neighbor (TSP heuristic)

TSP = Travelling Salesman Problem
Hard hota optimal solve karna, toh greedy NN use karte hain:

Algorithm:

Robot jahan hai → sabse kareeb wala dirty cell choose karo

Wahan jao

Fir next nearest choose karo

Repeat until saari assigned dirt clean ho jaye

Why Greedy?

Simple

Fast

Good enough for hackathon project

7️⃣ A* (A-Star) Pathfinding

Whenever robot 1 dirty cell se next dirty cell ja raha hota hai → woh A* algorithm use karta hai.

A* kya karta hai?

Grid me shortest path find karta hai using:

f = g + h
g = actual cost so far (steps taken)
h = heuristic (future guess: manhattan distance)

Why A*?

Fast

Optimal

Perfect for robot path navigation

Manhattan distance heuristic is admissible (kabhi underestimate nahi karta)

8️⃣ SIMULATION

Simulation = robot ki movement time-step wise.

Har timestep:

Robot apne planned path me next cell me move karta hai

Agar woh cell dirty ho → clean ho jata hai

Coordinates and cleaned cells record hote hain

9️⃣ VISUALIZATION — 3 Panels

Matplotlib se 3 images generate hoti hain:

1. Initial state

Dirty cells (yellow)

Agent starts (blue)

2. Planned paths

Robot 1 path

Robot 2 path

Assigned zones

3. Final cleaned map

Cleaned cells

No overlaps

Judges ko dikhaane ke liye perfect.

🔟 METRICS — Performance Evaluation
Important metrics:
Metric	Meaning
Coverage	Kitna % dirt cleaned
Total steps	Dono robots ki total distance
Makespan	Last robot ko finish karne ka time
Efficiency	Cleaned per step

Yeh metrics aapko compare karne me help karte hain.

⚡ EXTRA CONCEPTS
Why Coordination Is Needed?

Agar robots communicate na karein:

Dono ek hi dirt pe jaa sakte hain

Time waste

Energy waste

Collision possible

Voronoi assignment → fixes all

Why Greedy?

Simple & fast

For hackathon demo → perfect

Why A*?

Best algorithm for grid pathfinding

Fast

Accurate

Judges ko pata hota hai, so good impression

⭐ PART 2 — RESCUE BOT SQUAD
“Agents trapped victims ko dhoond kar rescue karte hain inside maze”
1️⃣ MAZE GENERATION

Grid ke andar:

1 = Wall

0 = Free cell

Walls random generate using WALL_DENSITY

Walls create complexity
→ robots ko navigate karna padta hai
→ BFS/A* realistic lagta hai

2️⃣ BFS for EXPLORATION

BFS = Breadth-First Search
Grid exploration ke liye best.

Why BFS?

Guarantees shortest path in unweighted grid

Perfect for exploring maze

Sab reachable cells mil jaate hain

Parent map se path reconstruct kiya ja sakta hai

BFS returns:

reachable set → kin cells tak pohoncha ja sakta hai

parent map → shortest path reconstruct karne ke liye

3️⃣ VICTIM REACHABILITY

Har agent BFS perform karta hai apne start se.

Agar koi victim reachable nahi hai (walls se block):

→ We ignore that victim
→ Because rescue possible hi nahi

4️⃣ LOGIC-BASED ASSIGNMENT (Nearest agent wins)

Har victim ko assign karte hain:

Jo agent BFS se reach kar sakta hai

Usme se jo nearest ho Manhattan distance se

Yeh simple, neat and logical strategy hai
Hackathon ke liye enough + explain karne me easy.

5️⃣ PATH PLANNING — A*

Victim tak shortest path find karne ke liye A* use hota hai.

BFS bhi chal sakta tha, but:

BFS short path deta hai

A* fastest short path deta hai

Maze me A* + Manhattan is ideal

6️⃣ SIMULATION

Har timestep robot move karta hai:

Agar victim wale cell pe pahunch gaya → rescue ho gaya

Animation me har second movement dikhta hai

7️⃣ VISUALIZATION

Same concept like cleaning project but now:

1 = wall

2 = victim

3 = rescued victim

4 = agent planned path

5+ = agents

Animation = judges ko “wow factor”.

8️⃣ METRICS

Total victims rescued

Makespan (total time)

Total movement

Efficiency = rescued per step

Compare different maze runs

⭐ DONO PROJECTS ME COMMON CONCEPTS
Concept	Use in Cleaning	Use in Rescue
Grid	Dirty cell map	Maze representation
Agents	Cleaners	Rescue robots
BFS	(optional) exploration	Primary exploration
A*	Route between tasks	Route to victims
Greedy order	TSP heuristic	Victim order selection
Assignment strategy	Voronoi	Nearest reachable agent
Simulation	Cleaning over time	Rescue operation
Visualization	3-panel	3-panel + animation
Metrics	cleaning efficiency	rescue efficiency
⭐ AB TUM KYA EXPLAIN KAR SAKTE HO (HACKATHON ME)
✔ How robots divide work (Voronoi / logic-based assignment)
✔ How robots find path (A*)
✔ How robots explore maze (BFS)
✔ Why Manhattan distance
✔ Why greedy ordering
✔ Why simulation needed
✔ Why animation powerful visualization
✔ Why metrics important
✔ Why no collision / overlap
✔ How system can scale to many robots
✔ Challenges solved:

Path planning

Coordination

Exploration

Collision avoidance

Performance evaluation

PART 4 — RESOURCE COLLECTION TEAM

“Multiple agents ek map me scattered resources collect karte hain shared task queue aur distributed logic ka use karke.”

1️⃣ GRID / MAP KYA HAI?

Ek 2D grid jisme:

0 = free cells

1 = obstacles

2 = resource cells

Agents randomly placed, obstacles randomly placed.

2️⃣ RESOURCES — Scattered across map

NUM_RESOURCES = 40

Random free cells par place kiye jaate hain.

Agents ko ye sab collect karne hote hain.

3️⃣ AGENTS — Multi-agent system

Example:
NUM_AGENTS = 4

Har agent ek unique position se start hota hai.

4️⃣ CORE PROBLEM

Agents ko duplicate kaam nahi karna hai:

Same resource competitive do agents collect na karein

Har resource exactly 1 agent should pick

Solution: Shared Task Queue

5️⃣ SHARED TASK QUEUE — Kaise kaam karta hai?
⚡ Concept:

Saare resources ek global list/queue me store hote hain.

Jab agent free hota hai → woh queue me available resource choose karta hai.

Jo resource assign ho gaya → queue se remove kar diya jata hai.

Isse duplication avoid hota hai.

6️⃣ DISTRIBUTED DECISION LOGIC

Do simple strategies:

A) Nearest Strategy

Agent free hua → queue se nearest resource pick karega

Cost = Manhattan distance

Pros: Simple & fast
Cons: Load balancing average

B) Bid Strategy (distributed intelligent logic)

Har agent ek “bid” calculate karta hai:

bid = 1 / (distance + 1)

Jis agent ka bid zyada → usko resource milta hai

Yeh natural division create karta hai

Agents un resources ko pick karte hain jinke liye unka advantage zyada hai

Pros:

Less conflict

Load balancing better

Smart behavior without central control

7️⃣ PATH PLANNING — A* ka use har resource tak jaane ke liye

Agent ko pick kiye hue resource tak shortest path A* de deta hai.

A* obstacles avoid karta hai.

8️⃣ OPPORTUNISTIC COLLECTION

Agar agent kisi resource ke upar se randomly guzar jaaye:
→ Wo turant collect kar leta hai (queue check kiye bina)

Yeh real-world jaisa behavior produce karta hai.

9️⃣ SIMULATION

Har timestep:

Agents move along A* path

Agar resource cell hai → collect

Collected resource queue se remove

Agent free → new work assigned

Logs update hote hain

🔟 VISUALIZATION

Outputs:

1. Final Map:

Obstacles (1)

Original resources (2)

Final agent positions (4+)

2. Bar Plot:

Har agent ne kitne resources collect kiye

3. Animation:

Step-by-step movement

Live collection count

Judges ko yeh bahut pasand aata hai.

⭐ METRICS
Metric	Meaning
Total collected	kitne resources collect hue
Steps taken	total simulation steps
Per-agent collection	fairness measure
Efficiency	collection rate per step
⭐ EXTRA CONCEPTS

Why shared queue?
Duplicate work avoid hota hai.

Why bid strategy?
Better load-balancing milta hai.

Why A?*
Obstacle-aware shortest path.

Why opportunistic pickup?
Realistic multi-agent emergent behavior.
