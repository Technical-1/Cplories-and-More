# C++lories & More

A command-line meal planner that builds a personalized weekly meal plan from the USDA National Nutrient Database — powered by two associative-container implementations (an ordered map and an unordered map) written from scratch in C++.

The interesting part isn't the meal plan; it's what's underneath it. Rather than reach for `std::map` and `std::unordered_map`, I implemented both data structures by hand — a binary search tree and a separately-chained hash table — and wired the program to benchmark them head-to-head on real lookups over ~8,800 ingredients. The nutrition app is the realistic workload that makes the comparison meaningful.

> Course project for COP3530 (Data Structures & Algorithms), built with teammates Julien Wakim and Carson Schmidt.

## Features

- **Personalized weekly meal plans** — enter your sex, weight, height, age, and activity level, and the program computes your daily calorie target and assembles five days of breakfast/lunch/dinner that fit it.
- **Dietary restriction filtering** — exclude any ingredient (by substring) and meals containing it are skipped during curation.
- **Lose-vs-gain targeting** — shifts the daily target ±500 kcal off maintenance depending on your goal.
- **Live data-structure benchmark** — search for or insert an ingredient and the program reports lookup/insert latency for the ordered map vs. the unordered map in microseconds.
- **From-scratch containers** — an ordered map (BST) and an unordered map (hash table with separate chaining and dynamic rehashing), no STL associative containers in the hot path.

## Tech Stack

- **Language**: C++14
- **Build**: CMake 3.21
- **Data**: USDA National Nutrient Database (`nndb_flat.csv`, ~8,800 foods)
- **Standard library**: `<chrono>` for benchmarking, `<forward_list>` for hash buckets, `<sstream>`/`std::quoted` for CSV parsing

## Getting Started

### Prerequisites

- A C++14-capable compiler (GCC, Clang, or MSVC)
- CMake ≥ 3.21
- `nndb_flat.csv` present in the working directory (included in the repo)

### Build & Run

```bash
cd "C++lories&More"
cmake -S . -B build
cmake --build build
# run from the directory containing nndb_flat.csv so the data file is found
./build/C__lories_More
```

Or compile directly without CMake:

```bash
cd "C++lories&More"
g++ -std=c++14 main.cpp Map.cpp UnorderedMap.cpp -o cplories
./cplories
```

### Usage

The program presents a numbered menu:

```
1. Dietary Restrictions   # list ingredients to exclude (comma-separated)
2. Activity Level         # 1 (sedentary) – 5 (very active)
3. Health Information     # sex, weight, height, age, lose/gain goal
4. Curate Meal Plan       # generate the 5-day plan
5. Time to Find Ingredient# benchmark ordered vs. unordered map
6. Quit
```

Fill in options 1–3, then choose 4 to generate your plan. Option 5 runs the data-structure comparison on any ingredient you type.

## Project Structure

```
C++lories&More/
├── main.cpp           # CLI, CSV ingestion, calorie model, meal-curation algorithm
├── Map.h / Map.cpp    # Ordered map — binary search tree
├── UnorderedMap.h / .cpp  # Unordered map — hash table with separate chaining
├── CMakeLists.txt     # C++14 build definition
└── nndb_flat.csv      # USDA National Nutrient Database (data source)
```

## Data Source

USDA National Nutrient Database — [data.world/craigkelly/usda-national-nutrient-db](https://data.world/craigkelly/usda-national-nutrient-db)

## License

Unlicensed (personal/academic project).

## Authors

Jacob Kanfer — [GitHub](https://github.com/Technical-1) · with Julien Wakim and Carson Schmidt (COP3530 team).
